# warm up
----
## list
* 複雜度
* 函式&遞迴
* 指標
* 參考
* struct
* 常用函式庫
* external syntax
------
# 複雜度
----
* 定性描述該演算法執行成本函式，用來
* 分析資料結構和演算法(DSA)
----
## 常用函數
----
* Big $O$(最常用)：用來表示一個複雜度的上界
* Big $\Omega$：用來表示一個複雜度的下界
* Big $\Theta$：要同時滿足Big $O$和Big $\Omega$
----
### 常見複雜度
* $O(1) < O(log\ n) < O(n) < O(n\ log\ n)$ $< O(n^2) < O(n^3) < O(2^n) < O(n!)$
* $O(\alpha(n))$(並查集)
----
## 時間/空間複雜度
* 時間複雜度：運算
* 空間複雜度：變數記憶體總和
----
### 區域空間不足
* static
* 全域
------
# 遞迴
----
## 語法
```cpp=
return_type function_name(paremeter list){
    Do something...
    return data;// void need not return;
}
```
----
## 自呼叫
* 終止條件以免無限遞迴
* 避免遞迴過深
----
```cpp=
int ans;
void f(int i){
    if(i==1){
        ans=1;
        return;
    }
    f(i-1);
    ans*=i;
    return;
}
```
----
## 用處
* 模組化
* 遞迴
----
## 常見遞迴使用
* 分治
* dp中的top-down
* 圖/樹的搜索
------
# 指標&參考
----
## 指標
* 記憶體操作
* 動態記憶體配置
----
```cpp=
int *p=new int;
(*p)=1;
delete p;
```
----
```cpp=
int a=5;
int *p=&a;
(*p)++;
cout<<a<<'\n'; // 6
```
----
## 參考
* 別名
* 類似指標
----
## 參考
* 取代太長的變數
* 取代指標傳可修改的值
------
# 傳值
----
* call by value
* call by address/value of pointer
* call by reference
----
## call by value
* 複製參數
* 不改原值
----
```cpp=
void swap(int x,int y){
    cout<<x<<' '<<y<<'\n';// 1 2
    int t=x;
    x=y;
    y=t;
    cout<<x<<' '<<y<<'\n';// 2 1
} 
int main(){
    int a=1,b=2;
    cout<<a<<' '<<b<<'\n';// 1 2
    swap(a,b);
    cout<<a<<' '<<b<<'\n';// 1 2
}
```
----
## call by address/value of pointer
* 對記憶體操作
* 會改原值
----
```cpp=
void swap(int *x,int *y){
    cout<<*x<<' '<<*y<<'\n';// 1 2
    int t=*x;
    *x=*y;
    *y=t;
    cout<<*x<<' '<<*y<<'\n';// 2 1
} 
int main(){
    int a=1,b=2;
    cout<<a<<' '<<b<<'\n';// 1 2
    swap(&a,&b);
    cout<<a<<' '<<b<<'\n';// 2 1
}
```
----
## call by reference
* 分身
* 會改原值
----
```cpp=
void swap(int &x,int &y){
    cout<<x<<' '<<y<<'\n';// 1 2
    int t=x;
    x=y;
    y=t;
    cout<<x<<' '<<y<<'\n';// 2 1
} 
int main(){
    int a=1,b=2;
    cout<<a<<' '<<b<<'\n';// 1 2
    swap(a,b);
    cout<<a<<' '<<b<<'\n';// 2 1
}
```
------
## struct
----
* 把資料包在一起
----
```cpp=
struct struct_name{
    type1 name1;
    type2 name2;
    ...
}; //<-notice
```
----
```cpp=
struct Plane{
    int x,y;
    Plane(){};
    Plane(int _x,int _y):x(_x),y(_y){}
    Plane add(const Plane &rhs)const{
        return Plane(x+rhs.x,y+rhs.y);
    }
    bool operator<(const Plane &rhs)const{
        if(x!=rhs.x)return x<rhs.x;
        return y<rhs.y;
    }
    ~Plane(){};
}
int main(){
    Plane p1;
    Plane p2(1,2);
    Plane p3=Plane();
    Plane p4=Plane(0,0);
}
```
----
## 建構子(constructor)
* 和 struct_name 同名
* 初始化
----
## 解構子(destructor)
* ~strcut_name
* 離開作用域時運作
----
## 重載運算子
* 依需要實作
------
# 常見函式庫
----
## algorithm
----
### sort
* 排序
----
```cpp
sort(a,a+6);
```
----
### min/max
* 最大最小值
----
```cpp
cout<<min(5,2)<<'\n';// 2
cout<<max(5,2)<<'\n';// 5
```
----
### lower_bound/upper_bound
* 找範圍
----
```cpp=
lower_bound(a, a+n, k); //最左邊 ≥ k 的位置
upper_bound(a, a+n, k); //最左邊 > k 的位置
upper_bound(a, a+n, k) - 1; //最右邊 ≤ k 的位置
lower_bound(a, a+n, k) - 1; //最右邊 < k 的位置
[lower_bound, upper_bound) //等於 k 的範圍
equal_range(a, a+n, k);
```
----
### next_permutation/prev_permutation
* 依字典序向前/後
----
```cpp
// next_permutation example
#include <iostream>     // std::cout
#include <algorithm>    // std::next_permutation, std::sort

int main () {
  int myints[] = {1,2,3};

  std::sort (myints,myints+3);

  std::cout << "The 3! possible permutations with 3 elements:\n";
  do {
    std::cout << myints[0] << ' ' << myints[1] << ' ' << myints[2] << '\n';
  } while ( std::next_permutation(myints,myints+3) );

  std::cout << "After loop: " << myints[0] << ' ' << myints[1] << ' ' << myints[2] << '\n';

  return 0;
}
```
----
## cmath
----
### atan/atan2
* 斜率轉為弧度
* atan2可處理x=0的情況
----
## iomanip

