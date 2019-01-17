# Graph
----
* 圖是由邊集合和點集合所形成的圖形
* 描述某些事物之間的某種特定關係。
* $G=(V,E)$
------
# 術語
----
## 無向邊、有向邊
* 無向邊代表邊沒有指定方向
* 有向邊則有指定方向
----
## 無向圖、有向圖、混合圖
* 無向圖是只有無向邊的圖
* 有向圖是只有有向邊的圖
* 混和圖則是包含無向邊和有向邊。
----
## 點、邊個數
用$|V|$、$|E|$來表示，在表示複雜度時，為了方便會用$V$、$E$來表示
----
## 權重(weight)
* 在點或邊上附帶一個數字
* 邊上權重較常見
* 權重通常代表代價
----
## 相鄰 (adjacent)
無向圖中,兩個點 $u$, $v$ 相鄰代表存在一個邊 $e_i = (u, v)$。
----
## 指向 (consecutive)
有向圖中, $u$ 指向 $v$ 代表存在一個邊 $e_i = (u, v)$。
----
## 度(degree)
一個點連到的邊數稱為"度"
在有向圖分成出度(d\_out)及入度(d\_in)
----
## walk
一條由$x$到$y$的路徑$x=v_1,v_2,v_3...,v_k=y$。
----
## trail
一條不重複邊的walk。
----
## 迴路(circut)
起點和終點一樣的trail。
----
## path
一條不重複點(起點和終點例外)的walk。
----
## 環(cycle)
起點和終點一樣的path。
----
## 自環 (loop)
一條邊 $e_i = (u, v)$ 滿足 $u = v$,$e_i$ 即稱為自環。
----
## 重邊 (multiple edge)
在一張圖中,存在 $e_i$, $e_j$ 滿足 $i$ != $j$ and $e_i = e_j$，則稱為重邊。
----
## 連通 (connected)
無向圖中,若 $u$ 和 $v$ 存在路徑,則 $u$ 和 $v$ 連通。若一群點兩兩連通,則這些點都連通。
------
# 儲存
----
* 相鄰矩陣(adjacency matrix)：通常會用二維陣列
* 相鄰串列(adjacency list)：vector, linklist
----
## 相鄰矩陣 v.s. 相鄰串列
* 相鄰串列幾乎稱霸所有情況
* 但邊數密且頻繁地需要找尋兩點之間的權重，用相鄰矩陣較適合
------
# 遍歷
----
* DFS
* BFS
----
## DFS
* 找到一條新的路就繼續找下去，直到沒有新的路時，原地返回
* stack 或 遞迴
----
```cpp
vector<int>G[N];
bitset<N> vis;
void dfs(int s){
    vis[s]=1;
    for(int t:G[s]){
        if(!vis[i])dfs(i);
    }
}
```
----
## BFS
* 把所有看到的路都加入清單中，並且以加入的順序來遍歷
* queue
----
```cpp
vector<int>G[N];
bitset<N> vis;
void bfs(int s){
    queue<int>q;
    q.push(i);
    vis[i]=1;
    while(q.empty()){
        int v=q.front(); q.pop();
        for(int t:G[v]){
            if(!vis[t]){
                q.push(t);
                vis[t]=1;
            }
        }
    }
}
```
----
## 題目
* zerojudge a290(給你一張有向圖，問你可不可以由A走到B)
* zerojudge a982(二維迷宮問題)
* zerojudge a634(馬步問題)
* UVa 572
------
# 樹
一種特殊的圖
----
## 特性
1. 為連通圖且$|V|=|E|+1$
1. 任意兩個點之間存在唯一路徑
1. 為連通圖，但拔掉一條邊即為不連通(分成兩張連通圖)。
1. 沒有環，但加上一條邊會形成環。
1. 若節點編號存在順序，除了第一個節點，每個節點都會伸出一條邊連到順序比自己前面的節點。
----
## 術語
----
### 根(root)
樹的一個代表性的點，通常會被當遍歷的起點，有給定根點的樹叫"有根樹"。至於無根樹依照題目需求，有時要隨機找一個點當根。
----
### 葉解點(leaf)
度數為1的節點，有根樹的根結點則會是題目需求來決定是否為葉節點。
----
### 父節點、子節點
有根樹中，兩個相連的節點，比較接近樹根的為父節點，反之為子節點。
----
### 祖先(ancestor)、子孫(descandent)
有根樹中，節點到根結點中，所有的節點皆為祖先。反過來說，該節點是他的祖先的子孫。依題目所需，有時自己也是自己的祖先(尤其是根最常這樣定義)。
----
### 距離(distance)
為兩個點所形成路徑之邊數，或是路徑上權重之和。
----
### 深度(depth)
有根樹中，節點到根結點之距離。
----
### 高度(height)
有根樹中，節點到與它距離最大的葉節點的距離稱為高度。根的高度稱為這整顆樹的高度。
----
### 子樹(subtree)
設有兩棵樹$T$,$T_1$，如果$V_1\in V$，$E_1\in E$，那麼我們說 $T_1$ 為 $T$ 的子樹
----
### N元樹
每個節點最多有N個節點，稱為N元樹。
------
# 二元樹
----
## 遍歷
* 分成前序、中序、後序
* DFS實作
----
```cpp
void dfs(int v){
    // cout<<v<<'\n'; preorder
    if(v.lc)dfs(v.lc);
    // cout<<v<<'\n'; inorder
    if(v.rc)dfs(v.rc);
    // cout<<v<<'\n'; postorder
}
```
----
## 二元搜尋樹
* 根結點的值大於左子節點的值，小於右子節點的值。
* 其左右子樹亦為二元搜尋樹。
----
* 會退化不實用
* 推廣結構
------
# 並查集
----
* 查詢所隸屬集合
* 合併兩個集合
----
* 初始
* 查詢
* 合併
----
## 初始
每個點自成一個集合，所以把樹根都設為自己
----
## 查詢
查詢的時候，要查到樹根為自己的點，為止否則的話就要繼續查
----
## 狀態壓縮
* 合併之後原本被指向的樹根就沒用了
* 一邊做查詢時，一邊做更新
----
## 啟發式合併
* 高度大的合併高度小的
* 高度變為$x$，則至少需要$2^x$個點，由此推出N個點所形成最高之高度為$\log(N)$
----
```cpp
int p[N],rank[N];
void init(){
    for(int i=0;i<N;i++){
        p[i]=i;
        rnak[i]=1;
    }
}
int Find(int x){
    if(x==p[x])return x;
    return p[x]=find(p[x]);
}
void Union(int a,int b){
    a=Find(a); b=Find(b);
    if(a==b)return;
    if(rank[a]<rank[b])p[a]=b;
    else if(rank[a]>rank[b])p[b]=a;
    else {p[a]=b; rank[a]++;}
}
```
----
* 複雜度為$O(\alpha(N))$
* Kruskal’s algorithm
----
## 題目
* zerojudge d808
* UVa 1160
* UVa 10158(陣列開兩倍)
* UVa 1329(帶權並查集)
------
# 最小生成樹
(Minimun Spanning Tree, MST)
----
## 生成樹
在一張圖中，如果有子圖剛好為也為一顆樹，我們就稱該子圖為生成樹
----
## 最小生成樹
權重最小的生成樹
----
## Kruskal’s algorithm
* 找最小權重
* 如果兩邊不為同一棵樹就合併
* 並查集
----
```cpp
struct Edge{
    int s,t,w;
    bool operaotr<(const Edge&rhs)const{
        return w<rhs.w;
    }
};
void Kruskal(){
    int cost=0;
    vector<Edge>E;
    init();
    for(auto it:E){
        it.s=Find(it.s);
        it.t=Find(it.t);
        if(it.s==it.t)continue;
        cost+=it.w;
        Union(it.s,it.t);
    }
}
```
----
* 時間複雜度$O(E(\log E+\alpha(V)))$
----
## Prim’s algorithm
* 將一棵MST連出的邊中，加入權重最小的邊(距離最近的點)
* 更新和點的距離
----
* 用priority\_queue，複雜度$O((V+E)logE)$
* 用費波那契堆(fibonacci heap)可以達到 $O(E+V\log V)$，但實作困難
* Kruskal比較好用
----
## Borůvka’s algorithm
* 延續Prim’s algorithm的思想
* 讓所有MST一起執行
* 最差情況每次兩兩成對
* 整題複雜度為$O((V+E)\log V)$)
* 期望複雜度$O((V+E))$
----
## 題目
* zerojudge a129
------
# 最短路徑
----
## 術語
----
### 負邊
權重為負的邊
----
### 負環
權重和為負的環
----
### 點源
成為起點的點，分成單源頭及多源頭。
----
### 鬆弛
單源頭最短路徑中，對於任意兩個點$u,v$，起點$s$到它們的距離$d_u,d_v$，如果$d_u > d\_v + w\_{u,v}$，$w\_{u,v}$為邊$(u,v)$的權重，我們可以讓$d\_u$更新為$d\_v+w\_{u,v}$，讓$s$到$u$的距離縮短，這個動作稱為"鬆弛"。
----
## Floyd-Warshall Algorithm
----
* 多源頭最短路徑
* 動態規劃
----
## DP式
* 狀態：$dp[k][i][j]$ 代表,若只以點 $1$到$k$ 當中繼點的話,則   
$dp[k][i][j]$ 為 $i$ 到 $j$ 的最短路徑長。
* 轉移：$dp[k][i][j] = min(dp[k-1][i][k] + dp[k-1][k][j], dp[k-1][i][j])$
* 基底：
  * $dp[0][i][j] = w[i][j]$ if $w[i][j]$ exists 
  * INF else
----
* 時/空間複雜度皆為$O(V^3)$
* 滾動陣列
* 空間複雜度可降為$O(V^2)$
----
```cpp
for (k = 0; k < n; k++)
			for (i = 0; i < n; i++)
				for (j = 0; j < n; j++)
					w[i][j] = w[j][i] = min(w[i][j], max(w[i][k], w[k][j]));
```
----
* $dp[i][j]<0$，代表存在負環
----
## 單點源最短路徑
求出一個點到所有點的最短路徑，其實就是以起點為根，最短路徑是由父節點鬆弛而來的最短路徑樹。我們找最短路徑，就是一直把鬆弛，直到所有點都不能鬆弛，所有點都獲得最短路徑了。要蓋出最短路徑樹，就只要把點指向最後一次被誰鬆弛就好了。
----
## Bellman-Ford Algorithm
* 單點源最短路徑
* 對所有邊枚舉，執行$V-1$輪，複雜度為$O(VE)$
* 如果執行第V次時還有邊可以鬆弛，代表有負環
----
```cpp
void bellman_ford(int s){
    d[s]=0;
    p[s]=s;
    for(int i=0;i<V-1;i++){
        for(int ss=0;ss<V;ss++){
            for(auto tt:v[ss]){
                if(d[ss]+w[ss][tt]<d[tt]){
                    d[tt]=d[ss]+w[ss][tt];
                    p[tt]=ss;
                }
            }
        }
    }
}
void has_negative_cycle(){
    for(int i=0;i<V;i++){
        for(int j=0;j<V;j++){
            if(d[i]+w[i][j]<d[j])return true;
        }
    }
    return false;
}
```
----
### 優化版本
* Shortest Path Faster Algorithm(SPFA)
* 枚舉起點是鬆弛過的邊，以鬆弛過的點除非被重新鬆弛
* 預期複雜度為$O(V+E)$，不過最差狀況仍為$O(VE)$
----
## Dijkstra’s Algorithm
* 把離樹根最近的點加入最短路徑樹裡
* 並把所有與該點相連的邊鬆弛
* 已經加入的點不會在被鬆弛
* 使用priority\_queue的複雜度為$O((V+E)\log E)$
* 使用費波那契堆複雜度為s$O(E+V\log V)$
----
```cpp
struct edge{
    int s,t;
    LL d;
    edge(){};
    edge(int s,int t,LL d):s(s),t(t),d(d){}
};

struct heap{
    LL d;
    int p; //point
    heap(){};
    heap(LL d,int p):d(d),p(p){}
    bool operator <(const heap& b)const{
        return d>b.d;
    }
};
int d[N],p[N];
vector<edge>edges;
vector<int>G[N];
bitset<N>vis;
void dijkstra(int ss){
    priority_queue<heap>Q;
    for(int i=0;i<V;i++)d[i]=INF;
    d[ss]=0;
    p[ss]=-1;
    vis.reset():
    Q.push(heap(0,ss));
    heap x;
    while(!Q.empty()){
        x=Q.top(); Q.pop();
        int p=x.p;
        if(vis[p])continue;
        vis[p]=1;
        for(int i=0;i<G[p].size();i++){
            edge& e=edges[G[p][i]];
            if(d[e.t]>d[p]+e.d){
                d[e.t]=d[p]+e.d;
                p[e.t]=G[p][i];
                Q.push(heap(d[e.t],e.t));
            }
        }
    }
}
```
----
而Dijkstra’s Algorithm不能處理負邊，原因是一旦點加入最短路徑樹，就不會再被更新，以維持良好複雜度，負邊會破壞此規則。
----
## 題目
* UVa 534
* UVa 10048
* UVa 929(方格上)
* UVa 11090