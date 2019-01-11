# warm up
----
## list
* 複雜度
* 函式&遞迴
* 指標
* 參考
* struct
* 常用函式庫
* extra syntax
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
* algorithm
* cmath
* iomanip
------
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
------
## cmath
----
### atan/atan2
* 斜率轉為弧度
* atan2可處理x=0的情況
----
```cpp
int main () {
  double PI=acos(-1.0);
  cout<<PI<<'\n'; // 3.14159
  cout<<atan(1)*180/PI<<'\n'; // 45
  cout<<atan(-1)*180/PI<<'\n'; // -45
  cout<<atan2(1,1)*180/PI<<'\n'; // 45
  cout<<atan2(-1,1)*180/PI<<'\n'; // -45
  return 0;
}
```
----
### log/log2/log10
* 以e,2,10為底的對數函數
----
```cpp
int main(){
	cout<<log(10)<<'\n'; // 2.30259
	cout<<log2(10)<<'\n'; // 3.32193
	cout<<log10(10)<<'\n'; // 1
	cout<<log(8)/log(2)<<'\n'; // 3
}
```
----
### pow
* 算次方
* $\geq 10^6$就會輸出科學記號
----
```cpp
int main(){
	cout<<pow(10,5)<<'\n'; // 100000
	cout<<pow(10,6)<<'\n'; // 1e+06
}
```
----
### sqrt
* 開根號
----
```cpp
int main(){
	cout<<sqrt(1)<<'\n'; // 1
	cout<<sqrt(2)<<'\n'; // 1.41421
	cout<<sqrt(3.0)<<'\n'; // 1.73205
}
```
------
## iomanip
----
### setw
* 設定輸出寬度
----

```cpp
int main () {
  cout<<setw(5)<<100<<'\n';  //"  100"
  cout<<setw(5)<<1234<<'\n'; //" 1234"
  cout<<setw(2)<<100<<'\n';  //  "100"
  return 0;
}
```
----
### setprecison
* 設定精度
----
```cpp
int main () {
  double f =3.14159;
  cout << setprecision(5) << f << '\n';// 3.1416
  cout << setprecision(9) << f << '\n';// 3.14159
  cout << fixed;
  cout << setprecision(5) << f << '\n';// 3.14159
  cout << setprecision(9) << f << '\n';// 3.141590000
  return 0;
}
```
------
# extra syntax
----
## break, continue, return
* break：跳出迴圈
* continue：這輪不做，到下一輪
* return：跳出函式，並回傳值
* 後面的else可省略
----
## const
* 不可變動
* 宣告常數
----
```cpp=
const int N=5;
int main(){
    cout<<N<<'\n'; // 5
    N++; // error
}
```
----
## static
* 只會被宣告一次
----

```cpp=
#include <iostream> 
using namespace std; 

void count(); 

int main() { 

    for(int i = 0; i < 10; i++) 
        count(); 

    return 0; 
} 

void count() { 
    static int c = 1; 
    cout << c << endl; 
    c++; 
}
/*
1
2
3
4
5
6
7
8
9
10 
 */
```
----
## define
* 巨集
* 取代
* 記得括號
----
```cpp=
#define one 1
#define ten(x) 10*x
#define sum(x,y) 2*x+y

int main(){
    cout<<1<<'\n';
    cout<<ten(5)<<'\n';
    cout<<sum(1,1)<<'\n';
    cout<<sum(1,1)*ten(2)<<'\n';
}
```
----
## typedef
* 為型態取別名
* C++11後使用using
----
```cpp=
typedef long long LL;
 using LL = long long; //C++11
```
----
## auto
* 自動判別型態
* 必須初始化
* C++14後可以應用在function
----
```cpp=
auto x;//error
auto y=1;
auto f(){return 1;}//from c++14
```
----
## range_based for
* 用範圍遍歷
----
```cpp
int sum = 0;
int arr[5] = {1,2,3,4,5};
for(int i=0;i<5;i++){
    int x = a[i];
    sum += x;
}

for(int x:arr){//can use auto x:arr
    sum += x;
}
```
----
## lambda
* 方便地定義匿名函式
----
* lambda introducer
* lambda declarator
* mutable specification
* 例外狀況規格
* 傳回值型別
* compound-statement
----
### lambda introducer
* 也叫Capture clause，宣告外部變數(在可視範圍(scope)內)傳入此函式內的方法。
----
* `[]`:只有兩個中括號，完全不抓取外部的變數。
* `[=]`：所有的變數都以傳值(call by value)的方式抓取
* `[&]`：所有的變數都以傳參考(call by reference)的方式抓取
* `[x,&y]`：x變數使用傳值，y變數使用傳參考
* `[=,&y]`：除了y變數使用傳參考以外。其餘的變數皆使用傳值的方式
* `[&,x]`：除了x變數使用傳值以外，其餘的變數皆使用傳參考的方式
----
### lambda declarator
* 也叫參數清單，傳入此函式對應資料。
----
### mutable specification
* 指定以傳值方式抓取進來的外部變數，如果用不到可省略。
* 與一般函數的傳入參數之異
	* 不可指定參數的預設值。
	* 不可使用可變長度的參數列表。
	* 參數列表不可以包含沒有命名的參數。
----
### 例外狀況規格
* 指定該函示會丟出的例外，其使用的方法跟一般函數的例外指定方式一樣，如果用不到可省略。
----
### 傳回值型別
* 指定lambda expression傳回型別，如果 lambda expression 所定義的函數很單純，只有包含一個傳回陳述式（statement）或是根本沒有傳回值的話，可省略(optional)
----
### compound-statement
* 亦稱為 Lambda 主體(lambda body)
* 跟一般的函數內容一樣
