# DP
----
* 問題分解成子問題(同遞迴)
* 重複子問題(不同於遞迴)
----
## 特性
* 重複子問題
* 最佳子結構
* 無後效性
----
## 步驟
* 訂出狀態
* 導出轉移
* 設好基底
----
時間複雜度，通常就會是「使用到的狀態個數」乘上「轉移時間」了。
------
# 費式數列
----
## DP式
* 狀態：$f(x)$代表費式數列第$n$項
* 轉移：$f(n)=f(n-1)+f(n-2)$
* 基底：$f(n)=n,where$ $n\leq 1$
----
## 遞迴版本
```cpp
int f(int n){
    if(n<=1)return n;
    return f(n-1)+f(n-2);     
}
```
----
* 時間太長
* 太多重復子問題
----
## top down
```cpp
int dp[N]
int f(int n){
    if(n<=1)return n;
    if(dp[n])return dp[n];
    return dp[n]=f(n-1)+f(n-2);     
}
```
----
* 好處是容易寫出來
* 缺點是遞迴的常數非常大
----
## Buttom up
```cpp
int dp[N];
int f(){
    dp[0]=dp[1]=1;
    for(int i=2;i<N;i++){
        dp[i]=dp[i-1]+dp[i-2];
    }
}
```
----
* 難寫但時間常數小
* 可用滾動陣列
----
## 滾動陣列
* 用不到的狀態可被覆蓋
* 資源回收再利用
------
# 經典問題
----
* 背包問題
* LCS
* LIS
------
# 背包問題
----
背包問題中，會給你背包的容量C，以及N樣物品，它們有不同的重量w和價值v，背包裡物品價值總和最大為何?
----
根據物品數量限制不同分成
* 01背包
* 無限背包
* 有限背包
----
## 01背包
01背包限制每樣物品最多只能放一個
----
### dp式
* 狀態：$dp[n][i]$ $=$ 使用$1$到$n$ 個物品湊出重量 i 時,所可得到的最大價值。
* 轉移：$dp[n][i] = max(dp[n-1][i-w[n]] + v[n], dp[n-1][i])$
* 基底：$dp[0][0] = 0$, $dp[0][i] = -INF$ when $i>0$
----
以防在DP的過程不小心用到，湊不出來的狀態要設成負無限大，或是使用if判斷取代預設。
----
```cpp
dp[N][C];
memset(dp,-INF,sizeof(dp));
dp[0][0]=0;
for(int i=0;i<N;i++){
    for(int j=w[i];j<=C;++j){
        dp[i][j]=max(dp[i-1][j−w[i]]+v[i],dp[i-1][j]);
    }
}
```
----
* 時間空間複雜度皆為$O(NC)$
* 空間可優化
----
利用滾動陣列降為$O(2N)$ 
```cpp
dp[N][C];
memset(dp,-INF,sizeof(dp));
dp[0][0]=0;
for(int i=0;i<N;i++){
    for(int j=w[i];j<=C;++j){
        dp[i&1][j]=max(dp[i&1^1][j−w[i]]+v[i],dp[i&1^1][j]);
    }
}
```
----
由後向前轉移，再降為$O(N)$
```cpp
dp[N];
memset(dp,-INF,sizeof(dp));
dp[0]=0;
for(int i=0;i<N;i++){
    for(int j=C;j>=w[j];j--){
        dp[j]=max(dp[j−w[i]]+v[i],dp[j]);
    }
}
```
----
## 無限背包
* 每樣物品能放無限多個
----
### DP式
* 狀態：$dp[n][i]$ $=$ 使用 $1$到$n$ 個物品湊出重量 i 時,所可得到的最大價值。
* 轉移：$dp[n][i] = max(dp[n - 1][i - w[n]] + v[n],$ $dp[n][i - w[n]] + v[n], dp[n - 1][i])$
* 基底：$dp[0][0] = 0, dp[0][i] = -INF$ when $i>0$
----
時間複雜度為$O(NC\Sigma\frac{C}{w_i})$
```cpp
dp[N];
memset(dp,-INF,sizeof(dp));
dp[0]=0;
for(int i=0;i<N;i++){
    for(int j=w[i];j<=C;j++){
        for(int k=1;k*w[i]<=C;k++){
            dp[j]=max(dp[j−w[i]]+v[i],dp[j]);
        }
    }
}
```
----
回顧01背包最後一個範例
* 由後往前確保每個物品都只放一個
* 無限背包則是放越多越好
* 那就由前往後
----
```cpp
memset(dp,-INF,sizeof(dp));
dp[0]=0;
for(int i=0;i<N;i++){
    for(int j=w[i];j<=C;j++){
        dp[j]=max(dp[j−w[i]]+v[i],dp[j]);
    }
}
```
----
## 有限背包
* 有限背包每樣物品能放限制最多可以放$a_i$個
----
* 時間複雜度為$O(NC\Sigma a_i)$
* 用二進位角度，複雜度可壓到$O(NC\Sigma(\log a_i))$
* 單調對列優化，再降到$O(NC)$
------
# LCS
最長共同子序列 (Longest Common Subsequence)
----
## 子序列
* 子序列是指一個序列去除某些元素後所形成的新序列(當然也可以不刪除任何東西)
----
## LCS
* 兩個字串去除元素後變成相同的序列的最長長度
----
## DP式
* 狀態：$dp[i][j]$ $=$ 使用 $a[1]$到$a[i]$和$b[1]~b[j]$ 的LCS長度。
* 轉移：$dp[i][j] = dp[i-1][j-1]+1 \ if\ a[i]=b[j]$ $max(dp[i-1][j],dp[i][j-1])\ else$
* 基底：$dp[i][0]=dp[0][i]=0$ when $i \geq 0$
----
## 題目
* Uva10405
------
# LIS
最長遞增子序列 (Longest Increasing Subsequence)
----
給你一個序列長度為N，求最長遞增子序列的長度
----
## DP式
* 狀態：$dp[n][i]$ $=$ 使用 $1$到$n$ 個數字湊出長度 $i$ 的 LIS,末端數字最小為何。
* 轉移：$dp[n][i] =min(dp[n-1][i],a[n])\  if\ a[n]>dp[n-1][i-1]$ $dp[n-1][i]\ else$
* 基底：$dp[i][0] = INF, dp[0][j] = -INF$ when $i \geq 0$ and $j \geq 1$
----
* 時間複雜度為$O(n^2)$
----
## 觀察
* 令$g[i]=dp[x][i]$, where $1\leq x \leq N$
* $g[i]$為一個嚴格遞減序列
* 改的數字剛好的$a[i]$
* 被改的數字為lower\_bound(a[i])
* 二分搜
----
複雜度$O(n\log n)$
```cpp
int main(){
    int n;
    while(cin>>n){
        vector<int>v;
        for(int i=0,x;i<n;i++){
            cin>>x;
            if(!v.size()||x>v.back())v.push_back(x);
            else *lower_bound(v.begin(), v.end(),x)=x;
            dp[i]=v.size();
        }
    }
}
```
----
## 題目
* UVa11456
* UVa11790