# STL
----
* STL初步介紹
* 各種資料結構
------
# 什麼是STL?
* C++內建的資料結構
----
## 型態模板
* 指定資料型態
* 視請況可不填滿
----
## 迭代器
* 提供遍歷
----
依據迭代器的強到弱可分為三種：
* 隨機存取(Random Access)：可與整數做+-法、遞增及遞減
* 雙向（Bidirectional）迭代器：遞增及遞減
* 單向（Forward）迭代器：只能遞增
----
根據用法可分為兩種：
* 輸入（Input）迭代器：讀取迭代器指向的內容，，所有的迭代器都可以當作輸入迭代器。
* 輸出（Output）迭代器：更改迭代器指向的內容時，除了常數（const）迭代器（也就是規定不能更動迭代器指向的內容）以外，所有的迭代器都可以當作輸出迭代器。
----
|  | 正向 | 逆向 |
| --- | --- | --- |
| 可改值    | C.begin() C.end() | C.rbegin() C.rend() |
| 不可改值     | C.cbegin() C.cend() | C.crbegin() C.crend() |
------
# 資料結構現身
------
# Part1
* Stack
* Queue
* Deque
----
## stack
* 有兩個端口，其中一個封閉，另一個端口負責插入、刪除
----
### 實作
```cpp
struct stack{
    int st[N],top;
    Stack():top(0){}
    int size(){
        return top;
    }
    void push(int x){
        st[top++]=x;
    }
    int top(){
        assert(top>0)
        return st[top];
    }
    void pop(){
        if(top)--top;
    }
}
```
----
### STL
```cpp
#include <iostream>
#include <stack>
using namespace std;
  
int main(){
    stack<int>st;
    st.push(1);
    cout<<st.top()<<'\n';// 1
    st.push(2);
    cout<<st.top()<<'\n';// 2
    st.push(3);
    cout<<st.top()<<'\n';// 3
    st.pop();
    cout<<st.top()<<'\n';// 2
}
```
----
## queue
* 有兩個端口，一個負責插入，另一個端口負責刪除的資料結構
----
### 實作
```cpp
struct Queue{
    int q[N],head,tail;
    Queue():head(0),tail(0){}
    int size(){
        return tail-head;
    }
    void push(int x){
        q[tail++]=x;
    }
    int front(){
        return q[head];
    }
    void pop(){
        head++;
    }
}
```
----
### STL
```cpp
#include <iostream>
#include <queue>
using namespace std;

int main(){
    queue<int>st;
    st.push(1);
    cout<<st.front()<<'\n';// 1
    st.push(2);
    cout<<st.front()<<'\n';// 1
    st.push(3);
    cout<<st.front()<<'\n';// 1
    st.pop();
    cout<<st.front()<<'\n';// 2
}
```
------
# Part2
* list
----
## 連結串列
* 插入元素只要$O(1)$
* 無法隨機存取
----
## 實作(單向)
```cpp
struct Node{
    int v;
    Node *next=nullptr;
}
```
----
## 實作(雙向)
```cpp
struct Node{
    int v;
    Node *next=nullptr,*prev=nullptr;
}
```
----
## STL
```cpp
// adapt from cppreference
#include <iostream>
#include <list>
 
int main(){
    std::list<char> letters {'o', 'm', 'g', 'w', 't', 'f'};
 
    if (!letters.empty()) {
        cout << letters.front() << '\n';// o
        cout << letters.back() << '\n'; // f
    }  
}
```
------
# Part3
* Vector
* String
* Bitset
----
## vector
* 可改變長度的陣列
----
## STL
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main(){
    vector<int>v;
    v.push_back(1);
    v.push_back(2);
    v.push_back(3);
    for(int i=0;i<v.size();i++){
        cout<<v[i]<<' ';
    }
    cout<<'\n';
    v.clear();

    v.resize(2);
    cout<<v.size()<<'\n';

    for(int i=0;i<v.size();i++){
    v[i]=5-i;
    }
    for(int i=0;i<v.size();i++){
    cout<<v[i]<<' ';
    }
    cout<<'\n';
}
/*
1 2 3
2
5 4
*/
```
----
### 兩特化
* vector<char>：string
* vector<bool>：bitset
----
## String
* 可變動長度的字元陣列
----
```cpp
// from cppreference
#include <iostream>
#include <string>
#include <sstream>// for getline
 
int main()
{
    // greet the user
    std::string name;
    std::cout << "What is your name? ";
    std::getline(std::cin, name);
    std::cout << "Hello " << name << ", nice to meet you.\n";
 
    // read file line by line
    std::istringstream input;
    input.str("1\n2\n3\n4\n5\n6\n7\n");
    int sum = 0;
    for (std::string line; std::getline(input, line); ) {
        sum += std::stoi(line);
    }
    std::cout << "\nThe sum is: " << sum << "\n";
}
/*
What is your name? John Q. Public
Hello John Q. Public, nice to meet you.
 
The sum is 28
*/
```
----
## bitset
* 節省的bool陣列
* 可當二進位位元運算
------
# Part4
* priorty_queue
----
## priorty_queue
* 維護最大/小值，可插入、刪除、及詢問最大/小值
----
### 一種實作：binary heap
```cpp
int heap[N],top=0;
void push(int v){
    heap[++top]=v;
    for(int i=top;i>1;){
        if(heap[i]<=heap[i/2])break;
        swap(heap[i],heap[i/2]);
        i<<=1;
    }
}
void pop(){
    heap[1]=heap[top--];
    for(int i=1;(i<<1)<=top;){
        if(heap[i]<heap[i<<1]){
            swap(heap[i],heap[i<<1]);
            i<<=1;
        }else if((i<<1)<top&&heap[i]<heap[(i<<1)+1]){
            swap(heap[i],heap[(i<<1)+1]);
            i=(i<<1)+1;
        }else{
            break;
        }
    }
}
```
----
### STL
```cpp
#include <iostream>
#include <queue>
using namespace std;

int main(){
    priority_queue<int>Q;
    Q.push(2);
    cout<<Q.top()<<'\n';// 2
    Q.push(5);
    cout<<Q.top()<<'\n';// 5
    Q.pop();
    cout<<Q.top()<<'\n';// 2
    Q.push(3);
    cout<<Q.top()<<'\n';// 3
}
```
------
# Part5
* Pair
* Tuple
* Set
* Map
----
## Pair&Tuple
* 多個資料型態組織合盟
* pair只能2個
* tuple可自由決定個數
----
## 自查找平衡二元樹
* 插入
* 刪除
* 尋找值
* 尋找lower_bound、upeer_bound
----
## Set&Map
* Set回傳鍵值(key value)
* map回傳對應值(mapped value)
----
## Set
```cpp
#include <iostream>
#include <set>
using namespace std;

int main(){
	set<int>sb;
	sb.insert(1);
	sb.insert(2);
	sb.insert(3);

	cout<<"1 : "<<(sb.find(1)!=sb.end()?"find\n":"not find\n");
	cout<<"1 : "<<(sb.count(1)?"find\n":"not find\n");
	
	sb.erase(1);
	cout<<"1 : "<<(sb.find(1)!=sb.end()?"find\n":"not find\n");
	cout<<"1 : "<<(sb.count(1)?"find\n":"not find\n");
}
/*
1 : find
1 : find
1 : not find
1 : not find
*/
```
----
### Map
```cpp
#include <iostream>
#include <map>
using namespace std;

int main(){
    map<string,int>tb;
    tb["123"]=1;
    tb["owowowo"]=2;
    tb["omomo"]=3;
    cout<<"tb[\"123\"]: "<<tb["123"]<<'\n';
    cout<<"tb[\"owowowo\"]: "<<tb["owowowo"]<<'\n';
    cout<<"tb[\"omomo\"]: "<<tb["omomo"]<<'\n';
    
    cout<<"123 : "<<(tb.find("123")!=tb.end()?"find\n":"not find\n");
    cout<<"123 : "<<(tb.count("123")?"find\n":"not find\n");
    
    tb.clear();
    cout<<"123 : "<<(tb.find("123")!=tb.end()?"find\n":"not find\n");
    cout<<"123 : "<<(tb.count("123")?"find\n":"not find\n");

    cout<<"owo : "<<(tb.find("owo")!=tb.end()?"find\n":"not find\n");
    tb.insert(make_pair("owo",659));
    cout<<"owo : "<<(tb.find("owo")!=tb.end()?"find\n":"not find\n");
}
/*
tb["123"]: 1
tb["owowowo"]: 2
tb["omomo"]: 3
123 : find
123 : find
123 : not find
123 : not find
owo : not find
owo : find
*/
```
----
#### multi-系列
* 可插入重複元素
* map無法用下標運算子
----
#### unorder 系列
* 降低常數
* 不會排序
* 沒有lower\_bound/upper\_bound
* 也不會依鍵值大小遍歷
* 迭代器為單向
