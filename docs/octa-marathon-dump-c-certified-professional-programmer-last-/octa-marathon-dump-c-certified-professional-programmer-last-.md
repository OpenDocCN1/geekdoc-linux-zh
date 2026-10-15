
# Octa Marathon 题库：C++ 认证专业程序员：最后冲刺指南

![](img/c29ca0d812816c404441ad99c4f4d88a_0_0.png)

考试代码：`C++ Institute CPP`

主题 1，卷 A

## 第 1 题

当你尝试编译并运行以下代码时，会发生什么？

```
#include <iostream>
#include <set>
#include <vector>
using namespace std;
int main(){
int t[] = { 3, 4, 2, 1, 6, 5, 7, 9, 8, 0 };
vector<int> v(t, t+10);
multiset<int> s1(v.begin(),v.end());
s1.insert(v.begin(),v.end());
pair<multiset<int>::iterator,multiset<int>::iterator> range;
range = s1.equal_range(6);
while (range.first != range.second) {
cout<<range.first<<" "; range.first++;
}
return 0;
}
```

- A. 程序输出：6 6
- B. 程序输出：5 7
- C. 程序输出：5 5 6 6 7
- D. 程序输出：5 5 7 7 7
- E. 程序输出：1 1 6 5 5

答案：A

解析：

## 第 2 题

当你尝试编译并运行以下代码时，会发生什么？

```
#include <vector>
#include <iostream>
#include <algorithm>

using namespace std;
template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o){}
void operator())(const T & val ) {

out<<val<< " ";
}
};
struct Sequence {
int start;
Sequence(int start):start(start){}
int operator++() {

return start++;
}
int main() {
vector<int> v1(10);
sort(v1.rbegin(),v1.rend(), Sequence(1));
rotate(v1.begin(),v1.begin() + 1, v1.end() );
for_each(v1.begin(), v1.end(), Out<int>(cout));cout<<endl;
return 0;
}
```

程序输出：

- A. 1 2 3 4 5 6 7 8 9 10
- B. 10 9 8 7 6 5 4 3 2 1
- C. 9 8 7 6 5 4 3 2 1 10
- D. 1 10 9 8 7 6 5 4 3 2

答案：C

解析：

## 第 3 题

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <fstream>
#include <string>
#include <list>
#include <algorithm>
#include <iomanip>
using namespace std;
class B { int val;
public:
B(int v=0):val(v){}
int getV() const { return val; }
operator int() const { return val; };};
```

```cpp
template<class T>struct Out {

ostream & out;
Out(ostream & o): out(o){}
void operator() (const T & val ) {out<<setw(3)<<hex<<val; } };
```

```cpp
int main () {
 int t[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
 ostream f("test.out", ios::trunc|ios::out);
list<B> l(t, t+10);
for_each(l.begin(), l.end(), Out<B>(f));
f.close();
f.open("test.out");
for(; ; f.good(); ) { {
 B i;
f>>i;
cout<<i<<" ";
}
f.close();
return 0;
}
```

- A. 文件 `test.out` 将以写入模式打开
- B. 文件 `test.out` 将截断
- C. 文件 `test.out` 将以读取模式打开
- D. 编译错误
- E. 程序将显示序列 1 2 3 4 5 6 7 8 9 10

答案：D

解析：

## 第 4 题

当你尝试编译并运行以下代码时，假设你输入序列：one two？会发生什么？

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;
int main ()
{
string a;
cin>>a;
cout<<a<<endl;
return 0;
}
```

程序输出：

- A. one
- B. one two
- C. 运行时异常
- D. 编译错误
- E. 结果未

答案：A

解析：

## 第 5 题

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <map>
#include <vector>
#include <sstream>
#include <string>
using namespace std;
int main() {
int t[] = { 3
```

输出将：

- A. 2 2
- B. 1 2
- C. 1 3
- D. 2
- E. 0

答案：A

解析：

## 第 6 题

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
class B { int val;
public:
B(int v):val(v){
int getV() const {return val; } operator <(const B & v) const { return val<v.val; }
ostream & operator<<(ostream & out, const B & v) { out<<v.getV(); return out; }
template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o)
void operator() (const T & val) {out<<val<<" };
int main() {
B t1[]={3,2,4,1,5};
B t2[]={5,6,8,2,1};
vector<B> v1(10);
sort(t1, t1+5);
sort(t2, t2+5);
set_intersection(t1,t1+5,t2,t2+5,v1.begin());
for_each(v1.begin(), v1.end(), Out<B>(cout));cout<<endl;
return 0;
}
```

程序输出：

- A. 编译错误
- B. 1 2 3 4 5 6 8 0 0
- C. 1 2 3 4 5 6 8 2 1
- D. 5 2 1 0 0 0
- E. 1 2 5 0 0 0

答案：D

解析：

## 第 7 题

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <list>
#include <vector>
#include <iostream>
using namespace std;
int main ()
{
int t[] = {1, 2, 3, 4, 5};
vector<int>v1(t, t+5);
list<int>l1;
l1.assign(v1.end(), v1.begin());
for(int i=0; i<l1.size(); i++)
{
cout<<l1.at(i)<< ";
}
cout<<endl;
return 0;
}
```

- A. 程序显示 5 4 3 2 1
- B. 程序显示 1 2 3 4 5
- C. 编译错误
- D. 段错误异常

答案：C

解析：

## 第 8 题

当你尝试编译并运行以下代码时会发生什么？



```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
class B { int val;
public:
int (int v):val(v)
int getV() const {return val; } operator <(const B & v) const { return val<v.val; }
ostream & operator<<(ostream & out, const B & v) { out<<v.getV(); return out; }
template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o)
void operator()(const T & val) {out<<val<<" };
int main() {
B t1[]={3,2,4,1,5};
B t2[]={6,10,8,7,9};
vector<B> v1(10);
sort(t1, t1+5);
sort(t2, t2+5);
merge(t1,t1+5,t2,t2+5,v1.begin());
for_each(v1.begin(), v1.end(), Out<B>(cout));cout<<endl;
return 0;
}
```

程序输出：

- A. 1 2 3 4 5 6 10 8 7 9
- B. 3 2 4 1 5 6 7 8 9 10
- C. 3 2 4 1 5 6 10 8 7 9
- D. 1 2 3 4 5 6 7 8 9 10
- E. 编译错误

答案：E

解析：

## 第 9 题

关于以下代码，哪句话是正确的？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
class A {
int a;
public:
A(int a) : a(a) {}
int getA() const { return a; }

void setA(int a) { this->a = a; }
/* 在此处插入代码 */
};
```

```cpp
struct add10 { void operator()(A & a) { a.setA(a.getA() + 10); } };

int main() {
 t[] = { 10, 5, 9, 6, 2, 4, 7, 8, 3, 1 };
vector<A> v1(t, t + 10);
for_each(v1.begin(), v1.end(), add10());
vector<A>::iterator it == find(v1.begin(), v1.end(), A(7));
cout << it->getA() << endl;
return 0;
}
```

- A. 可以编译并打印 7
- B. 编译
- C. 可以编译但程序结果不可预测
- D. 添加代码：

bool operator!=(const A & b) const {

if (this->a != b.a) { return true; } return false; }

在位置 1 处允许程序编译

答案：B

解析：

## 第 10 题

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

void myfunction(int i) {
  cout << " " << i;
}
void multiply (int a) {
  a*2;
}

int main() {
  int t[] = { 10, 5, 9, 6, 2, 4, 7, 8, 3, 1 };
  vector<int> v1(t, t+10);
  for_each(v1.begin(), v1.end(), multiply);
  iter_swap(v1.begin(),v1.end(),t+9);
  for_each(v1.begin(), v1.end(), function);
  return 0;
}
```

程序输出：

- A. 1 5 9 6 2 4 7 8 3 1
- B. 编译错误
C. 1 2 3 4 5 6 7 8 9 10
D. 10 9 8 7 6 5 4 3 2 1
E. 10 5 9 6 2 4 7 8 3 1

答案：A

解析：

## 题编号：11

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o){}
void operator()(const T & val) { out<<val<<" "; }
};

int main() {
int t[]={3,2,4,1,5,10,9,7,8,6};
vector<int> v1(t,t+10);
out<<*max_element(v1.begin(), v1.end());
return 0;
}
```

程序输出：

- A. 3
- B. 1
- C. 6
- D. 10
- E. 编译错误

答案：D

解析：

## 题编号：12

当你尝试编译并运行以下代码时，会发生什么：

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
template<class T>struct Out {
ostream &out;
Out(ostream & o) : out(o) {}
void operator() (const T & val ) { out<<val<<" "; } };

int main() {
int t1[]={3,2,4,1,5};
int t2[]={5,6,8,2,1};
vector<int> v1(10);
sort(t1, t1+5);
sort(t2, t2+5);
set_intersection(v1,t1+5,t2,t2+5,v1.begin());
for_each(v1.begin(), v1.end(), Out<int>(cout));cout<<endl;
return 0;
}
```

程序输出：

- A. 编译错误
- B. 1 2 3 4 5 6 8 0 0 0
- C. 1 2 3 4 5 6 8 2 1 0
- D. 1 1 2 3 4 5 5 6 8
- E. 1 2 5 0 0 0 0 0 0 0

答案：E

解析：

## 题编号：13

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <deque>
#include <set>
using namespace std;

void myfunction(int i) {
cout << " " << i;
}

int main() {
int t[] = { 10, 5, 9, 6, 2, 4, 7, 8, 3, 1 };
vector<int> v1(t, t + 10);
deque<int> d1(t, t + 10);
set<int> s1(t, t + 10);

for_each(v1.begin(), v1.end(), myfunction); // 行 I
for_each(d1.begin(), d1.end(), myfunction); // 行 II
for_each(s1.begin(), s1.end(), myfunction); // 行 III

return 0;
}
```

A. 程序输出：10596247831110596247831112345678910
B. 程序输出：10596247831110596247831110596247831
C. 程序输出：123456789101234567891012345678910
D. 行 I 编译错误
E. 行 III 编译错误

答案：A

解析：

## 题编号：14

当你尝试编译并运行以下代码时，会发生什么？



```cpp
#include <iostream>
#include <algorithm>
#include <map>

using namespace std;

int main() {
int t[] = { 10, 5, 9, 6, 2, 4, 7, 8, 3, 1 };
map<int,int> m;
for(int i=0; i < 10; i++) {
m[i]=t[i];
}
pair<const int,int> p(5,5);

map<int, int>::iterator it = find(m.begin(), m.end(), p);
if (it != m.end())
{
    cout<<it->first<<endl;
}
else
{
    cout<<"Not found!";
    return 0;
}
```
程序输出：

- A. 5
- B. Not found!
- C. 10
- D. 编译错误

答案：B

解析：

## 题编号：15

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <set>
using namespace std;

void myfunction(int i) {
  cout << " " << i;
}

int main() {
  int t[] = { 10, 5, 9, 6, 2, 4, 7, 8, 3, 1 };
  set<int> s1(t, t+10);
  vector<int> v1(s1.begin(), s1.rend());
  swap_ranges(v1.begin(), v1.end(), s1.begin());
  for_each(v1.begin(), v1.end(), myfunction);
  for_each(s1.begin(), s1.end(), myfunction);
  return 0;
}
```

程序输出：

- A. 10 9 8 7 6 5 4 3 2 1 3 4 5 6 7 8 9 10
- B. 编译错误
- C. 1 2 3 4 5 6 7 8 9 10 1 2 3 4 5 6 7 8 9 10
- D. 1 2 3 4 5 6 7 8 9 10 10 9 8 7 6 5 4 3 2
- E. 10 9 8 7 6 5 4 3 2 10 9 8 7 6 5 4 3 2

答案：B

解析：

## 题编号：16

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <set>
#include <list>
using namespace std;
int main(){
int t[] = {1, 1, 2, 2, 3, 3, 4, 4, 5, 5 };

list<int> v(t, t+10);
set<int> s1(v.begin(),v.end());
if (s1.count(3) == 2) {
s1.erase(3);
}
for(set<int>::iterator i=s1.begin();i!=s1.end(); i++) {
cout<<i;
}
return 0;
}
```

- A. 程序输出：1 2 4 5
- B. 程序输出：1 2 4 5
- C. 程序输出：1 2 3 4 5
- D. 程序输出：1 1 2 3 4 5
- E. 编译错误

答案：A

解析：

## 题编号：17

当你尝试编译并运行以下代码时，会发生什么：

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <functional>
using namespace std;
template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o){}
void operator()(const T & val ) { out<<val<<" "; }
};

int Add(int a, int b) {
return a+b;
}

int main() {
int t[]={1,2,3,4,5,6,7,8,9,10};
vector<int> v1(t, t+10);
vector<int> v2(10);
transform(v1.begin(), v1.end(), v2.begin(), bind2nd(ptr_fun(Add),1));
vector<int>::iterator it = find_if(v2.begin(), v2.end(),bind2nd(equal_to<int>(),10));
cout<<*it<<endl;
return 0;
}
```

程序输出：

- A. false
- B. true
- C. 10
- D. 0
- E. 编译错误

答案：C

解析：

## 题编号：18

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <deque>
using namespace std;

void myfunction(int i) {
cout << " " << i;
}

int main() {
int t[] = { 10, 5, 9, 6, 2, 4, 7, 8, 3, 1 };
deque<int> d1(t, t+10);
vector<int> v1(d1.begin(), d1.rend());
sort(d1.begin(), d1.end());
swap_ranges(v1.begin(), v1.end(), d1.begin());
for_each(v1.begin(), v1.end(), myfunction);
for_each(d1.begin(), d1.end(), myfunction);
return 0;
}
```

程序输出：

- A. 10 9 8 7 6 5 4 3 2 1 1 2 3 4 5 6 7 8 9 10
- B. 编译错误
- C. 1 2 3 4 5 6 7 8 9 10 1 2 3 4 5 6 7 8 9 10
- D. 1 2 3 4 5 6 7 8 9 10 10 9 8 7 6 5 4 3 2
- E. 10 9 8 7 6 5 4 3 2 1 10 9 8 7 6 5 4 3 2

答案：D

解析：

## 题编号：19

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
template<class T>struct Out {
ostream & out;
Out(ostream & o) : out(o) {}
void operator()(const T & val ) { out<<val<<" "; }
};

int main() {
int t1[]={3,2,4,1,5};
int t2[]={5,6,8,2,1};
vector<int> v1(10);
sort(t1, t1+5);
sort(t2, t2+5);
set_intersection(v1,t1+5,t2,t2+5,v1.begin());
for_each(v1.begin(), v1.end(), Out<int>(cout));cout<<endl;
return 0;
}
```

程序输出：

- A. 编译错误
- B. 1 2 3 4 5 6 8 0 0 0
- C. 1 2 3 4 5 6 8 2 1 0
- D. 1 1 2 3 4 5 5 6 8
- E. 1 2 5 0 0 0 0 0 0 0

答案：A

解析：

## 题编号：20

当你尝试编译并运行以下代码时，会发生什么？



```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <deque>
#include <set>
using namespace std;

void myfunction(int i) {
cout << " " << i;
}

int main() {
int t[] = { 10, 5, 9, 6, 2, 4, 7, 8, 3, 1 };
vector<int> v1(t, t + 10);
deque<int> d1(t, t + 10);
set<int> s1(t, t + 10);

for_each(v1.begin(), v1.end(), myfunction); // 行 I
for_each(d1.begin(), d1.end(), myfunction); // 行 II
for_each(s1.begin(), s1.end(), myfunction); // 行 III

return 0;
}
```

A. 程序输出：10596247831110596247831112345678910

B. 程序输出：10596247831110596247831110596247831

C. 程序输出：123456789101234567891012345678910

D. 行 I 编译错误

E. 行 III 编译错误

答案：A

解析：

## 题编号：21

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <map>

using namespace std;

int main() {
int t[] = { 10, 5, 9, 6, 2, 4, 7, 8, 3, 1 };
map<int,int> m;
for(int i=0; i < 10; i++) {
m[i]=t[i];
}
pair<const int,int> p(5,5);

map<int, int>::iterator it = find(m.begin(), m.end(), p);
if (it != m.end())
{
    cout<<it->first<<endl;
}
else
{
    cout<<"Not found!";
    return 0;
}
}
```

程序输出：

- A. 5
- B. Not found!
- C. 10
- D. 编译错误

答案：B

解析：

## 题编号：22

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <set>
#include <vector>
using namespace std;

template<class T> void print(T start, T end) {
while (start != end) {
std::cout << *start << " "; start++;
}
}
```

```cpp
int main(){

vector<int>v;
multiset<int> s;
for(int i=10; i>0; i--) {
  v.push_back(i); s.push_back(i);
}
print(v.begin(), v.end()); print(s.begin(), s.end());cout<<endl;
return 0;
}
```

- A. 程序输出：10 9 8 7 6 5 4 3 2 1 1 2 3 4 5 6 7 8 9 10
- B. 程序输出：10 9 8 7 6 5 4 3 2 1 10 9 8 7 6 5 4 3 2 1
- C. 程序输出：10 9 8 7 6 5 4 3 2 1 以及范围在 1-10 的不可预测数字序列
- D. 编译错误

答案：D

解释：

# 题目编号：23

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <map>
using namespace std;

int main() {
int t[] = { 1, 1, 2, 2, 3, 4, 5, 5 };
string s[] = { "one", "one", "two", "two", "three", "three", "four", "four", "five", "five" };
map<int, string> m;
for (int i = 0; i < 10; i++) {
  m.push_back(pair<int, string>(t[i], s[i]));
}

for (map<int, string>::iterator i = m.begin(); i != m.end(); i++) {
  cout << i->first << " " << i->second << " ";
}
return 0;
}
```

- A. 程序输出：1 2 3 4 5
- B. 编译错误
- C. 程序输出：1 1 2 2 3 3 4 4 5 5
- D. 程序输出：one two three four five
- E. 程序输出：one one two three three four four five five

答案：B

解释：

# 题目编号：24

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <deque>
#include <iostream>
#include <algorithm>
using namespace std;
class B { int val;
public:
B(int v):val(v) {}
int getV() const { return val; } bool operator < (const B & v) const { return val<v.val; }
ostream & operator<<(ostream & out, const B & v) { out<<v.getV(); return out; }
};
template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o) {}
void operator()(const T & val) { out<<val<< " "; };
};
int main() {
int t[]={8, 10, 5, 1, 4, 6, 2, 7, 9, 3};
deque<B> d1(t, t+10);
sort(d1.begin(), d1.end());
deque<B>::iterator it = upper_bound(d1.begin(), d1.end(), B(4), greater<B>);
for_each(it, d1.end(), Out<B>(cout)); cout<<endl;
return 0;
}
```

程序输出：

- A. 5 6 7 8 9 10
- B. 4 5 6 7 8 9 10
- C. 编译错误
- D. 1 2 3 4 5
- E. 1 2 3 4

答案：C

解释：

# 题目编号：25

哪些栈的初始化（行号）是正确的？选择所有适用项。

```cpp
#include <iostream>
#include <deque>
#include <list>
#include <stack>
#include <vector>

using namespace std;

int main()
{
deque<int> mydeck;
list<int> mylist;
vector<int> myvector;
stack<int> first;// Line I
stack<int> second(mydeck);//// Line II
stack<int> third(second);//// Line III
stack<int, list<int> > fourth(mylist);//// Line IV
stack<int, vector<int> > fifth(myvector);//// Line V
return 0;
}
```

- A. 行 I
- B. 行 II
- C. 行 III
- D. 行 IV
- E. 行 V

答案：A,B,C,D,E

解释：

# 题目编号：26

当你尝试编译并运行以下代码时会发生什么？



```cpp
#include <deque>
#include <iostream>
#include <algorithm>

using namespace std;

class B { int val;
public:
B(int v):val(v){}
int getV() const { return val; } bool operator < (const B & v) const { return val<v.val; }
ostream & operator <<(ostream & out, const B & v) { out<<v.getV(); return out; }
template<class T> struct Out {
ostream & out;
Out(ostream& o): out(o){}
void operator() (const T & val) { out<<val<< " ";
};
int main(){
int t[]={8, 10, 5, 1, 4, 6, 2, 7, 9, 3};
deque<B> d1(t, t+10);
sort(d1.begin(), d1.end());
deque<B>::iterator it = upper_bound(d1.begin(), d1.end(), B(4));
for_each(it, d1.end(), Out<B>(cout));
return 

}


```

输出：

- A. 5 6 7 8 9 10
- B. 4 5 6 7 8 9 10
- C. 6 7 8 9 10
- D. 1 2 3 4 5
- E. 1 2 3 4

答案：A

解释：

# 题目编号：27

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
class B { int val;
public:
B(int v):val(v){}
int getV() const { return val; } bool operator < (const B & v) const { return val<v.val; }
ostream & operator<<(ostream & out, const B & v) { out<<v.getV(); return out; }
};
template<class T>struct Out {
ostream & out;
Out(ostream & o) : out(o){}
void operator() (const T & val) { out<<val<< " "; };
};
int main() {
B t1[]={3,2,4,1,5};
B t2[]={5,6,8,2};
vector<B> v1(10,0);
sort(t1,t1+5);
sort(t2,t2+5);
set_symmetric_difference(t2,t2+5,t1,t1+5,v1.begin());
for_each(v1.begin(), v1.end(), Out<B>(cout));cout<<endl;
return 0;
}
```

程序输出：

- A. 6834000
- B. 340000
- C. 6800000
- D. 编译错误
- E. 3468000

答案：E

解释：

# 题目编号：28

当你尝试编译并运行以下代码时：

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <functional>
using namespace std;

template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o){}
void operator() (const T & val ) { out<<val<<" "; }
};
int main() {
int t[]={3,2,4,1,5,6,10,7,9};
vector<int> v1(t, t+10);
for_each(v1.begin(), v1.end(), bind(plus<int>()));
for_each(v1.rbegin(), v1.rend(), Out<int>(cout));cout<<endl;
return 0;
}
```

程序输出：

- A. 3 2 4 1 5 6 10 7 9
- B. 4 3 5 2 6 7 11 9 8 10
- C. 9 7 8 10 6 5 4 3
- D. 10 8 9 11 7 6 5 4
- E. 编译错误

答案：C

解释：

using namespace std;

```
void myfunction(int i) {
cout << " " << i;
}

bool classifier(int v) {
return v%2==0;
}

int main() {
 int t[] = { 1, 5, 2, 5, 2, 4, 4, 3, 3, 1 };
vector<int> v1(t, t+10);
set<int> s1(t, t+10);
replace(v1.begin(), v1.end(), classifier, 10);
for_each(v1.begin(), v1.end(), myfunction);
return 0;

}
```

程序输出：

- A. 1 5 10 5 10 10 10 3 3 1
- B. 1 5 2 5 2 4 4 3 3 1
- C. 编译错误
- D. 10 10 2 10 2 4 4 10 10 10

答案：C

解释：

# 题目编号：35

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <deque>
#include <list>
#include <iostream>
using namespace std;
int main ()
{
list<int>l1;
deque<int>d1;
for(int i=0; i<5; i++)
{
l1.push_back(i);l1.push_front(i);
d1.push_back(i);d1.push_front(i);
}
for(int i=0; i<d1.size(); i++)
{
cout<<d1[i]<<" "<<l1[i]<<" << "";n
}

cout<<endl;
return 0;
}
```

- A. 程序显示 4 4 3 3 2 2 1 0 0 0 1 2 2 3 4 4
- B. 运行时异常
- C. 第 11 行导致编译错误
- D. 第 12 行导致编译错误
- E. 第 16 行导致编译错误

答案：E

解释：

# 题目编号：36

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <deque>
#include <vector>
#include <iostream>
using namespace std;

int main ()
{
 int t[] = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
vector<int> v1(t, t + 10);
deque<int> d1(v1.begin(), v1.end());
deque<int> d2;
d2 = d1;
d2.insert(d1.rbegin(), 10);

for(int i = 0; i<d1.size(); i++)
{
  cout<<d1[i]<<" ";
}
return 0;
}
```

- A. 程序输出：0 1 2 3 4 5 6 7 8 9 10
- B. 程序输出：10 0 1 2 3 4 5 6 7 8 9
- C. 程序输出：0 1 2 3 4 5 6 7 8 9
- D. 编译错误

答案：D

解释：

# 题目编号：37

当你尝试编译并运行以下代码时会发生什么：

```cpp
#include <iostream>
using namespace std;
int main()
{
  cout<<100<<" ";
  cout.setf(ios::hex);
  cout<<100<<" ";
  return 0;
}
```

程序输出：

- A. 100 64
- B. 100 0x64
- C. 0x64 0x64
- D. 64 0x64
- E. 100 100

答案：E

解释：

# 题目编号：38

当你尝试编译并运行以下代码时会发生什么？



```cpp
#include <iostream>
using namespace std;
int main()
{
    cout.setf(ios::hex, ios::basefield);
    cout << 100 << " ";
    cout.flags(ios::showbase);
    cout << 100 << " ";
    return 0;
}
```

程序输出：

- A. 64 64
- B. 64 0x64
- C. 0x64 0x64
- D. 64 100
- E. 编译错误

答案：D

解释：

# 题目编号：39

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
int main () {
int t[] = {1,2,3,2,3,5,1,2,7,3,2,1,10, 4,4,5};
vector<int> v (t,t+15);
vector<int>::iterator it = search_n(v.begin(), v.end(), 4, 2);
cout<< it-v.begin();
return 0;
}
```

程序输出：

- A. 10
- B. 3
- C. 1
- D. 15
- E. 编译错误

答案：D

解释：

# 题目编号：40

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <deque>
#include <vector>
#include <iostream>
#include <string>
using namespace std;

template<typename T>
void print(T start, T end)
{
    while (start != end)
    cout<<*start++;
}
int main ()
{
    string t[] = {"one", "two", "three", "four", "five"};
    vector<string> v1(t, t+5);
    deque<string> d1(v1.rbegin(), v1.rend());
    d1.push_back("zero");
    print(d1[0].rbegin(),d1[0].rend());

    return 0;
}
```

- A. 程序输出：zero
- B. 程序输出：if
- C. 编译错误
- D. 程序输出：five

答案：B

# 题目编号：41

在 1 和 2 处独立插入哪些代码会导致程序显示 0 1 2 3 4 5 6 7 8 9？

```cpp
#include <list>
#include <iostream>
using namespace std;
class A { int a; public:
A(int a){this->a=a;}
/* 插入代码 1 */
/* 插入代码 2 */
template<class T> void print(T start, T end) {
while (start != end) {
std::cout << *start << " "; start++;
}
int main() {
A t1[] = { 1, 7, 8, 4, 5 };list<A> l1(t1, t1 + 5);
A t2[] = { 3, 2, 6, 9 };list<A> l2(t2, t2 + 5);
l1.sort();l2.sort();l1.merge(l2);
print(l1.begin(),l1.end());
print(l2.begin(),l2.end());
cout<<endl;
}
```

- A. 位置 1：`operator int() { return a; }`
- B. 位置 1：`operator int() { return a; } bool operator < (const A & b) { return this->a<b.a; }`
- C. 位置 1：`bool operator < (const A & b) { return this->a<b.a; }`
- D. 位置 1：`bool operator < (const A & b) { return this->a;} friend ostream & operator <<(ostream & c, const A & c); 位置 2：`ostream & operator <<(ostream & c, const A & a) { c<<a; }`
- E. 位置 1：`bool operator < (const A & b) { return this->a<b.a; } 位置 2：`ostream & operator <<(ostream & c, const A & a) { c<<a; }`

答案：A,D

解释：

# 题目编号：42

当你尝试编译并运行以下代码会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int main () {
 int t[] = {1,2,3,4,5,1,2,3,4,5};
vector<int> v (t,t+10);
vector<int>::iterator it;
int m1[] = { 1, 2, 3 };
it = search (v.begin(), v.end(), m1,m1+3);
cout << "found at position: " << it-v.begin() << endl;
return 0;
}
```

程序输出：

- A. 在位置：5
- B. 在位置：0
- C. 在位置：6
- D. 在位置：1
- E. 在位置：10

答案：B

解释：

# 题目编号：43

当你尝试编译并运行以下代码会发生什么？

```cpp
#include <deque>
#include <iostream>
#include <algorithm>
using namespace std;
template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o){}
void operator() (const T & val ) { out<<val<<" "; } };
struct Sequence { int start; }
Sequence(int start):start(start){}
int operator()(){return 10*(1+(start++ % 3));};

int main() {
deque<int> d1(10);

generate(d1.begin(), d1.end(), Sequence(1));
sort(d1.begin(), d1.end());

pair<deque<int>::iterator, deque<int>::iterator> result = equal_range(d1.begin(), d1.end(), 20);

for_each(result.first, result.second, Out<int>(cout));cout<<endl;
return 0;
}
```

程序输出：

- A. 10 10 10 20 20 20 30 30 30
- B. 20 20 20
- C. 10 20 20 20
- D. 20 20 20 30
- E. 10 20 20 20 20 30

答案：B

解释：

# 题目编号：44

独立引入哪些更改将允许代码编译并显示

"one" "eight"

"nine" "ten" 请全选



```cpp
#include <iostream>
#include <map>
#include <string>
using namespace std;
class A {

int a;
public:
A(int a):a(a){}
int getA() const { return a;}
/* 插入代码 1 */
/};
/* 插入代码 2 */

int main(){
 int t[] = {3, 4, 2, 1, 6, 5, 7, 9, 8, 10 };
string s[] = {"three", "four", "two", "one", "six", "five", "seven", "nine", "eight", "ten"};

map<A, string> m;/* 替换代码 3 */
for(int i=0; i<10; i++) {
m.insert(pair(A(t[i]), s[i]));
}
map<A, string>::iterator i=m.lower_bound(A(2));/* 替换代码 4 */
for(;i!=m.end(); i++) {
cout<<i->second<<" ";
}
}
```

- A. 位置 1：`operator int() const { return a; }`
- B. 位置 1：`bool operator < (const A & b) const { return a<b; }`
- C. 位置 1：`bool operator < (const A & b) const { return this->a<b.a; }`
- D. 位置 1：`bool operator < (const A & b) { return this->a;} friend ostream & operator <<(ostream & c, const A & c); 位置 2：`ostream & operator <<(ostream & c, const A & a) { c<<a; }`

答案：A,D

解释：

# 题目编号：45

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <functional>

using namespace std;
template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o){}
void operator()(const T & val) { out<<val<<"; } };

int main() {
 int t1[]={3,2,4,1,5};
int t2[]={6,10,8,7,9};
vector<int> v1(5);
transform(t1,t1+5,t2,v1.rbegin(), plus<int>());
for_each(v1.rbegin(), v1.rend(), Out<int>(cout));cout<<endl);
return 0;
}
```

程序输出：

- A. 9 12 12 8 14
- B. 14 8 12 12 9
- C. 3 2 4 1 5 6 10 8 7 9
- D. 1 2 3 4 5 6 7 8 9 10
- E. 编译错误

答案：A

解释：

# 题目编号：46

当你尝试编译并运行以下代码会发生什么？

```cpp
#include <vector>
#include <iostream>
```

```cpp
#include <algorithm>
using namespace std;
class B {
  int val;
public:
  B(int v):val(v){}
  int getV() const { return val; }
  bool operator < (const B & v) const { return val<v.val; };
  ostream & operator <<(ostream & out, const B & v) { out<<v.getV(); return out; }
};
template<class T>struct Out {
  ostream & out;
  Out(ostream & o): out(o){ }
  void operator() (const T & val ) { out<<val<<" "; } };};


int main() {
  B t1[]={3,2,4,1,5};
  int t2[]={5,6,8,2,1};
  vector<B> v1(10,0);
  sort(t1, t1+5);
  sort(t2, t2+5);
  set_union(t1,t1+5,t2+5,v1.begin());
  for_each(v1.begin(), v1.end(), Out<B>(cout));cout<<endl;
  return 0;
}
```

程序输出：

A. 3241568210
B. 1234568210
C. 1122345568
D. 1234568000
E. 编译错误

答案：E

解释：

# 题号：47

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <map>
#include <vector>
#include <sstream>
#include <string>
using namespace std;
int main(){
  int t[] = {3, 4, 2, 1, 6, 5, 7, 9, 8, 0 };
  vector<int> v(t, t+10);
  map<int,string> m;
  for(vector<int>::iterator i=v.begin(); i!=v.end(); i++) {
    string s; s<<*i<<*i; m.insert(pair<int,string>(*i,s.str));
  }
  for(map<int, string>iterator i=m.begin();i!= m.end(); i++) {
    cout<<i->second<<"";
  }

  return 0;
}
```

- A. 程序输出：3 4 2 1 6 5 7 9 8 0
- B. 程序输出：00 11 22 33 44 55 66 77 88 99
- C. 程序输出：0 1 2 3 4 5 6 7 8 9
- D. 程序输出：0 0 1 11 2 22 3 33 4 44 5 55 6 66 7 77 8 88 9 99
- E. 编译错误

答案：E

解释：

# 题号：48

假设文件 `test.in` 包含以下序列：1 2 3，当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <fstream>
#include <string>
#include <list>
#include <algorithm>
using namespace std;
template<class T>struct Out {
```

程序将输出：

- A. 1 2 3
- B. 1 2 3
- C. 无输出
- D. 编译错误
- E. 程序无限运行无输出

答案：B

解释：

# 题号：49

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

template<class T>struct Out {
  ostream & out;
  Out(ostream & o): out(o){}
  void operator() (const T & val) { out<<val<<" "; }

int main() {
  int t1[]={3,2,4,1,5};
  int t2[]={6,10,8,7,9};
  vector<int> v1(10);

  sort(t1, t1+5); sort(t2, t2+5);

  copy(t1,t1+5,v1.begin());
  copy(t2,t2+5,v1.begin()+5);
  merge(v1.begin(), v1.begin()+5,v1.end());

  for_each(v1.begin(), v1.end(), Out<int>(cout));cout<<endl;

  return 0;
}
```

程序输出：

- A. 1 2 3 4 5 6 10 8 7 9
- B. 3 2 4 1 5 6 10 8 7 9
- C. 3 2 4 1 5 6 7 8 9 10
- D. 1 2 3 4 5 6 7 8 9 10
- E. 编译错误

答案：E

解释：



# 题号：50

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <vector>
#include <set>

struct Sequence {
  int start;
  Sequence(int start):start(start){}
  int operator() { return start++; }
};
bool predicate(int v) { return v%2==0; }
int main() {
  vector<int> v1(10);
  generate_n(v1.begin(), 10, Sequence(1));
  set<int> s1(v1.begin(), v1.end());
  remove_if(s1.begin(), s1.end(), predicate);
  for_each(s1.begin(), s1.end(), predicate);cout<<endl;
  return 0;
}
```

程序输出：

- A. 1 3 5 7 9 6 7 8 9 10
- B. 1 3 5 7 9
- C. 2 4 6 8 10
- D. 编译错误

答案：D

解释：

# 题号：51

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <string>
#include <list>
#include <iostream>
using namespace std;

template<class T> void print(T start, T end) {
  while (start != end) {
    std::cout << *start << " ";
    start++;
  }
}
int main() {
  string t1[]={"1", "2", "3", "4", "5", "6", "7", "8", "9", "10"};
  list<string> l1(t1, t1 + 10);
  list<string> l2(l1);
  l2.reverse();
  l1.splice(l1.end(),l2);
  l1.unique();
  print(l1.begin(), l1.end()); cout<<endl;
  return 0;
}
```

- A. 编译错误
- B. 程序输出：1 2 3 4 5 6 7 8 9 10 8 7 6 5 4 3 2
- C. 程序输出：1 2 3 4 5 6 7 8 9 10 9 8 7 6 5 4 3 2
- D. 程序输出：1 2 3 4 5 6 7 8 9 10

答案：B

解释：

# 题号：52

当你尝试运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
int main () {
  int t[] = {1,2,3,4,5,1,2,3,5,4};
  vector<int> v(t,t+10);
  vector<int>::iterator it;
  int m1[] = {1, 3, 2};
  it = find(v.begin(), v.end(), m1, m1+3);
  if (it != v.end())
    cout << "Found at position: " << it-v.begin() << endl;
  return 0;
}
```

- A. 程序输出：Found at position: 5
- B. 程序输出：Found at position: 0
- C. 无输出
- D. 程序输出：Found at position: 10

答案：C

解释：

# 题号：53

当你尝试编译并运行以下代码时，假设文件 `test.in` 包含以下序列：1 2 3？

```cpp
#include <iostream>
#include <fstream>
#include <string>
#include <list>
#include <algorithm>
using namespace std;
template<class T>struct Out {
  ostream & out;
  Out(ostream & o): out(o){}
  void operator()(const T & val ) {out<<val<<" "; }; };
int main () {
  ifstream f("test.in");
  list<int> l;
  for(; f.good(); ) {
    int i;
    f>>i;
    l.push_back(i);
  }
  f.close();
  for_each(l.begin(), l.end(), Out<int>(cout));
  return 0;
}
```

程序将输出：

- A. 1 2 3
- B. 1 2 3 3
- C. 无输出
- D. 编译错误
- E. 程序无限运行无输出

答案：A

解释：

# 题号：54

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <vector>
#include <iostream>
int main () {
  int t[]={1,2,3,4,5};
  vector<int> v1(t,t+5);
  vector<int> v2(v1);
  v1.resize(10);
  v2.reserve(10);
  vector<int>::iterator i = v1.begin();
  int ii = 0;
  while (i != v1.end()) {
    std::cout << i[ii] << " ";
    i++;
  }
  i = v2.begin();
  while (i != v2.end()) {
    std::cout << i[ii] << " ";
    i++;
  }
  return 0;
}
```

- A. 程序输出：1 2 3 4 5 1 2 3 4 5
- B. 编译错误
- C. 程序输出：1 2 3 4 5 0 0 0
- D. 程序输出：1 2 3 4 5 0 0 0

答案：A

解释：

```cpp
return 0;
}
```

程序输出：

- A. 1 2 3 4 5 6 7 8 9 10
- B. 2 3 4 5 6 7 8 9 10 11
- C. 10 9 8 7 6 5 4 3 2 1
- D. 11 10 9 8 7 6 5 4 3 2
- E. 编译错误

答案：D

解释：

题目编号：58

独立引入的哪些更改允许代码通过编译并显示“one” “eight” “nine” “ten”？选择所有适用项。

```cpp
#include <iostream>
#include <map>
#include <string>
using namespace std;
class A {
int a;
public:
```

```cpp
A(int a):a(a){
int getA() const { return a; }
/* 在此处插入代码 1 */
/};
/* 在此处插入代码 2 */
int main() {
int t[]={ 3, 4, 2, 1, 6, 5, 7, 9, 8, 10 };
string s[] = {"three","four","two","one","six","five","seven","nine","eight","ten"};
multimap<A,string> m;/* 在此处替换代码 3 */
for(int i=0; i<10; i++) {

m.insert(pair<A,string>(A(t[i]),s[i]));
}
m.erase(m.lower_bound(2),m.upper_bound(7));
multimap<A, string>::iterator i=m.begin();/* 在此处替换代码 4 */
for( ; i!=m.end(); i++) {
cout<<i->second<<" ";
}
out<<endl;
return 0;
}
```

- A. 在 Place 1 插入 `operator int() const { return a; }`
- B. 在 Place 1 插入 `bool operator < (const A & b) const { return a.b; }`
- C. 在 Place 1 插入 `bool operator < (const A & b) const { return b.a<a; }`



```cpp
struct R { bool operator()(const A& a, const A& b) { return a.getA()<b.getA(); }; 插入到

Place 2 

将标记为 3 的行替换为 `multimap<A, string, R> m;`

将标记为 4 的行替换为 `multimap<A, string, R>::iterator i=m.begin();`

```
答案：A,B,D

解释：

# 题目编号：59

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <map>
using namespace std;

int main() {

t t[] = { 10, 5, 9, 6, 2, 4, 7, 8, 3, 1 };
map<int, int> m;
for(int i=0; i < 10; i++) {

m[i]=t[i];
}
map<int, int>::iterator it = find(m.begin(), m.end(), 5);
cout<<it?first;
```

```cpp
return 0;
}
```

程序输出：

- A. 5
- B. 4
- C. 10
- D. 编译错误

答案：D

解释：

# 题目编号：60

当你尝试编译并运行以下代码时会发生什么？选择所有适用项。

```cpp
#include <iostream>
#include <fstream>
#include <string>
#include <list>
#include <algorithm>
#include <iomanip>
using namespace std;
template<class T>struct Out {
```

```cpp
ostream & out;
Out(ostream & o): out(o){
void operator()(const T & val) {out<<setw(3)<<val;
int main() {
int t[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
fstream f("test.out", ios::trunc|ios::out);
list<int> l(t, t+10);
for_each(l.begin(), l.end(), Out<int>(f));
f.close(); f.open("test.out");
for(; f.good(); ) {

int i; f>>i;

cout<<i<<""
}
f.close();
return 0;
}
```

- A. 打开 `test.out` 写入
- B. `test.out` 被截断
- C. 打开 `test.out` 读取
- D. 文件未创建或打开
- E. 程序输出 1 2 3 4 5 6 7 8 9 10

答案：A,C,E

解释：

# 题目编号：61

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <string>
using namespace std;
template <class T>
class A {
T_v;
public:
A() {}
A(T v) : _v(v){}
T getV() { return _v; }
void add(T & a) { _v+=a; }
void add(string & a) {
_v.insert(0, a);
}
```
```cpp
int main()
{
  A<string>a("Hello");
  string s(" world!");
  a.add(s);
  cout << a.getV() << endl;
}
``````

- A. 程序输出: Hello world!
- B. 编译错误
- C. 程序输出: world!Hello
- D. 程序无输出

答案：B

解释：

# 题目编号：62

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
```
```cpp
using namespace std;
template<class T>struct Out {
stream & out;
Out(ostream & o): out(o){}
void operator()}(const T & val ) {
out<<val<<"" }
};
```
```cpp
struct Sequence {
int start;
Sequence(int start):start(start){}
int operator()(){
return start++; } };
int main() {
vector<int> v1(10);
vector<int> v2(10);
generate(v1.begin(),v1.end(), Sequence(1));
reverse_copy(v1.begin(),v1.end(), v2.begin());
sort(v2.begin(),v2.end(), less_equal<int>());
for_each(v2.begin(),v2.end(), Out<int>(cout));cout<<endl;
return 0;
}
```

程序输出：

- A. 1 2 3 4 5 6 7 8 9 10
- B. 10 9 8 7 6 5 4 3 2 1
- C. 无输出
- D. 编译错误

答案：A

解释：

# 题目编号：63

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <set>
using namespace std;
class A {
int a;
public:
A(int a) : a(a) { }
A() const { return a; } void setA(int a) { this->a = a; }
bool operator < (const A & b) const { return a<b.a; }
};
```
```cpp
struct Compare {
bool operator ()(A & a) {
if (a.getA() < 5) return true;
return false;
}
}
```
```cpp
int main () {
int t[] = {1,2,3,2,5,1,2,7,3,2,10, 4,45};
set<A> d (t,t+13);
number = count(d.begin(), d.end(), Compare());
cout << number;
}
}
```

- A. 12
- B. 4
- C. 2
- D. 0
- E. 编译错误

答案：E

解释：

# 题目编号：64

给定三个文件：`class.h`, `class.cpp` 和 `main.cpp` 包含一个小型 C++ 项目，你尝试编译并运行哪个程序？假设环境完全就绪。

// 文件: main.cpp
```cpp
#include <iostream>
#include "class.h"
using namespace std;
int main()
{
A<int> a;
cout << a.getV() << endl;
return 0;
}
```
// 文件: class.h
```cpp
#ifndef CLASS_
#define CLASS_
template <class T>
class A {
T_v;
public:
A() {}
A(T v);
T getV();
};
#endif
```
// 文件: class.cpp
```cpp
#include "class.h"
template<typename T>
A<T>::A(T v) : _v(v) {}
template<class T>
A<T>::getV() { return _v; }
```

- A. 程序输出: 0
- B. 程序无法编译
- C. 程序输出：不可预测
答案：D

解释：

# 题目编号：65

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
using namespace std;
template<class A>
void f(A a)
{
cout<<1<<endl;
}
void f(int a)
{
cout<<2<<endl;
}
int main()
{
int a = 1;
f<float>(a);
return 0;
}
```



- A. 程序输出: 1
- B. 程序输出: 2
- C. 编译错误
- D. 运行时异常

答案：A

解释：

题目编号：66

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <list>
#include <iostream>
using namespace std;
template<class T> {
void print(T start, T end) {
while (start != end) {
std::cout << *start << " "; start++;
}
}
int main() {
{
int t1[]={ 1, 7, 8, 4, 5 };
list<int> l1(t1, t1 + 5);
int t2[]={ 3, 2, 6, 9, 0 };
list<int> l2(t2, t2 + 5);
l1.sort();
list<int>::iterator it = l2.begin();
it++; it++;
l1.splice(l1.end(),l2, it, l2.end());
print(l1.begin(), l1.end()); cout<<"Size:"<<l1.size();
print(l2.begin(), l2.end()); cout<<"Size:"<<l2.size()<<endl;
return 0;
}
}
```

- A. 程序输出: 1 4 5 7 8 6 9 0 Size:8 3 2 Size:2
- B. 程序输出: 1 4 5 7 8 6 9 0 Size:8 3 2 6 9 0 Size:5
- C. 编译错误
- D. 程序输出: 0 1 4 5 6 7 8 9 Size:8 3 2 Size:2
- E. 程序输出: 0 1 4 5 6 7 8 9 Size:8 3 2 6 9 0 Size:5

答案：A

解释：

题目编号：67

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o){}
void operator())(const T & val ) {
out<<val<<" " ";
}
};
```

```cpp
struct Sequence {
int start;
Sequence(int start):start(start){}
int operator()() { return 10*(1+(start++ % 3)); };
int main() {
vector<int> v1(10);
vector<int> v2(10);
generate(v1.begin(),v1.end(), Sequence(1));nsort(v1.rbegin(),v1.rend());
unique_copy(v1.begin(),v1.end(), v2.begin());
for_each(v2.begin(), v2.end(), Out<int>(cout);cout<<endl;
return 0;
}
}
```

A. 20 30 10 20 30 20 30 10 20
B. 30 20 10 0 0 0 0 0 0 0
C. 30 0 0 0 0 0 0 0 20 10

D. 编译错误

Answer: B

解释:

# 题目编号: 68

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <set>
using namespace std;
class A {
int a;
public:
    A(int a) : a(a) {}
    int getA() const { return a; } 
    void setA(int a) { this->a = a; }
    operator int() const { return a;}
};
```

```cpp
int main() {
    int t[] = {1,2,3,2,3,5,1,2,7,3,2,1,10, 4,4,5};
    set<A> s (t,t+15);
    cout<<equal(s.begin(), s.end(), t)<<endl;
    return 0;
}
```

程序输出：
- A. true
- B. false
- C. 1
- D. 0
- E. 编译错误

Answer: D

解释:

# 题目编号: 69

在类 B 的标记处添加哪种方法可以让以下代码通过编译？请选择所有可能的解决方案。

...（后续内容以此类推）

## 问题编号: 81

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <set>
using namespace std;
int main() {
    int t[] = {1,2,3,2,3,5,1,2,7,3,2,1,10,4,4,5};
    vector<int> v1(t, t + 15);
    set<int> s1(t, t + 15);
    pair<set<int>::iterator, vector<int>::iterator> resultSet = mismatch(s1.begin(), s1.end(), v1.begin());
    cout << resultSet.first << " " << resultSet.second << endl;
    return 0;
}
```

程序输出：
A. 24
B. 42
C. 05
D. 编译错误

答案：B

解释：

## 问题编号: 82

哪些独立引入的更改允许代码通过编译并显示 0 0 1 1 8 8 9 9（选择所有适用）？

```cpp
#include <iostream>
#include <set>
#include <vector>
using namespace std;
class A {
    int a;
public:
    A(int a):a(a){}
    int getA() const { return a;}
    /* 在此处插入代码 1 **/
};
/* 在此处插入代码 2 **/
```

```cpp
int main() {
    A t[] = { 3, 4, 2, 1, 6, 7, 9, 8, 0 };
    set<A> s(t, t+10);/* 替换代码 3 */
    multiset<A> s1(s.begin(),s.end());/* 替换代码 4 */
    s1.insert(s1.begin(),s1.end());
    s1.erase(s1.lower_bound(2),s1.upper_bound(7));
    multiset<A>::iterator i=s1.begin();/* 替换代码 5 */
    for(;i!=s1.end(); i++)
    {
      cout<<i << " " << i->getA();
    }
    cout<<endl;
    return 0;
}
```

A. 在位置 1 插入 `operator int() const { return a; }`
B. 在位置 1 插入 `bool operator < (const A & b) const { return a < b; }`
C. 在位置 1 插入 `bool operator < (const A & b) const { return b < a; }`
D. 在位置 2 插入 `struct R { bool operator ()(const A & a, const A & b) { return a.getA()<b.getA(); }; }`，并替换标记为 3 的行变为 `set<A,R>s(t, t+10);`，替换标记为 4 的行变为 `multiset<A,R> s1(s.begin(),s.end());`，替换标记为 5 的行变为 `multiset<A,R>::iterator i=s1.begin();`

答案：A,B,D

解释：

## 问题编号: 83

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <deque>
#include <iostream>
#include <algorithm>
using namespace std;
```



## 问题编号: 84

当你尝试编译并运行以下代码时会发生什么？选择所有适用项。

```cpp
template<class T>
struct Out {
    ostream & out;
    Out(ostream & o) : out(o){}
    void operator() (const T & val) { out<<val<<" "; }
};

int main() {
    int t[]={8, 10, 5, 1, 4, 6, 7, 9, 3};
    deque<int> d1(t, t+10);
    deque<int>::iterator it = lower_bound(d1.begin(), d1.end(), 4);
    for_each(it, d1.end(), Out<int>(cout));
    cout<<endl;
    return 0;
}
```

程序输出：
A. 8 10 5 1 4 6 2 7 9 3
B. 4 5 6 7 8 9 10
C. 1 2 3 4 5 6 7 8 9 10
D. 编译错误
E. 1 2 3 4

答案：A

## 问题编号: 84

当你尝试编译并运行以下代码时会发生什么？选择所有适用项。

```cpp
#include <iostream>
#include <fstream>
#include <string>
#include <list>
#include <algorithm>
#include <iomanip>
using namespace std;

class B { 
    int val;
public:
    B(int v=0):val(v){}
    int getV() const { return val;}
    operator int() const { return val; };
};

template<class T>
struct Out {
    ostream & out;
    Out(ostream & o): out(o){}
    void operator()(const T & val ) {out<<setw(3)<<hex<<val; } 
};
```

```cpp
int main () {
    int t[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    fstream f("test.out", ios::trunc);
    list<B> l(t, t+10);
    for_each(l.begin(), l.end(), Out<B>(f));
    f.close();
    f.open("test.out");
    for(; f.good(); ) {
        int i;
        f>>i;
        cout<<i<<" ";
    }
    return 0;
}
```

A. 打开 `test.out`
B. `test.out` 被截断
C. 打开 `test.out` 读取
D. 既未创建也打开
E. 程序显示 1 2 3 4 5 6 7 8 9 10

答案：A,C,E

解释：

## 问题编号: 85

当你尝试编译并运行以下代码会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

class B { 
    int val;
public:
    B(int v):val(v){}
    int getV() const { return val;} 
    bool operator >(const B & v) const { return val>v.val; }
    ostream & operator<<(ostream & out, const B & v) { out<<getV(); return out;}
};

template<class T>
struct Out {
    ostream & out;
    Out(ostream & o): out(o){}
    void operator()(const T & val ) { out<<val<<" "; }
};

int main() {
    B t[]={3,2,4,1,5,10,9,7,8,6};
    vector<B> v1(t, t+10);
(sort(.begin(), v1.end. greater<B>());
    cout<<*min_element(v..(),(),(),1..());());
return 0;
```

：
A. . B.  
C.  
D. 10
E. 编译错误

答案：E

## 问题编号: 86

假设输入序列 64 100，尝试编译并运行以下代码会发生什么？

```cpp
#include <iostream>
#include <string>
#include <sstream>
#include <iomanip>
using namespace std;

int main () {
    string s;
    getline(cin, s);
    stringstream input(s);
    stringstream output;
    for(!input.fail()) {
        int i;
        input>>hex>>i;
        output<<setw(4)<<i;
    }
    cout<<output.str();
    return 0;
}
```

A. 64 100
B. 100 256
C. 100 256 256
D. 0x64 100
E. 0x100 256 256

答案：C

解释：

## 问题编号: 87

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <functional>
using namespace std;

template<class T>
struct Out {
    ostream &out;
    Out(ostream &o): out(o){}
    void operator() (const T & val ) { out<<val<<" "; }
};

int Add(int a, int b) {
    return a+b;
}

int main() {
    int t[]={1,2,3,4,5,6,7,8,9,10};
    vector<int> v1(t, t+10);
    vector<int> v2(10);
    transform(v1.begin(), v1.end(), v2.begin(), bind(Add, 1));
    for_each(v2.begin(), v2.rend(), Out<int>(cout));
    cout<<endl;
    return 0;
}
```

程序输出：
A. 1 2 3 4 5 6 7 8 9 10
B. 2 3 4 5 6 7 8 9 10 11
C. 10 9 8 7 6 5 4 3 2 1
D. 11 10 9 8 7 6 5 4 3 2
E. 编译错误

答案：D

解释：

## 问题编号: 88

当你尝试编译并运行以下代码时会发生什么：

```cpp
#include <vector>
#include <set>
#include <iostream>
#include <algorithm>
using namespace std;

template<class T>
struct Out {
    ostream &out;
    Out(ostream & o) : out(o){
    void operator()(const T & val) { out<<val<<" "; } }
};

struct Sequence {
    int start;
    Sequence(int start):start(start){}
    int operator() { return start++; }
};

int main() {
    vector<int> v1(10);
    generate_n(v1.begin(), 10, Sequence(1));
    random_shuffle(v1.rbegin(), v1.rend());
    sort(v1.begin(), v1.end(), greater<int>());



```cpp
for_each(v1.begin(), v1.end(), Out<int>(cout<<endl));

return 0;

}
```

程序输出：
A. 8 10 5 1 4 6 2 7 9 3
B. 1 2 3 4 5 6 7 8 9 10
C. 编译错误
D. 10 9 8 7 6 5 4 3 2 1

答案：C

解释：

## 问题编号: 89

当你尝试编译并运行以下代码会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <map>
using namespace std;
void myfunction(pair<int, int> i) {
    cout << "" << i.first;
}
int main() {
    int t[] = { 10, 5, 9, 6, 2, 4, 7, 8, 3, 1 };
    map<int, int> m;
    for(int i=0; i < 10; i++) {
        m[i]=t[i];
    }
    for_each(m.begin(), m.end(), myfunction);
    return 0;
}
```

程序输出：
A. 105 96 247 83
B. 012 345 567 89
C. 98 765 432 210
D. 138 742 695
E. 编译错误

答案：B

解释：

## 问题编号: 90

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout<<true<<boolalpha<<false;
    return 0;
}
```

程序输出：
A. true false
B. 0
C. 1 false
D. true 0
E. 编译错误

答案：C

解释：

```cpp
for_each(v1.begin(), v1.end(), Out<B>(cout));cout<<endl;
return 0;
}
```

程序输出：
- A. 8 10 5 1 4 2 7 9 3
- B. 1 2 3 4 5 6 7 8 9 10
- C. 编译错误
- D. 10 9 8 7 6 5 4 3 2 1

答案: B

解析:

## 题号: 92

关于下面的代码，哪句描述是正确的？选择所有适用项。

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
class F {
int val;
public:
F(int v):val(v){}
```
```cpp
bool operator() (int v) {
  if (v == val) return true;
  return false;
}
;
```
int main() {
```cpp
int t[] = { 10, 5, 9, 6, 2, 4, 7, 8, 3, 1 };
vector<int> v1(t, t + 10);
if (find(v1.begin(), v1.end(), 6) == find(v1.begin(), v1.end(), F(6))) {
  cout<<"Found!\n";
} else {
  cout<<"Not found!\n";
}
return 0;
}
```

- A. 它将成功编译
- B. 它将显示 Found!
- C. 它将显示 Not found!
- D. 它将无法成功编译

答案: D

解析:

## 题号: 93

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <deque>
#include <vector>
#include <iostream>
using namespace std;
int main ()
{
vector<int>v1;
deque<int>d1;
for(int i=0; i<5; i++)
{
v1.push_back(i);v1.push_front(i);
d1.push_back(i);d1.push_front(i);
}
for(int i=0; i<d1.size(); i++)
{
cout<<d1[i]<<" "<<v1[i]<<" ";
}
cout<<endl;
return 0;
}
```

它的输出将：
- A. 4433222100001223344
- B. 因第11行导致运行时异常错误
- C. 因第12行导致编译错误

答案: C

解析:

## 题号: 94

当你尝试编译并运行以下代码时会发生什么：

```cpp
#include <iostream>
#include <algorithm>
#include <deque>
#include <vector>
using namespace std;
bool identical(int a, int b) {
return b == 2*a?true:false;
}
int main() {
int t[] = {1,2,3,2,3,5,1,2,7,3,2,1,10, 4,4,5};
```
```cpp
int u[] = {2,4,6,4,6,10,2,14,6,4,20,8,8,5};
vector<int> v1(t, t + 15);
deque<int> d1(u, u + 15);
```
```cpp
pair<deque<int>::iterator, vector<int>::iterator > result;
result = mismatch(d1.begin(), d1.end(), v1.begin(), identical); //Line I
if (result.first == d1.end() && result.second == v1.end())//Line II
```cpp
cout<<"Identical\n";
} else {
cout<<"Not identical\n";
}
return 0;
}
```

程序输出：
- A. Identical
- B. Not identical
- C. I行编译错误
- D. II行编译错误

答案: B

解析:

## 题号: 95

假设你输入以下序列：true false，当你尝试编译并运行下面的代码会发生什么？

```cpp
#include <iostream>
#include <string>
using namespace std;
int main ()
{
bool a,b;
cin>>a>>b;
cout<<a<<b;
return 0;
}
```

程序输出：
- A. true
- B. true0
- C. false
- D. 10
- E. 以上都不是

答案: D

解析:

## 题号: 96

尝试编译并运行以下代码会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
class B { int val;
public:
B(int v):val(v){}
int getV() const { return val; } operator <(const B & v) const { return val; }
ostream & operator<<(ostream & out, const B & v) { out<<v.getV(); return out; }
template<class T>struct Out {
ostream & out;
Out(ostream & o){
void operator()(const T & val) { out<<val<<" "; };
int main() {
int t[]={8, 10, 5, 1, 4, 6, 7, 9, 3};
vector<B> v1(t, t+10);
sort(v1.begin(), v1.end(), greater<B>());
for_each(v1.begin(), v1.end(), Out<B>(cout));cout<<endl;
return 0;
}
```

程序输出：
- A. 8 10 5 1 4 6 7 9 3
- B. 1 2 3 4 5 6 7 8 9 10
- C. 编译错误
- D. 10 9 8 7 6 5 4 3 2 1

答案: C

解析:

## 题号: 97

尝试编译并运行以下代码会发生什么？



```cpp
#include <iostream>

using namespace std;

template <class T>
class A {
T _v;
public:
  A() {}
  A(T v) : _v(v){}
  friend ostream & operator<<(ostream & c, const A<T> & v);
};
```

```cpp
template <class T>
ostream & operator<<(ostream & c, const A<T> & v) {
c<<v._v;return c;
}
```

```cpp
int main()
{
  A<int>a(10);
  cout<<a<<endl;
  return 0;
}
```

- A. 程序显示:10
- B. 程序无法编译
- C. 程序将编译
- D. 程序将无输出

答案: B

解析:

## 题号: 98

尝试编译并运行以下代码会发生什么：

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <functional>
using namespace std;
class B { int val;
public:
B(int v=0):val(v)
int getV() const { return val;}
operator int () const { return val; };
```

```cpp
template<class T>struct Out {
ostream &out;
Out(ostream & o) : out(o)
void operator()(const T & val) { out<<val<<" "; } };
```

```cpp
int main() {
B t[]={3,2,4,1,5,6,10,8,7,9};
vector<B> v1(t, t+10);
for_each(v1.begin(), v1.end(), bind(plus<B>(), 1));
for_each(v1.rbegin(), v1.rend(), Out<B>(cout));cout<<endl;
return 0;
}
```

程序输出：
- A. 3 2 4 1 5 6 10 8 7 9
- B. 4 3 5 2 6 7 11 9 8 10
- C. 9 7 8 10 6 5 1 4 2 3
- D. 10 8 9 11 7 6 2 5 3 4
- E. 编译错误

答案: C

解析:

## 题号: 99

尝试编译并运行以下代码会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
class A {
int a;
public:
A(int a) : a(a) {}
int getA() const { return a; } setA(int a){ this->a = a; }
bool operator===(A & b) { return a == b.a; }
};
struct Compare {
bool operator()(const A & a, const A & b) {return a.getA() < b.getA();};
};
```

```cpp
int main () {
int t[] = {1,2,3,4,5,1,2,3,4,5};
vector<A> v(t, t+10);
vector<A>::iterator it;
A m1[] = {A(1), A(2), A(3)};
it = search(v.begin(), v.end(), m1, m1+3, Compare());
cout << "Found at position: " << it-v.begin() << endl;
return 0;
}
```

程序输出：
- A. Found at position: 5
- B. Found at position: 0
- C. Found at position: 7
- D. 编译错误
- E. Found at position: 10

答案: B

解析:

## 题号: 100

尝试编译并运行以下代码会发生什么？

```cpp
#include <deque>
#include <iostream>
#include <algorithm>
using namespace std;
class B { int val;
public:
B(int v):val(v){}
int getV() const { return val; };
ostream & operator<<(ostream & out, const B & v) { out<<v.getV(); return out; }
template<class T>struct Out {
ostream & out;
Out(ostream & o):out(o){}
void operator()(const T & val) { out<<val<<" };
int main() {
t[]={8, 10, 5, 1, 4, 6, 2, 7, 9, 3};
deque<B> d1(t, t+10);
deque<B>::iterator it = lower_bound(d1.begin(), d1.end(), 4);
for_each(it, d1.end(), Out<B>(cout));cout<<endl;
return 0;
}
```

程序输出：
- A. 8 10 5 1 4 6 2 7 9 3
- B. 4 5 6 7 8 9 10
- C. 1 2 3 4 5 6 7 9 10
- D. 编译错误
- E. 1 2 4

答案: D

解析:

## 题号: 101

尝试编译并运行以下代码会发生什么？

```cpp
#include <deque>
#include <iostream>
#include <algorithm>
using namespace std;

class B { int val;
public:
B(int v):val(v){}
int getV() const { return val; } operator < (const B & B) const { return val<v.val; };
ostream & operator<<(ostream & out, const B & v) { out<<v.getV(); return out; }
template<class T>struct Out {
ostream & out; Out(ostream & o): out(o){
void operator()(const T & val) { out<<val<<" };
int main() {
t[]={20, 30, 10, 20, 30, 10, 20, 30, 20};
deque<B> d1(t, t+10);
sort(d1.begin(), d1.end());
pair<deque<B>::iterator, deque<B>::iterator> result = equal_range(d1.begin(), d1.end(), B(20));
for_each(result.first, result.second, Out<B>(cout));cout<<endl;
return 0;
}
```

程序输出：
- A. 10 10 10 20 20 20 30 30 30
- B. 20 20 20
- C. 10 20 20 20
- D. 20 20 20 30 30
- E. 10 20 20 20 30

答案: B

解析:

## 题号: 102

尝试编译并运行以下代码会发生什么？



```cpp
#include <iostream>
#include <deque>
#include <list>
#include <queue>
#include <vector>

using namespace std;

int main()
{
int t[]={ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
deque<int> mydeck(t, t+10);list<int> mylist(t,t+10);
queue<int> first;
queue<int> second(mydeck);
queue<int> third(second);
queue<int, list<int>> fourth(mylist);
mylist.clear();third.clear();
cout << third.size() << " " << "mydeck.size()" << endl;
cout << fourth.size() << " " << "mylist.size()" << endl;
return 0;
}
```

- A. 程序输出: 10 0

10 0

- B. 程序输出: 0 0

0 0

- C. 程序输出: 10 10

10 10

D. 程序输出: 10 0 0 10

E. 编译错误

答案: E

解释:

# 题目编号: 103

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <deque>
#include <list>
#include <queue>
#include <vector>

using namespace std;
class compare {
    bool reverse;
public:
    compare(bool revparam = false){ reverse = revparam};
    bool operator()(int lhs, int rhs) const{
        if (reverse)return (lhs > rhs);
        else return (lhs < rhs);
    }
};
int main(){
    int myints[] = { 3, 4, 2, 1, 6, 5, 7, 9, 8, 0 };
```

```cpp
priority_queue<int, deque<int>> first(myints, myints + 10);
priority_queue<int, vector<int>, compare<int>> second(myints, myints + 10,
compare(false));
while (first.size() > 0){
```

```cpp
cout << first.top() << " "; first.pop();
}
while (second.size() > 0) {
cout << second.top() << " ";second.pop();
}
return 0;
}
```

A. 编译错误

B. 程序输出: 9 8 7 6 5 4 3 2 1 0 9 8 7 6 5 4 3 2 1 0

C. 程序输出: 9 8 7 6 5 4 3 2 1 0 1 2 3 4 5 6 7 8 9 0

D. 程序输出: 3 4 2 1 6 5 7 9 8 0 3 4 2 1 6 5 7 9 8 0 0

答案: B

解释:

# 题目编号: 104

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <deque>
#include <iostream>
#include <algorithm>
#include <set>
using namespace std;

template<class T>struct Out {
 ostream &o;

Out(ostream &o) : out(o);
 void operator()(const T &val) { out<<val<<" "; } };

int main() {
 int t[]={8, 10, 5, 1, 4, 6, 2, 7, 9, 3};
```

```cpp
deque<int> d1(t, t+10);
set<int> s1(t,t+10);
cout<<binary_search(s1.begin(),s1.end(), 4)<< <<binary_search(d1.begin(),d1.end(), 4)<<endl;
return 0;
}
```

选择所有可能的输出（所有适用项）：

- A. 1 0

- B. 1 1

- C. true false

- D. false false

- E. 编译错误

答案: A,B

解释:

# 题目编号: 105

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
template<class T>struct Out {
ostream &o;
Out(ostream & o) : out(o){
void operator()(const T & val) { out<<val<<" " ; } };
```

```cpp
struct Add {
int operator()(int & a, int & b) {
return a+b;
}
};
int main() {
 t[]={1,2,3,4,5,6,7,8,9,10};
vector<int> v1(t, t+10);
```

```cpp
vector<int> v2(10);
transform(v1.begin(), v1.end(), v2.begin(), bind2nd(Add(),1));
for_each(v2.rbegin(), v2.rend(), Out<int>(cout));cout<<endl;
return 0;
}
```

程序输出:

- A. 1 2 3 4 5 6 7 8 9 10

- B. 2 3 4 5 6 7 8 9 10 11

- C. 10 9 8 7 6 5 4 3 2 1

- D. 11 10 9 8 7 6 5 4 3 2

- E. 编译错误

答案: E

解释:

# 题目编号: 106

当你尝试编译并运行以下代码时会发生什么，假设你输入以下序列：1 2 3<enter>？

```cpp
#include <iostream>

using namespace std;

int main ()
{}
```

```cpp
int a,b,c;
cin>>a>>b>>c;
cout<<a<<b<<c<<endl;
return 0;
}
```

程序将输出:

- A. 123

- B. 1 2 3

- C. 321

- D. 编译错误

- E. 结果未定义

答案: A

解释:

# 题目编号: 107

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <map>
#include <vector>
#include <string>
using namespace std;
int main(){
int second[]={ 3, 4, 2, 1, 6, 5, 7, 9, 8, 0 };
string first[] = {"three", "four", "two", "one", "six", "five", "seven", "nine", "eight", "zero"};
map<int,string> m;
```

```cpp
for(int i=0; i<10; i++) {
m.insert(pair<int,string>(second[i],first[i]));
}
m[0]="ten";
m.insert(pair<int,string>(1,"eleven"));
for(map<int,string>::iterator i=m.begin();i!= m.end(); i++) {
cout<<i<<"";
}
return 0;
}
```

- A. 程序输出: zero one two three four six seven

- B. 程序输出: ten one two three five seven

- C. 程序输出: zero eleven two three five seven

- D. 程序输出: ten eleven two three five seven

- E. 程序输出: 0 1 2 3 4 5 6 7

答案: B

解释:

# 题目编号: 108

当你尝试编译并运行以下代码时会发生什么，假设你输入序列：1 2 3<enter>？



```cpp
#include <iostream>
#include <string>
#include <sstream>

using namespace std;
int main ()
{
  string s;
  getline(cin, s);
  stringstream input(s);
  stringstream output;

  for(; !input.fail(); )
    int i;
    input>>i;
    output<<i<<" ";
  cout<<output.str();
  return 0;
}
```

程序将输出:

- A. 1 2 3

- B. 1 2 3

- C. 0x1 0x2 0x3

- D. 0x1 0x2 0x3

- E. 程序无限循环

答案: B

解释:

## 题目编号: 109

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
struct Compare {
bool operator()(int a) {
if (a >5) return true;
return false;
};
int main () {
int t[] = {1,2,3,2,3,5,1,2,7,3,2,10, 4,5};
vector<int> v (t,t+15);
int number = count(v.begin(), v.end(), Compare());
cout<< number;
}
```

程序输出:

- A. 4

- B. 3

- C. 2

- D. 0

答案 编译错误

解释:

## 题目编号: 110

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <deque>
#include <set>
#include <iostream>
#include <algorithm>
using namespace std;
class B { int val;
public:
B(int v=0):val(v)
int getV() const { return val; }
bool operator <(const B& v) const { return val<v.val; }
ostream& operator<<(ostream& out, const B& v) { out<<v.getV(); return out; }
template<class T>struct Out {
ostream& out;
Out(ostream& o) : out(o){}
void operator() (const T& val) { out<<val<<" } };
int main() {
int t[]={8, 10, 5, 1, 4, 6, 2, 7, 9, 3};
deque<B> d1(t,t+10);
sort(d1.begin(),d1.end());
set<B> s1(t,t+10);
cout<<binary_search(s1.begin(),s1.end(), 4)<< <<binary_search(d1.begin(),d1.end(), 4)<<endl;
return 0;
}
```

程序输出:

- A. 1 0

- B. 1 1

- C. true true

- D. false false

- E. 编译错误

答案: E

解释:

## 题目编号: 111

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
using namespace std;
class A
{
  int a,b;
public:
  A(const A& c) { a = c.a; }
  A():a(0),b(0){}
  void setA(int a) {this->a = a;} void setB(int b) {this->b = b;}
  int getA() {return a;} int getB() {return b;}
};
int main ()
{
  vector<A>v;
  A a;
  a.setA(10); a.setB(11);
  v.push_back(a);
  cout<<v[0].getB()<<v[0].getA()<<endl;
  return 0;
}
```

- A. 程序输出 10 11

- B. 结果不可预测的

- C. 程序输出 10 0

- D. 程序输出 11 0

- E. 编译错误

答案: B

解释:

## 题目编号: 112

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
class B { int val;
public:
B(int v=0):val(v)
int getV() const { return val; }
operator int () const { return val; };
template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o)
void operator()(const T & val ) { out<<val<<" "; } };
struct Add {
B operator()(B & a, B & b) { return a+b; };
int main() {
int t[]={1,2,3,4,5,6,7,8,9,10};
vector<B> v1(t, t+10);
vector<B> v2(10);
transform(v1.begin(), v1.end(), v2.begin(), bind1(Add()),1),
for_each(v2.rbegin(), v2.rend(), Out<B>(cout));cout<<endl;
return 0;
}
```

程序输出:

- A. 1 2 3 4 5 6 7 8 9 10

- B. 2 3 4 5 6 7 8 9 10 11

- C. 10 9 8 7 6 5 4 3 2 1

- D. 11 10 9 8 7 6 5 4 3 2

- E. 编译错误

答案: E

解释:

## 题目编号: 113

当你尝试编译并运行以下代码时会发生什么：

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
template<class T>struct Out {
ostream & out;
Out(ostream & o) : out(o){
void operator() (const T & val ) { out<<val<<" "; } };
int main() {
int t1[]={3,2,4,1,5};
int t2[]={5,6,8,2,1};
vector<int> v1(10);
sort(t1, t1+5);
sort(t2, t2+5);
set_symmetric_difference(t1,t1+5,t2+5,v1.begin());
for_each(v1.begin(), v1.end(), Out<int>(cout));cout<<endl;
return 0;
}
```

程序输出:

- A. 6 8 3 4 0 0 0 0 0

- B. 3 4 0 0 0 0 0 0 0

- C. 6 8 0 0 0 0 0 0 0

- D. 编译错误

- E. 3 4 6 8 0 0 0 0 0

答案: E

解释:

## 题目编号: 114

当你尝试编译并运行以下代码时会发生什么，假设在程序执行之前文件 test.out 已经存在？

```cpp
#include <iostream>
#include <fstream>
```

```cpp
#include <string>
#include <list>
#include <algorithm>
#include <fstream>
using namespace std;

template<class T>
struct Out {
    ostream & out;
    Out(ostream & o) : out(o) {}
    void operator()(const T & val) { out << val << " "; };
};
```



```cpp
int main () {
    int t[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    fstream f("test.out");
    list<int> l(t, t + 10);
    for_each(l.begin(), l.end(), Out<int>(f));
    f.close();
    return 0;
}
```

- A. 将创建并打开文件 `test.out` 用于写入
- B. 将创建并打开文件 `test.out` 用于读取
- C. 既创建也不打开文件
- D. 文件 `test.out` 将包含序列 1 2 3 4 5 6 7 8 9 10
- E. 编译错误

答案: C

解释：

题目编号: 115

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
class A {
    int a;
public:
    A(int a) : a(a) {}
    int getA() { return a; } void setA(int a) { this->a = a; }
    bool operator===(const A &b) const { return a == b.a; }
};
bool compare(const A &a, const A &b) { return a == b; }
int main () {
    int t[] = {1,2,3,3,5,1,2,4,4,5};
    vector<A> v(t,t+10);
    vector<A>::iterator it = v.begin();

    while ( (it = adjacent_find(it, v.end(), compare)) != v.end()) {
        cout << it - v.begin() << ""; it++; }
    }
    cout << endl;
    return 0;
}
```

- A. 程序输出: 2 3
- B. 程序输出: 2 7
- C. 程序输出: 3 8
- D. 编译错误
- E. 程序将无限运行

答案: B

解释：

题目编号: 116

下述代码中的哪些行包含了 `queue` 对象的正确实例化？

```cpp
#include <iostream>
#include <deque>
#include <list>
#include <queue>
#include <vector>
using namespace std;

int main()
{
    deque<int> mydeck;
    list<int> mylist;
    vector<int> myvector;
    queue<int> first; // 行 I
    queue<int> second(mydeck); // 行 II
    queue<int> third(second); // 行 III
    queue<int> fourth(mylistist); // 行 IV
    queue<int> fifth(myvector); // 行 V
    return 0;
}
```

- A. 行 I
- B. 行 II
- C. 行 III
- D. 行 IV
- E. 行 V

答案: A,B,C

解释：

题目编号: 117

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

void print(int v) {
    cout << v << "";
}
struct Sequence {
    int start;
    Sequence(int start):start(start){}
    int operator()() {
        return start++;
    }
};

int main() {
    vector<int> v1(10);
    generate_n(v1.begin(), 10, Sequence(1));

    for_each(v1.begin(), v1.end(), print);
    cout << endl;
    return 0;
}
```

程序输出：

A. 1 2 3 4 5 6 7 8 9 10
B. 0 000000000
C. 编译错误
D. 无输出

答案: A

解释：

题目编号: 118

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
using namespace std;

class C {
public:
    int _c;
    C():_c(0){}
    C(int c) { _c = c; }
    C operator+=(C & b) {
        C tmp;
        tmp._c = _c+b._c;
        return tmp;
    }
};

template <class T>
class A {
    T _v;
public:
    A() {}
    A(T v) : _v(v){}
    T getV() { return _v; }
    void add(T & a) { _v+=a; }
};

int main()
{
    A<int> b(2);
    A<C>a(5);
    C c;
    a.add(c);
    cout << a.getV() << endl;
    return 0;
}
```

A. 程序将显示: 2
B. 程序无法编译
C. 程序可以编译
D. 程序将导致异常

答案: B

解释：

题目编号: 19

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <vector>
#include <iostream>
using namespace std;

int main ()
{
  std::vector<int>v1;
  for(int i = 0; i<10; i++) {v1.push_back(i); }
  v1.resize(4);
  std::vector<int>::iterator it = v1.end();
  v1.insert(v1.end(), 1, 4);
  for(int i=0; i<=v1.size(); i++) {std::cout<<v1.at(i)+" } std::cout<<endl;
  return 0;
}
```

A. 编译错误
B. 程序输出 0 1 2 3 4
C. 程序输出 0 2 4 异常
D. 程序输出 0 2 4 8

答案: C

题目编号: 20

哪些关键字可以定义模板参数？请选择所有答案：

A. `class`
B. `typedef`
C. `typename`
D. `static`
E. `volatile`

答案: A,C

解释：

题目编号: 21

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <iomanip>
using namespace std;
```

显示的数字部分为：

A. 26
B. 000
C. 20
D. 000
E. 26

答案: D

题目编号: 22

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
bool compare(int a, int b) { return a == b; }
int main () {
    int t[] = {1,2,3,4,5,1,2,4,5};
    vector<int> v(t,t+10);
    vector<int>::iterator it = v.begin();
    int m1[] = {1, 2, 3};
    while ((it = find_first_of(it, v.end(), m1, m1+3)) != v.end()) {
        cout << it - v.begin() << ""; it++; }
    cout << endl;
    return 0;
}
```

A. 程序输出: 0 1 2 5 6 7
B. 程序输出: 0 5
C. 程序输出: 0
D. 编译错误
E. 程序无限运行

答案: E

题目编号: 23

当你尝试编译并运行以下代码时，会发生什么？



```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <functional>
using namespace std;
class B { 
    int val;
public:
    B(int v=0):val(v){}
    int getV() const { return val; }
    B operator +(const B &b) const { return B(val+b.val); }
    ostream & operator<<(ostream & out, const B & v) { out<<v.getV(); return out; }
};
template<class T>
struct Out {
    ostream & out;
    Out(ostream & o, const T & v) : out(o){}
    void operator()(const T & val) { out<<val<< " "; };
};
B Add(B a, B b) { return a+b; }
int main() {
    int t[]={1,2,3,4,5,6,7,8,9,10};
    vector<B> v1(t, t+10);
    vector<B> v2(10);
    transform(v1.begin(), v1.end(), v2.begin(), bind(Add));
    for_each(v2.rbegin(), v2.rend(), Out<B>(cout));cout<<endl;
    return 0;
}
```

程序输出：

A. 1 2 3 4 5 6 7 8 9 10 11

B. 2 3 4 5 6 7 8 9 10 11

C. 10 9 8 7 6 5 4 3 2 1

D. 11 10 9 8 7 6 5 4 3 2

E. 编译错误

答案: D

题目编号: 24

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <vector>
#include <iostream>
using namespace std;
class A
{
    int a,b;
public:
    A & operator =(const A & c) { a = c.a; return *this; }
    A():a(0),b(0){}
    void setA(int a) {this->a = a;} void setB(int b) {this->b = b;}
    int getA() {return a;} int getB() {return b;}
};
```

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main ()
{
    float f = 10.126;
    cout<<setprecision(2)<<f;
}
```

程序输出：

A. 10.1

B. 10

C. 10.12

D. 10

10

题目编号: 26

```题目
## 以下代码时，会发生什么？

int main() {
    int t[] = { 10, 5, 9, 6, 2, 4, 7, 8, 3, 1 };
    vector<int> v1(t, t + 10);
    copy_backward(t, t+10, v1.rend());
    for_each(v1.begin(), v1.end(), [](int i) { cout << " " << i; });
    return 0;
}
```

题目编号： 27

```题目
## 以下代码时，会发生什么？

#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

void myfunction(int i) {
    cout << " " << i;
}

int main() {
    int t[] = { 10, 5, 9, 6, 2, 4, 7, 8, 3, 1 };
    vector<int> v1(t, t + 10);
    copy_backward(t, t+10, v1.rend());
    for_each(v1.begin(), v1.end(), myfunction);
    return 0;
}
```

注：由于原文文本在第26题后存在大量截断和格式混乱，翻译已根据上下文对可识别部分进行了逻辑还原

解释：

题编号： 129

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>

#include <algorithm>
using namespace std;
class B { int val;
public:
B(int v):val(v) {}
int getV() const { return val; }
bool operator<(const B & v) const { return val<v.val; }
ostream & operator<<(ostream & out, const B & v) { out<<v.getV(); return out; }
template<class T>struct Out {
ostream & out;
Out(ostream & o) : out(o) {}
void operator()(const T & val ) { out<<val<<" "; } 
};

int main() {
B t1[]={3,2,4,1,5};
B t2[]={6,10,8,7,9};
vector<B> v1(10,0);
sort(t1,t1+5); sort(t2,t2+5);
copy(t1,t1+5,v1.begin());
copy(t2,t2+5,v1.begin()+5);
inplace_merge(v1.begin(), v1.begin()+5,v1.end());
for_each(v1.begin(), v1.end(), Out<B>(cout));cout<<endl;
return 0;
}
```

程序输出：

+   A. 1 2 3 4 5 6 10 8 7 9

B. 3 2 4 1 5 6 7 8 9 10

C. 3 2 4 1 5 6 10 8 7 9

D. 1 2 3 4 5 6 7 8 9 10

E. 编译错误

答案：D

解释：

题编号： 130

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <set>
#include <vector>
using namespace std;
int main(){
int myints[] = { 3, 4, 2, 1, 6, 5, 7, 9, 8, 0 };
set<int>(myints,myints+10);
multiset<int> s1(s.begin(),s.end());
s1.insert(s.begin(),s.end());
s1.erase(s1.lower_bound(2),s1.upper_bound(7));
for(multiset<int>::iterator i=s1.begin();i!=s1.end(); i++) {
  cout<<i<<"";
}
return 0;
}
```

输出将是：

+   A. 0 0 1 1 8 8 9 9

B. 0 1 8 9

C. 2 3 4 5 6 7

D. 3 4 9 8 0

E. 3 3 4 4 9 9 8 8 0 0

答案：A

解释：

题编号： 131

当你尝试编译并运行以下代码时会发生什么？



```cpp
#include <deque>
#include <vector>
#include <iostream>
using namespace std;
int main ()
{
int t[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    deque<int>d1(t, t+10);
    vector<int>v1(t, t+10);
    cout<<v1.size() <<v1.capacity() ";
    cout<<d1.size() <<d1.capacity() ";
    d1.resize(12); v1.resize(12);
    cout<<v1.size() <<v1.capacity() ";
    cout<<d1.size() <<d1.capacity() ";
    d1.reserve(20);v1.reserve(20);
    cout<<v1.size() <<v1.capacity() ";
    cout<<d1.size() <<d1.capacity()<<endl;
    return 0;
}
```

### 题编号：132
当你尝试编译并运行以下代码时会发生什么？

A. 输出为 10 10 10 12 12 20 20
B. `reserve` 和 `resize` 相同
C. 编译错误
D. `capacity` 总是更小

答案：C

解释：

### 题编号：133
当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <deque>
#include <list>
#include <stack>
#include <vector>
using namespace std;
int main()
{
deque<int> mydeck;list<int> mylist; vector<int> myvector;
stack<int> first;
stack<int> second(mydeck);
stack<int> third(second);
stack<int, list<int>> fourth(mylist);
fourth.push(10);fourth.push(11);fourth.push(12);
stack<int, vector<int>> fifth(myvector);
fifth.push(10);fifth.push(11);fifth.push(12);
while(!fifth.empty())
{
cout<<fifth.top()";
fifth.pop();
}
while (!fourth.empty())
{
cout << fourth.front() << " ";
fourth.pop();
}
return 0;
}
```

A. 程序输出：12 11 10
B. 编译错误
C. 程序输出：10 11 12

答案：B

解释：

### 题编号：134
当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
class B { int val;
public:
B(int v=0):val(v){
int getV() const { return val;}
operator int () const { return val; }
ostream & operator<<(ostream & out, const B & v) { out<<v.getV(); return out; }};

template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o){}
void operator()(const T & val ) { out<<val<< " "; }
struct Add {
B operator()(B & a, B & b) { return a+b; }
int main() {
B t[]={1,2,3,4,5,6,7,8,9,10};
vector<B> v1(t, t+10);
vector<B> v2(10);
transform(v1.begin(), v1.end(), v2.begin(), bind(Add(),));
for_each(v2.begin(), v2.end(), Out<B>(cout));cout<<endl;
return 0;
}
```

程序输出：

+   A. 1 2 3 4 5 6 7 8 9 10
B. 2 3 4 5 6 7 8 9 10 11
C. 10 9 8 7 6 5 4 3 2 1
D. 11 10 9 8 7 6 5 4 3 2 1
E. 编译错误

答案：E

解释：

### 题编号：135
当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <list>
#include <iostream>

using namespace std;
template<class T> void print(T start, T end) {
while (start != end) {
std::cout << *start << " "; start++;
}
}
class A {
int a;
public:
A(int a):a(a){}
operator int () const { return a;
int getA() const { return a; }
}
int main() {
int t1[]={ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
list<A> l1(t1, t1 + 10);
list<A> l2(l1);
l2.reverse(); l1.splice(l1.end(),l2);
l1.pop_back();l1.unique();
print(l1.begin(), l1.end()); cout<<endl;
return 0;
}
```

+   A. 编译错误
+   B. 运行时异常
+   C. 程序输出：1 2 3 4 5 6 7 8 9 1 0 9 8 7 6 5 4 3 2
+   D. 程序输出：1 2 3 4 5 6 7 8 9 1 0 9 8 7 6 5 4 3 2
+   E. 程序输出：1 2 3 4 5 6 7 8 9 1 0 9 8 7 6 5 4 3 2

答案：C

解释：

### 题编号：137
当你尝试编译并运行以下代码时会发生什么，假设你输入了以下序列：

```cpp
#include <vector>
#include <iostream>
#include <deque>
#include <list>
using namespace std;
int main()
{
deque<int> mydeck;list<int> mylist; vector<int> myvector;
stack<int> first;
stack<int> second(mydeck);
stack<int> third(second);
stack<int, list<int>> fourth(mylist);
fourth.push(10);fourth.push(11);fourth.push(12);
stack<int, vector<int>> fifth(myvector);
fifth.push(10);fifth.push(11);fifth.push(12);
while(!fifth.empty())
{
cout<<fifth.top()";
fifth.pop();
}
while (!fourth.empty())
{
cout << fourth.front() << " ";
fourth.pop();
}
return 0;
}
```

答案：D

解释：

### 题编号：138
哪些是 `priority_queue` 对象的有效实例化：

```cpp
#include <iostream>
#include <deque>
#include <list>
#include <queue>
#include <vector>
using namespace std;
```

`priority_queue<int, deque<int>> first;//行 I`

`priority_queue<int, list<int>> second;//行 II`

`priority_queue<int> third(first);//行 III`

`priority_queue<int, vector<int>> fourth(third);//行 IV`

`priority_queue<int> fifth(myvector.begin(),myvector.end());//行 V`

A. 行 I
B. 行 II
C. 行 III
D. 行 IV

答案：D

解释：



```cpp
#include <iostream>
#include <set>

#include <vector>

using namespace std;
int main(){
    int myints[]= { 3, 4, 2, 1, 6, 5, 7, 9, 8, 0 };
    vector<int>v(myints,myints+10);
    set<int> s1(v.begin(),v.end());
    s1.insert(v.begin(),v.end());
    s1.erase(s1.lower_bound(2),s1.upper_bound(7));
    for(set<int>::iterator i=s1.begin();i!=s1.end(); i++) {
        cout<<*i<<" "
    }
    return 0;
}
```

A. 程序输出：0 0 1 1 8 8 9 9

B. 程序输出：2 3 4 5 6 7

C. 程序输出：1 6 5 7

D. 程序输出：3 4 9 8 0

答案：A

解释：

题编号： 139

当你尝试编译并运行以下代码时会发生什么，假设你输入了以下序列：1 2 3 4 quit<enter>?

```cpp
#include <iostream>
#include <string>
#include <list>
#include <algorithm>

using namespace std;
template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o){}
void operator()(const T & val ) { out<<val<<" "; } };

int main ()
{
list<string> l;
while(cin.good())
{
string s;
cin>>s;
if (s == "quit") break;
l.push_back(s);
}
}
```

```cpp
}
for_each(l.begin(), l.end(), Out<string>(cout));
return 0;
}
```

程序将输出：

- A. 1 2 3 4

- B. 1 2 3 4 quit

- C. 1

- D. 程序无限运行无输出

答案：A

解释：

# 题目编号： 140

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <set>
using namespace std;

void myfunction(int i) {
  cout << " " << i;
}
int multiply(int a) {
  return a*2;
}
```

```cpp
int main() {
  int t[] = { 10, 5, 9, 6, 2, 4, 7, 8, 3, 1 };
  vector<int> v1(t, t+10);
  set<int> s1(t, t+10);
  transform(s1.begin(), s1.end(), v1.begin(), multiply);
  transform(v1.begin(), v1.end(), s1.begin(), multiply);
  for_each(s1.begin(), s1.end(), myfunction);
  return 0;
}
```

程序输出：

- A. 20 10 18 12 4 8 14 16 6 2

- B. 2 4 6 8 10 12 14 16 18 20

- C. 4 8 12 16 20 24 28 32 36 40

- D. 编译错误

答案：D

解释：

# 题目编号： 141

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <functional>
using namespace std;
template<class T>struct Out {
  ostream & out;
  Out(ostream & o) : out(o){}
  void operator()(const T & val ) { out<<val<<""; }
 }

int main() {
  int t[]={3,2,4,1,5,6,10,8,7,9};
  vector<int> v1(t, t+10);
  for_each(v1.begin(), v1.end(), bind1(plus<int>(), 1));
  for_each(v1.rbegin(), v1.rend(), Out<int>(cout));cout<<endl;
  return 0;
}
```

程序输出：

- A. 3 2 4 1 5 6 1 0 8 7 9

- B. 4 3 5 2 6 7 11 9 8 10

- C. 9 7 8 10 6 5 1 4 2 3

- D. 10 8 9 11 7 6 2 5 3 4

- E. 编译错误

答案：C

解释：

# 题目编号： 142

当你尝试编译并运行以下代码时会发生什么？选择所有可能的答案。

```cpp
#include <iostream>

using namespace std;

class B {};

template <typename T>
class A {
  T _v;
public:
  A() {}
  A(T v) : _v(v){}
  T getV() { return _v; }
  void add(T a) { _v+=a; }
};
```

```cpp
int main()
{
  A<int> a(1);
  A<B>b;
  a.add(10);
  cout << a.getV() << endl;
  return 0;
}
```

- A. 程序显示：11

- B. 程序无法编译

- C. 程序可以编译

- D. 程序运行时异常

答案：A,C

解释：

# 题目编号： 143

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <deque>
#include <vector>
#include <iostream>
using namespace std;

class A
{
  int a;
public:
  A(int a) {this->a = a;}
  ~A() {c--;}
  static int c;
};
int A::c(0);
int main ()
{
  A t[] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
  vector<A>v1(t, t+10);
  deque<A>d1(v1.begin(), v1.end());
  deque<A> d2;
  d2 = d1;
  cout<<A::c<< endl;
  return 0;
}
```

创建了多少个 A 对象？

- A. 10

- B. 20

- C. 30

- D. 40

答案：D

解释：

# 题目编号： 144

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
using namespace std;
int main()
{
  cout.setf(ios::hex, ios::base);
  cout<<100<< " ";
  cout.setf(ios::showbase);
  cout<<100<< " ";
  return 0;
}
```

程序输出：

- A. 64 21

- B. 64 21 0x64

- C. 0x64 21 0x64

- D. 100 33

- E. 编译错误

答案：D

解释：

# 题目编号： 145

当你尝试编译并运行以下代码时会发生什么？



```cpp
#include <list>
#include <deque>
#include <iostream>
using namespace std;
template<class T>
void print(T start, T end) {
  while (start != end) {
    std::cout << *start << " "; start++;
  }
}

int main() {
  int t1[] = { 1, 7, 8, 4, 5 };
  list<int> l1(t1, t1 + 5);
  int t2[] = { 3, 2, 6, 9, 0 };
  deque<int> d1(t2, t2 + 5);

  l1.sort();
  d1.sort();
  l1.merge(d1);
  print(l1.begin(), l1.end());
  print(d1.begin(), d1.end()); cout<<endl;
  return 0;
}
```

- A. 程序输出：0 1 2 3 4 5 6 7 8 9 0 2 3 6 9
- B. 程序输出：0 1 2 3 4 5 6 7 8 9
- C. 程序输出：9 8 7 6 5 4 3 2 1
- D. 编译错误

答案：D

解释：

# 题目编号：146

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
using namespace std;
int main()
{
  cout.setf(ios::hex, ios::base);
  cout<<100<< " ";
  cout.unsetf(ios::hex);
  cout<<100<< " ";
  return 0;
}
```

程序输出：

- A. 64 64
- B. 100 0x64
- C. 0x64 0x64
- D. 64 100
- E. 编译错误

答案：D

解释：

# 题目编号：147

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <deque>
#include <set>
using namespace std;
class A {
  int a;
public:
  A(int a):a(a) {
  int getA() const { return a; } 
  void setA(int a) { a = a; }
  bool operator < const A &b ) const { return a<b; }
};
struct display { 
  void operator()(const A & a) { cout << " " << a.getA(); } 
};
struct add{
  void operator()( A & a) { a.setA(a.getA()+10); };
};

int main() {
  A t[] = { 10, 5, 9, 6, 2, 4, 7, 8, 3, 1 };
  vector<A> v1(t, t+10);
  set<A> s1(t, t+10);
  for_each(v1.begin(), v1.end(), add());
  for_each(s1.begin(), s1.end(), display());
  return 0;
}
```

- A. 程序输出：10 5 9 6 2 4 7 8 1 2 3 4 5 6 7 8 9
- B. 程序输出：20 15 19 16 12 14 17 18 13 11 2 3 4 5 6 7 8 9
- C. 程序输出：20 15 19 16 12 14 17 18 13 11 2 3 4 5 6 7 8 9 20
- D. 编译错误

答案：D

解释：

# 题目编号：148

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <functional>
using namespace std;
class B { 
  int val;
public:
  B(int v=0):val(v){}
  int getV() const { return val; }
  operator +(const B& b) const { return B(val+b.val); }
};
template<class T>struct Out {
  ostream & out;
  Out(ostream& o){}
  void operator()(const T& val) { out<<val<<" } }
 Add : public binary_function<B, B, B> {
  B operator () (const B& a, const B& b) const { return a+b; }
};

int main() {
  B t[]={1,2,3,4,5,6,7,8,9,10};
  vector<B> v1(t, t+10);
  vector<B> v2(10);
  transform(v1.begin(), v1.end(), v2.begin(), bind(Add(), 1));
  for_each(v2.rbegin(), v2.rend(), Out<B>(cout));cout<<endl;
  return 0;
}
```

程序输出：

- A. 1 2 3 4 5 6 7 8 9 10
- B. 2 3 4 5 6 7 8 9 10 11
- C. 10 9 8 7 6 5 4 3 2 1
- D. 11 10 9 8 7 6 5 4 3 2
- E. 编译错误

答案：D

解释：

# 题目编号：149

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
template<class T>struct Out {
  ostream & out;
  Out(ostream & o): out(o){
  void operator<<(const T & val) {
    out<<val<<" ";
  }
};
struct Sequence {
  int start;
  Sequence(int start):start(start){}
  int operator()() { return start++; }
};
struct Odd { bool operator()(int v) { return v%2==0; };
int main() {
  vector<int> v1(10);
  generate(v1.begin(), v1.end(), Sequence(1));
  partition(v1.begin(), v1.end(), Odd());
  for_each(v1.begin(), v1.end(), Out<int>(cout));cout<<endl;
  return 0;
}
```

选择所有可能的输出：

- A. 1 2 3 4 5 6 7 8 9 10
- B. 5 7 3 9 1 10 2 8 4 6
- C. 10 2 8 4 6 5 7 3 9 1
- D. 4 6 8 10 2 7 5 3 1 9
- E. 2 4 6 8 10 1 3 5 7 9

答案：C,D,E

解释：

# 题目编号：150

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <functional>
using namespace std;
class B { 
  int val;
public:
  B(int v=0):val(v){
  int getV() const { return val;}
  B operator?(const B &b)const { return B(val ? b.val); }
};
```



```cpp
ostream & operator <<(ostream & out, const B & v) { out<<v.getV(); return out; }

template<class T>struct Out {
  ostream & o; out(o){}
  void operator()(const T &val) { out<<val<<" "; };
 }
int main() {
  B t1[]={1,2,3,4,5,6,7,8,9,10};
  B t2[]={1,2,3,4,5,6,7,8,9,10};
  vector<B> v1(t1, t1+10);
  vector<B> v2(t2, t2+10);
  vector<B> v3(10);
  transform(v1.begin(), v1.end(), v2.rbegin(), v3.begin(), minus<B>());
  for_each(v3.rbegin(), v3.rend(), Out<B>(cout));cout<<endl;
  return 0;
}
```

程序输出：

- A. 9 7 5 3 1 ?1 ?3 ?5 ?7 ?9
- B. ?1 ?3 ?5 ?7 ?9 7 5 3 1
- C. 1 3 5 7 9 ?1 ?3 ?5 ?7 ?9
- D. 1 3 5 7 9 ?1 ?3 ?5 ?7 ?9
- E. ?9 ?7 ?5 ?3 ?1 1 3 5 7

答案：A

解释：

## 题目编号：151

当你尝试编译并运行以下代码时会发生什么？

#include <iostream>

```cpp
#include <algorithm>
#include <vector>
#include <set>
using namespace std;
```

```cpp
void myfunction(int i) { cout << " " << i; }
struct sequence {
    int val, inc;
    sequence(int s, int val) : val(s), inc(val) {}
    int operator()() {
        int r = val; val += inc;
        return r;
    }
};
int main() {
    vector<int> v1(10);
    fill(v1.begin(), v1.end(), sequence(1,1));
    for_each(v1.begin(), v1.end(), myfunction);
    return 0;
}
```

程序输出：

- A. 1 2 3 4 5 6 7 8 9 10
- B. 10
- C. 0 000000000
- D. 编译错误

答案：D

解析：

## 题目编号: 152

当你尝试编译并运行以下代码时，会发生什么：

```cpp
#include <iostream>
#include <algorithm>
#include <set>
using namespace std;
struct Even {
    bool operator ()(int a) {
        return (a % 2)==0?true:false;
    }
};
```

```cpp
int main () {
    int t[] = {1,2,3,2,3,5,1,2,7,3,2,10, 4,4,5};
    set<int> s(t,t+15);
    int number = count_if(s.begin(), s.end(), Even());
    cout<< number<<endl;
    return 0;
}
```

程序输出：

- A. 4
- B. 3
- C. 7
- D. 8
- E. 编译错误

答案：B

解析：

## 题目编号: 153

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <vector>
#include <set>
#include <deque>
#include <iostream>
#include <algorithm>

using namespace std;

template<class T>struct Out {
    ostream &out;
    Out(ostream & o): out(o){}
    void operator()(const T & val ) const {
        out<<val<<" ";
    }
};
struct Sequence {
    int start;
    Sequence(int start):start(start){}
    int operator()() {
        return start++;
    }
};
```

```cpp
int main() {
    vector<int> v1(5);
    generate(v1.begin(), v1.end(), Sequence(1));
    set<int> s1(v1.rbegin(), v1.rend());
    deque<int> d1(s1.rbegin(), s1.rend());
    reverse(v1.begin(), v1.end());
    reverse(s1.begin(), s1.end());
    reverse(d1.begin(), d1.end());
    for_each(v1.begin(), v1.end(), Out<int>(cout));
    for_each(s1.begin(), s1.end(), Out<int>(cout));
    for_each(d1.begin(), d1.end(), Out<int>(cout));cout<<endl;
    return 0;
}
```

程序输出：

- A. 5 4 3 2 1 2 3 4 5 1 2 3 4 5
- B. 1 2 3 4 5 1 2 3 4 5 5 4 3 2 1
- C. 无输出
- D. 1 2 3 4 5 4 3 2 1
- E. 编译错误

答案：E

解析：

## 题目编号: 154

当你尝试编译并运行以下代码时，会发生什么：

```cpp
#include <vector>
#include <set>
#include <iostream>
#include <algorithm>
using namespace std;
template<class T>struct Out {
    ostream & out;
    Out(ostream & o) : out(o){}
    void operator()(const T & val) { out<<val<<" "; }
};
bool Greater(int v1, int v2) { return v1<v2; }
int main() {
    int t[]={8, 10, 5, 1, 4, 6, 2, 7, 9, 3};
    vector<int> v1(t, t+10);
    sort(v1.begin(), v1.end(), Greater);
    for_each(v1.begin(), v1.end(), Out<int>(cout));
    return 0;
}
```

程序输出：

- A. 8 10 5 1 4 6 2 7 9 3
- B. 1 2 3 4 5 6 7 8 9 10
- C. 编译错误
- D. 10 9 8 7 6 5 4 3 2

答案：B

解析：

## 题目编号: 155

当你尝试编译并运行以下代码时，会发生什么？



```cpp
#include <iostream>
#include <map>
#include <string>

using namespace std;
int main() {
    int second[] = { 3, 4, 2, 1, 6, 5, 7, 9, 8, 10 };
    string first[] = {"three", "four", "two", "one", "six", "five", "seven", "nine", "eight", "ten"};
    map<int,string> m;
    for(int i=0; i<10; i++) {
        m.insert(pair<int,string>(second[i],first[i]));
    }
    if (m[1] ="eleven") {
        cout<<"eleven";
    }
    for(map<int,string>::iterator i=m.begin();i!=m.end(); i++) {
        cout<<i->first<<"<<i->second<<" ";
    }
    cout<<m.size();
    return 0;
}
```

程序输出：

- A. 输出 one two three four five six seven ten 1

- B. 输出 one two three four five six seven ten 10

- C. 输出 one two three four five six seven ten 10

- D. 输出 eleven one two three four five six seven ten 10

- E. 运行时异常

答案：A

解析：

题目编号: 156

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <set>
#include <vector>
using namespace std;
int main(){
    int t[]={ 3, 4, 2, 1, 6, 5, 7, 9, 8, 0 };
    vector<int>v(t, t+10);
    multiset<int> s1(v.begin(),v.end());
    multiset<int, greater<int>> s2(v.begin(), v.end());
    for(multiset<int, greater<int>>::iterator i=s2.begin();i!=s2.end(); i++) {
        cout<<*i<<" ";
    }
    for(multiset<int>::iterator j=s1.begin();j!=s1.end(); j++) {
        cout<<*j<<" ";
    }
    cout<<endl;
    return 0;
}
```

输出将：

- A. 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9

- B. 9 8 7 6 5 4 3 2 1 0 9 8 7 6 5 4 3 2 1

- C. 0 1 2 3 4 5 6 7 8 9 9 8 7 6 5 4 3 2 1 0

- D. 9 8 7 6 5 4 3 2 1 0 0 1 2 3 4 5 6 7 8 9

答案：D

解析：

题目编号: 157

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
int main () {
    int t[] = {1,2,3,3,5,1,2,4,5};
    vector<int> v (t,t+10);
    vector<int>::iterator it = v.begin();
    while ( it = adjacent_find(it, v.end())) != v.end()) {
        cout<<v.begin();
        it++;
    }
    cout<< endl;
    return 0;
}
```

程序输出：

- A. 输出: 2 3

- B. 输出: 2 7

- C. 输出: 3 8

- D. 编译错误

- E. 程序死循环

答案：B

解析：

题目编号: 158

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <deque>
#include <vector>
#include <iostream>
using namespace std;
int main ()
{
    int t[] = {1, 2 ,3,4,5};
    vector<int>v1(t, t+5);
    deque<int>d1;
    d1.assign(v1.end(), v1.begin());
    for(int i=0; i<d1.size(); i++) {
        cout<<d1.at(i) << ";
    }
    cout<<endl;
    return 0;
}
```

程序输出：

- A. 输出 5 4 3 2 1

- B. 输出 1 2 3 4 5

- C. 第8行编译错误

- D. 第10行编译错误

- E. 段错误运行时异常

答案：E

解析：

题目编号: 159

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <iomanip>

using namespace std;
int main ()
{
    float f = 10.126;
    cout<<showpoint<<f<<setprecision(2)<<endl;
    return 0;
}
```

程序输出：

- A. 10.13

- B. 10.12

- C. 10.126

- D. 10.13

答案：C

解析：

题目编号: 160

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <iomanip>
#include <string>
using namespace std;
int main()
{
    float f1 = 10.126;
    float f2 = 10.0;
    cout<<showpoint<<f1<<fixed<<setprecision(2)<<f2;
    return 0;
}
```

程序输出：

- A. 10.13 10.0

- B. 10.12 10.0

- C. 10.126 10

- D. 10.13 10

答案：D

解析：

题目编号: 161

哪些更改允许代码编译并显示：

```cpp
#include <iostream>
#include <set>
#include <vector>

using namespace std;
class A {
    int a;
public:
    A(int a):a(a){}
    int getA() const { return a; }
    /* 插入代码 1 */
};

int main(){
    int t[]={ 3, 4, 2, 1, 6, 5, 7, 9, 8, 0 };
    vector<A>v(t, t+10);
    set<A> s1(v.begin(),v.end());
    s1.insert(v.begin(),v.end());
    s1.erase(s1.lower_bound(2),s1.upper_bound(7));
    /* 插入代码 2 */
    for(set<A>::iterator i=s1.begin();i!=s1.end(); i++) {
        cout<<i->getA() << " ";
    }
    cout<<endl;
    return 0;
}
```

- A. 在位置1处插入 `operator int() const { return a; }`

- B. 在位置1处插入 `bool operator < (const A & b) const { return a<b; }`

- C. 在位置1处插入 `bool operator < (const A & b) const { return b.a; }`

- D. 在位置2处插入 `bool operator < (const A & a, const A & b) { return a.getA()<b.getA(); }`

答案：A,B,D

解析：

题目编号: 162

当你尝试编译并运行以下代码时，会发生什么？



```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
void myfunction(int i) { cout << " " << i; }
int main() {
    int t[] = { 10, 5, 9, 6, 2, 4, 7, 8, 3, 1 };
    vector<int> v1(t, t + 10);
    copy(t, t+10, v1.end());
    for_each(v1.begin(), v1.end(), myfunction());
    return 0;
}
```

- A. 10 5 9 6 2 4 7 8 3 1
- B. 10 5 9 6 2 4 7 8 3 1 10 5 9 6 2 4 7 8 3 1
- C. 编译错误
- D. 运行时异常/段错误

答案：D

解析：

题目编号: 163

当你尝试编译并运行以下代码时，会发生什么：

```cpp
#include <deque>
#include <iostream>
#include <algorithm>
using namespace std;
template<class T>struct Out {
```

```cpp
template<class T>
struct Out {
    ostream & out;
    Out(ostream & o) : out(o) {}
    void operator()(const T & val) { out << val << " "; }
};

int main() {
    int t[] = {8, 10, 5, 1, 4, 6, 7, 9, 3};
    deque<int> d1(t, t + 10);
    sort(d1.begin(), d1.end());
    deque<int>::iterator it = upper_bound(d1.begin(), d1.end(), 4);
    for_each(it, d1.end(), Out<int>(cout));
    cout << endl;
    return 0;
}
```

程序输出：

- A. 5 6 7 8 9 10
- B. 4 5 6 7 8 9 10
- C. 1 2 3 4 5 6 7 8 9 10
- D. 1 2 3 4 5
- E. 1 2 3 4

答案：A

解释：

## 题编号：164

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

class B {
    int val;
public:
    B(int v) : val(v) {}
    int getV() const { return val; }
    bool operator < (const B & v) const { return val < v.val; }
};

template<class T>
struct Out {
    ostream & out;
    Out(ostream & o) : out(o) {}
    void operator()(const T & val) { out << val << " "; }
};

int main() {
    B t1[] = {3, 2, 4, 1, 5};
    B t2[] = {5, 6, 8, 2, 1};
    vector<B> v1(10, 0);
    sort(t1, t1 + 5);
    sort(t2, t2 + 5);
    set_difference(t1, t1 + 5, t2, t2 + 5, v1.begin());
    for_each(v1.begin(), v1.end(), Out<B>(cout));
    cout << endl;
    return 0;
}
```

程序输出：

- A. 1 2 3 4 5 6 8 0 0 0
- B. 3 4 0 0 0 0 0 0 0
- C. 6 8 0 0 0 0 0 0 0
- D. 编译错误
- E. 1 2 5 0 0 0 0 0 0

答案：D

解释：

## 题编号：165

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

template<typename T>
class B {
    T val;
public:
    B(T v) : val(v) {}
    T getV() const { return val; }
    bool operator < (const B & v) const { return val < v.val; }
};

template<class T>
ostream & operator <<(ostream & out, const B<T> & v) {
    out << v.getV();
    return out;
}

template<class T>
struct Out {
    ostream & out;
    Out(ostream & o) : out(o) {}
    void operator()(const T & val) { out << val << " "; }
};

bool Less(const B<float> &a, const B<float> &b) { 
    return int(a.getV()) < int(b.getV()); 
}

int main() {
    float t[] = {2.28, 1.66, 1.32, 3.94, 3.64, 2.3, 2.98, 1.96, 2.62, 1.13};
    vector<B<float>> v1;
    v1.assign(t, t + 10);
    stable_sort(v1.begin(), v1.end(), Less);
    for_each(v1.begin(), v1.end(), Out<B<float>>(cout));
    cout << endl;
    return 0;
}
```

程序输出：

- A. 1.66 1.32 1.96 1.13 2.28 2.3 2.98 2.62 3.64 3.94
- B. 1.66 1.32 1.96 1.13 2.28 2.3 2.98 2.62 3.64 3.94
- C. 1.66 1.32 1.96 1.13 2.28 2.3 2.98 2.62 3.64 3.94
- D. 1.66 1.32 1.96 1.13 2.28 2.3 2.98 2.62 3.64 3.94
- E. 1.66 1.32 1.96 1.13 2.28 2.3 2.98 2.62 3.64 3.94

*(注：由于原文提供的选项内容存在重复或不完整，此处按逻辑翻译，实际输出结果取决于 `stable_sort` 对整数转换后值的稳定性处理)*

*(修正：原文提供的选项文本较为杂乱，此处根据题意翻译逻辑)*

答案：A (注：原文选项内容存在异常，此处以逻辑为准)

解释：

程序输出：

A. 9 12 12 8 14
B. 14 8 12 12 9
C. 3 2 4 1 5 6 10 8 7 9
D. 1 2 3 4 5 6 7 8 9 10
E. 编译错误

答案：E

解释：

# 题目编号：173

当你尝试编译并运行以下代码时，程序的输出是什么？

```cpp
#include <iostream>
#include <map>
#include <vector>
#include <string>
using namespace std;
int main(){
int second[] = { 3, 4, 2, 1, 6, 5, 7, 9, 8, 0 };
string first[] = {"three", "four", "two", "one", "six", "five", "seven", "nine", "eight", "zero"};
multimap<int,string> m;
```



```cpp
for(int i=0; i<10; i++) {
    m.insert(pair<int,string>(second[i],first[i]));
}
m[0]="ten";
m.insert(pair<int,string>(1,"eleven"));
for(multimap<int,string>::iterator i=m.begin();i!=m.end(); i++) {
    cout<<i?"second<<" ";
}
return 0;
}
```

- A. zero one two three four five six seven eight nine
- B. ten one two three four five six seven eight nine
- C. zero eleven two three four five six seven eight nine
- D. ten eleven two three four five six seven eight nine
- E. 编译错误

答案：E

解释：

## 题目编号：174

当你尝试编译并运行以下代码时，会发生什么：

```cpp
#include <iostream>
using namespace std;
```

```cpp
template<class A>
void f(A &a)
{
  cout<<1<<endl;
}
```

```cpp
void f(int &a)
{
  cout<<2<<endl;
}
```

```cpp
int main()
{
  int a = 1;
  f(a);
  return 0;
}
```

- A. 程序显示：1
- B. 程序显示：2
- C. 编译错误
- D. 运行时异常

答案：B

解释：

## 题目编号：175

当你尝试编译并运行以下代码时，会发生什么：

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
int main () {
int t[] = {1,2,3,4,5,1,2,3,4,5};
vector<int> v (t,t+10);
vector<int>::iterator it;
int m1[] = {1, 3, 2};
it = find_first_of (v.begin(), v.end(), m1+3);
cout << "First found at position: " << it?v.begin() << endl;
return 0;
}
```

- A. 程序输出：First found at position: 5
- B. 程序输出：First found at position: 0
- C. 程序输出：First found at position: 6
- D. 程序输出：First found at position: 1
- E. 程序输出：First found at position: 10

答案：B

解释：

## 题目编号：176

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <map>
using namespace std;
int main() {
int t[] = { 1, 1, 2, 2, 3, 3, 4, 4, 5, 5 };
string s[] = { "one", "one", "two", "two", "three", "three", "four", "four", "five", "five" };
multimap<int, string> m;
for (int i = 0; i < 10; i++) {
m.push_back(pair<int, string>(t[i], s[i]));
}
for (multimap<int, string>::iterator i = m.begin(); i != m.end(); i++) {
cout << i->first << " " << i->second << "";
}
return 0;
}
```

- A. 程序输出：1 2 3 4 5
- B. 编译错误
- C. 程序输出：1 2 3 4 5
- D. 程序输出：one two three
- E. 程序输出：one two three five

答案：B

解释：

## 题目编号：177

当你尝试编译并运行以下代码时会发生什么？（多选）

```cpp
#include <deque>
#include <vector>
#include <iostream>
using namespace std;
class A
{
    int a;
public:
    A(int a) {this->a = a; }
    A(const A & a) {this->a = a; }
    ~A() { }
    static int c;
};
int A::c(0);
int main ()
{
A* t[] = {new A(1), new A(2), new A(3), new A(4), new A(5)};
vector<A*> v1(t, t+5);
deque<A*> d1(v1.begin(), v1.end());
d1.clear();
v1.clear();
cout<<A::c<< endl;
return 0;
}
```

- A. 创建了 15 个 A
- B. 创建了 5 个 A
- C. 所有对象都调用了析构函数
- D. 程序显示 5

答案：B,D

解释：

## 题目编号：178

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <list>
#include <iostream>
using namespace std;
template<class T>
void print(T start, T end) {
while (start != end) {
    std::cout << *start << " ";
    start++;
}
}
int main()
{
int t1[] = { 1, 2, 3, 4, 5};
list<int> l1(t1, t1 + 5);
l1.remove(2);
print(l1.begin(), l1.end()); cout<<endl;
return 0;
}
```

- A. 程序输出：1 2 4 5
- B. 程序输出：3 4 5
- C. 程序输出：1 3 4 5
- D. 程序输出：4 5

答案：C

解释：

## 题目编号：179

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <functional>
using namespace std;
class B { int val;
public:
B(int v=0):val(v){}
int getV() const { return val; }
operator int () const { return val; }
ostream & operator<<(ostream & out, const B & v) { out<<v.getV(); return out; }
template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o)
void operator()(const T & val ) { out<<val<<" "; }; }
int main() {
B t[]={3,2,4,1,5,6,10,8,7,9};
vector<B> v1(t, t+10);
transform(v1.begin(), v1.end(), v1.begin(), bind2nd(plus<B>(), 1));
for_each(v1.rbegin(), v1.rend(), Out<B>(cout));cout<<endl;
return 0;
}
```

程序输出：

- A. 3 2 4 1 5 6 10 8 9
- B. 4 3 5 2 6 7 11 9 10
- C. 9 7 8 10 6 5 1 4 2 3
- D. 10 8 9 11 7 6 2 5 3 4
- E. 编译错误

答案：D

解释：

## 题目编号：180

当你尝试编译并运行以下代码时会发生什么？



```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <functional>
using namespace std;
template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o);
void operator() (const T & & val) { out<<" "<<val<<" "; }; }
struct Add {
int operator()(int a, int b) {
return a+b;
}
};
int main() {
int t[]={1,2,3,4,5,6,7,8,9,10};
vector<int> v1(t, t+10);
vector<int> v2(10);
transform(v1.begin(), v1.end(), v2.begin(), bind2nd(Add<int>(), 1));
for_each(v2.rbegin(), v2.rend(), Out<int>(cout));
```

程序输出：

- A. 1 2 3 4 5 6 7 8 9 10
- B. 2 3 4 5 6 7 8 9 10 11
- C. 10 9 8 7 6 5 4 3 2 1
- D. 11 10 9 8 7 6 5 4 3 2
- E. 编译错误

答案：E
解释：

# 题目编号：181

当你尝试编译并运行以下代码时会发生什么？

```cpp

#include <deque>

#include <iostream>

#include <algorithm>

#include <functional>

#include <set>

using namespace std;

class B { int val;

public:

B(int v=0):val(v){}

int getV() const { return val; }

};

set<B> s1;

int main() {

B t[]={8, 10, 5, 1, 4, 6, 2, 7, 9, 3};

deque<B> d1(t, t+10);

set<B> s1(t, t+10);

sort(d1.begin(), d1.end());

d1.clear();

s1.clear();

cout<<includes(d1.begin(),s1.end(), t1+4)"<<endl;

return 0;

}

```

程序输出：

- A. 1
- B. 0
- C. 1
- D. 0
- E. 编译错误

答案：A
解释：

# 题目编号：182

当你尝试编译并运行以下代码时会发生什么：

```cpp

#include <deque>

#include <iostream>

#include <algorithm>

#include <functional>

using namespace std;

class B { int val;

public:

B(int v=0):val(v)

int getV() const { return val; }

B operator+(const B &b) const { return B(val + b.val); } };

ostream &operator<<(ostream & out, const B & v) { out<<v.getV(); return out; }

template<class T>struct Out {

stream & out;

Out(ostream & o) : out(o){}

void operator()(const T & val) { out<<val<<" "; };nt A

template<typename A>

struct Add : public binary_function<A, A, A> {

A operator()(const A & a, const A & b) const { return a+b; } }

int main() {

int t[]={1,2,3,4,5,6,7,8,9,10};

deque<B> d1(t, t+10);

deque<B> d2(10);

transform(d1.begin(), d1.end(), d2.begin(), bind2nd(Add<B>(), 1));

for_each(d2.rbegin(), d2.rend(), Out<B>(cout));cout<<endl;

return 0;

}
```



程序输出：

A. 9 12 12 8 14
B. 14 8 12 12 9
C. 3 2 4 1 5 6 10 8 7 9
D. 1 2 3 4 5 6 7 8 9 10
E. 编译错误

答案：E

解释：

# 题目编号：173

当你尝试编译并运行以下代码时，程序的输出是什么？

```cpp
#include <iostream>
#include <map>
#include <vector>
#include <string>
using namespace std;
int main(){
int second[] = { 3, 4, 2, 1, 6, 5, 7, 9, 8, 0 };
string first[] = {"three", "four", "two", "one", "six", "five", "seven", "nine", "eight", "zero"};
multimap<int,string> m;
for(int i=0; i<10; i++) {
    m.insert(pair<int,string>(second[i],first[i]));
}
m[0]="ten";
m.insert(pair<int,string>(1,"eleven"));
for(multimap<int,string>::iterator i=m.begin();i!=m.end(); i++) {
    cout<<i?"second<<" ";
}
return 0;
}
```

- A. zero one two three four five six seven eight nine
- B. ten one two three four five six seven eight nine
- C. zero eleven two three four five six seven eight nine
- D. ten eleven two three four five six seven eight nine
- E. 编译错误

答案：E
解释：

# 题目编号：174

当你尝试编译并运行以下代码时，会发生什么：

```cpp
#include <iostream>
using namespace std;
template<class A>
void f(A &a)
{
  cout<<1<<endl;
}
void f(int &a)
{
  cout<<2<<endl;
}
int main()
{
  int a = 1;
  f(a);
  return 0;
}
```

- A. 程序显示：1
- B. 程序显示：2
- C. 编译错误
- D. 运行时异常

答案：B
解释：

# 题目编号：175

当你尝试编译并运行以下代码时，会发生什么：

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
int main () {
int t[] = {1,2,3,4,5,1,2,3,4,5};
vector<int> v (t,t+10);
vector<int>::iterator it;
int m1[] = {1, 3, 2};
it = find_first_of (v.begin(), v.end(), m1+3);
cout << "First found at position: " << it?v.begin() << endl;
return 0;
}
```

- A. 程序输出：First found at position: 5
- B. 程序输出：First found at position: 0
- C. 程序输出：First found at position: 6
- D. 程序输出：First found at position: 1
- E. 程序输出：First found at position: 10

答案：B

解释：

# 题目编号：176

当你尝试编译并运行以下代码时，会发生什么？

```cpp
#include <iostream>
#include <map>
using namespace std;
int main() {
int t[] = { 1, 1, 2, 2, 3, 3, 4, 4, 5, 5 };
string s[] = { "one", "one", "two", "two", "three", "three", "four", "four", "five", "five" };
multimap<int, string> m;
for (int i = 0; i < 10; i++) {
m.push_back(pair<int, string>(t[i], s[i]));
}
for (multimap<int, string>::iterator i = m.begin(); i != m.end(); i++) {
cout << i->first << " " << i->second << "";
}
return 0;
}
```

- A. 程序输出：1 2 3 4 5
- B. 编译错误
- C. 程序输出：1 2 3 4 5
- D. 程序输出：one two three
- E. 程序输出：one two three five

答案：B
解释：

# 题目编号：177

当你尝试编译并运行以下代码时会发生什么？（多选）

```cpp
#include <deque>
#include <vector>
#include <iostream>
using namespace std;
class A
{
    int a;
public:
    A(int a) {this->a = a; }
    A(const A & a) {this->a = a; }
    ~A() { }
    static int c;
};
int A::c(0);
int main ()
{
A* t[] = {new A(1), new A(2), new A(3), new A(4), new A(5)};
vector<A*> v1(t, t+5);
deque<A*> d1(v1.begin(), v1.end());
d1.clear();
v1.clear();
cout<<A::c<< endl;
return 0;
}
```

- A. 创建了 15 个 A
- B. 创建了 5 个 A
- C. 所有对象都调用了析构函数
- D. 程序显示 5

答案：B,D
解释：

# 题目编号：178

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <list>
#include <iostream>
using namespace std;
template<class T>
void print(T start, T end) {
while (start != end) {
    std::cout << *start << " ";
    start++;
}
}
int main()
{
int t1[] = { 1, 2, 3, 4, 5};
list<int> l1(t1, t1 + 5);
l1.remove(2);
print(l1.begin(), l1.end()); cout<<endl;
return 0;
}
```

- A. 程序输出：1 2 4 5
- B. 程序输出：3 4 5
- C. 程序输出：1 3 4 5
- D. 程序输出：4 5

答案：C
解释：

# 题目编号：179

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <functional>
using namespace std;
class B { int val;
public:
B(int v=0):val(v){}
int getV() const { return val; }
operator int () const { return val; }
```



```cpp
ostream & operator<<(ostream & out, const B & v) { out<<v.getV(); return out; }

template<class T>struct Out {

ostream & out;

Out(ostream & o): out(o)

void operator()(const T & val ) { out<<val<<" "; }; }

int main() {

B t[]={3,2,4,1,5,6,10,8,7,9};

vector<B> v1(t, t+10);

transform(v1.begin(), v1.end(), v1.begin(), bind2nd(plus<B>(), 1));

for_each(v1.rbegin(), v1.rend(), Out<B>(cout));cout<<endl;

return 0;

}
```

程序输出：

- A. 3 2 4 1 5 6 10 8 9
- B. 4 3 5 2 6 7 11 9 10
- C. 9 7 8 10 6 5 1 4 2 3
- D. 10 8 9 11 7 6 2 5 3 4
- E. 编译错误

答案：D

解释：

# 题目编号：180

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <functional>
using namespace std;
template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o);
void operator() (const T & & val) { out<<" "<<val<<" "; }; }
struct Add {
int operator()(int a, int b) {
return a+b;
}
};
int main() {
int t[]={1,2,3,4,5,6,7,8,9,10};
vector<int> v1(t, t+10);
vector<int> v2(10);
transform(v1.begin(), v1.end(), v2.begin(), bind2nd(Add<int>(), 1));
for_each(v2.rbegin(), v2.rend(), Out<int>(cout));
```

程序输出：

- A. 1 2 3 4 5 6 7 8 9 10
- B. 2 3 4 5 6 7 8 9 10 11
- C. 10 9 8 7 6 5 4 3 2 1
- D. 11 10 9 8 7 6 5 4 3 2
- E. 编译错误

答案：E

解释：

# 题目编号：181

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <deque>
#include <iostream>
#include <algorithm>
#include <functional>
#include <set>
using namespace std;
class B { int val;
public:
B(int v=0):val(v){}
int getV() const { return val; }
};
set<B> s1;
int main() {
B t[]={8, 10, 5, 1, 4, 6, 2, 7, 9, 3};
deque<B> d1(t, t+10);
set<B> s1(t, t+10);
sort(d1.begin(), d1.end());
d1.clear();
s1.clear();
cout<<includes(d1.begin(),s1.end(), t1+4)"<<endl;
return 0;
}
```

程序输出：

- A. 1
- B. 0
- C. 1
- D. 0
- E. 编译错误

答案：A

解释：

# 题目编号：182

当你尝试编译并运行以下代码时会发生什么：

```cpp
#include <deque>
#include <iostream>
#include <algorithm>
#include <functional>
using namespace std;
class B { int val;
public:
B(int v=0):val(v)
int getV() const { return val; }
B operator+(const B &b) const { return B(val + b.val); } };
ostream &operator<<(ostream & out, const B & v) { out<<v.getV(); return out; }
template<class T>struct Out {
stream & out;
Out(ostream & o) : out(o){}
void operator()(const T & val) { out<<val<<" "; };nt A
template<typename A>
struct Add : public binary_function<A, A, A> {
A operator()(const A & a, const A & b) const { return a+b; } }
int main() {
int t[]={1,2,3,4,5,6,7,8,9,10};
deque<B> d1(t, t+10);
deque<B> d2(10);
transform(d1.begin(), d1.end(), d2.begin(), bind2nd(Add<B>(), 1));
for_each(d2.rbegin(), d2.rend(), Out<B>(cout));cout<<endl;
return 0;
}
```

E. 编译错误

答案：D

解释：

### 题目编号：183

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
class A {
public:
virtual int f() { return 10; }
virtual ~A(){
};
class B: public A {
int f() { return 11; }
virtual ~B(){
};
int main ()(){
  std::vector<A*>v1;
  for(int i = 10; i>0; i--)
  {
    i%2>0?v1.push_back(new A()):v1.push_back(new B());
  }
  std::vector<A>::iterator it = v1.begin();
  while(it != v1.end())
  {
    std::cout<<v1.back()->f()<";
    v1.pop_back();++it;
  }
  return 0;
}
```

- A. 类 A 的析构函数会被调用
- B. 类 B 的析构函数会被调用
- C. 代码无法编译
- D. 程序输出 10 11 10 11 10
- E. 程序输出 10 11 10 11 10 11 10 11 10 11

答案：D

解释：

### 题目编号：184

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <map>
using namespace std;
int main() {
  int t[] = { 1, 1, 2, 2, 3, 4, 4, 5, 5 };
  string s[] = { "one", "one", "two", "two", "three", "three", "four", "four", "five", "five" };
  map<int,string> m;
  for (int i = 0; i < 10; i++) {
    m.insert(pair<int,string>(t[i], s[i]));
  }
  if (m.count(3) == 2) {
    m.erase(3);
  }
  for (map<int,string>::iterator i = m.begin(); i!=m.end(); i++) {
    cout << i<<" " << i->first << " ";
  }
  return 0;
}
```

- A. 程序输出: 1 2 3 4 5
- B. 程序输出: 1 2 4 5
- C. 程序输出: 1 1 2 3 4 4 5 5
- D. 程序输出: 1 1 2 3 3 4 4 5 5
- E. 程序输出: one two three four five

答案：A

解释：

### 题目编号：185

当你尝试编译并运行以下代码时会发生什么？



```cpp
#include <vector>
#include <iostream>
int main () {
  std::vector<int>v1;
  for(int i = 0; i<10; i++) {v1.push_back(i); }
  std::vector<int> v2(v1.begin()+2, v1.end()-2);
  std::vector<int>::iterator it = v2.begin();
  for ( ; it != v2.end(); it++) {std::cout<<it++<<it<<" " "; } std::cout<<std::endl;
  return 0;
}
```

- A. 编译错误

- B. 程序输出 0 1 2 3 4 5 6 7 8 9

- C. 程序输出 2 3 4 5 6

- D. 程序输出 2 4 6

答案：D

解释：

### 题目编号：186

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <deque>
#include <iostream>
#include <algorithm>
#include <functional>
using namespace std;
class B { int val;
public:
B(int v):val(v){}
int getV() const {return val; }
bool operator>(const B& v) const { return val; }
ostream & operator<<(ostream& out, const B& v) { out<<v; }

template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o){}
void operator()(const T & val) { out<<val<< " }
int main() {
  int t[]={8,10, 5, 1, 4, 6, 2, 7, 9, 3};
  deque<B> d1(t, t+10);
  sort(d1.begin(), d1.end(), greater<B>());
  deque<B>::iterator it = lower_bound(d1.begin(), d1.end(), 4,greater<B>());
  for_each(it, d1.end(), Out<int>(cout));cout<<endl;
  return 0;
}
```

程序输出：

- A. 4 3 2 1

- B. 3 2 1

- C. 5 4 3 2

- D. 编译错误

- E. 1 2 3 4

答案：A

解释：

### 题目编号：187

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
using namespace std;
class A {
int a;
public:
A():a(0) A(int a){this->a = a;}
void setA(int a) {this->a = a;}
int getA() {return a;}
};
ostream &operator<<(ostream & cout, const A & a) {
cout << a.getA();
return cout;
}
int main () {
  vector<A*>v(5, new A());
  v.push_back(new A(1));
  vector<A*>::iterator it;
  for(it = v.begin(); it != v.end(); it++) {
    cout<<it<<" ";
  }
  cout<<endl;
  return 0;
}
```

- A. 程序输出 0 0 0 0 1

- B. 程序输出 0 0 0 0

- C. 编译错误

- D. 程序输出 1 1 1 1 1

- E. 以上都不是

答案：E

### 题目编号：188

当你尝试编译并运行以下代码时会发生什么：

```cpp
#include <iostream>
#include <deque>
#include <list>
#include <queue>
#include <vector>
using namespace std;

int main() {
  deque<int> mydeck;list<int> mylist; vector<int> myvector;
  queue<int> first; queue<int> second(mydeck);
  queue<int> third(second); queue<int, list<int> > fourth(mylist);
  fourth.push(10);fourth.push(11);fourth.push(12);
  queue<int, vector<int> > fifth(myvector);
  fifth.push(10);fifth.push(11);fifth.push(12); // 行 I
  while(!fifth.empty()) {
    cout<<fifth.front()< ""; // 行 II
    fifth.pop(); // 行 III
  }
  while (!fourth.empty()) {
    cout << fourth.front() << " ""; // 行 IV
    fourth.pop();
  }
  return 0;
}
```

- A. 程序输出: 10 11 12 10 11 12

- B. 行 I 编译错误

- C. 行 II 编译错误

- D. 行 III 编译错误

- E. 行 IV 编译错误

答案：D

### 题目编号：189

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <deque>
#include <vector>
#include <iostream>
using namespace std;
int main () {
  int t[] = {1, 2 ,3 ,4,5, 6, 7, 8, 9, 10};
  vector<int>v1(t, t+10);
  deque<int>d1(t, t+10);
  d1.empty();
  v1.empty();
  if (v1.isEmpty()) {
  cout<<"I am empty";
  } else {
  cout<<"I am not empty";
  }
  cout<<v1.size<<" "<<d1.size<<endl;
  return 0;
}
```

- A. 程序输出: I am empty 0 0

- B. 程序输出: I am not empty 0 0

- C. 编译错误

- D. 程序输出: I am not empty 10 10

答案：C

### 题目编号：190

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o){ }
void operator()(const T & val) { out<<val<<""; }

struct Add {
int operator()(int a, int b) {
return a+b;
};
int main() {
  int t[]={1,2,3,4,5,6,7,8,9,10};
  vector<int> v1(t, t+10);
  vector<int> v2(10);
  sort(v1.begin(), v1.end(), Add());
  vector<int>::iterator it = lower_bound(v1.begin(), v1.end(), 4,Add());
  for_each(it, v1.end(), Out<int>(cout));cout<<endl;
  return 0;
}
```

程序输出：

- A. 1 2 3 4 5 6 7 8 9 10

- B. 2 3 4 5 6 7 8 9 10 11

- C. 10 9 8 7 6 5 4 3 2

- D. 11 10 9 8 7 6 5 4 3 2

```cpp
}
for (multimap<int, string>::iterator i = m.begin(); i != m.end(); i++) {
    cout << i->first << " ";
}
return 0;
}
```

A. 程序输出: 1 2 3 4 5

B. 程序输出: 1 2 4 5



C. 程序输出: 1 1 2 2 3 4 4 5 5

D. 程序输出: 1 1 2 2 4 4 5 5

E. 程序输出: one two three four five

答案: D

解释：

## 题目编号: 194

当你尝试编译并运行以下代码时，会发生什么情况？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <set>
using namespace std;

void myfunction(int i) {
cout << "" << i;
}

int main() {
  vector<int> v1(10,1);
  fill(v1.begin()+2, v1.end(), 2,2);
  fill_n(v1.begin()+4,2,3);
  for_each(v1.begin(),v1.end(),function);
  return 0;
}
```

程序输出：

- A. 1 1 2 2 3 2 2
- B. 1 1 2 2 2 2
- C. 编译错误
- D. 以上都不是

答案: A

解释：

## 题目编号: 195

当你尝试编译并运行以下代码时，会发生什么情况？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <set>
using namespace std;

void myfunction(int i) {
cout << " " << i;
}

int main() {
  int t[] = {10, 5, 9, 6, 2, 4, 7, 8, 3};
  set<int> s1(t,t+10);
  vector<int> v1(s1.rbegin(),s1.rend());
  swap(s1, v1);
  for_each(v1.begin(),v1.end(),myfunction);
  for_each(s1.begin(),s1.end(),myfunction);
  return 0;
}
```

程序输出：

- A. 10 9 8 7 6 5 4 3 2 2 3 4 5 6 7 8 9 10
- B. 编译错误
- C. 2 3 4 5 6 7 8 9 10
- D. 10 9 8 7 6 5 4 3 2

答案: B

解释：

## 题目编号: 196

当你尝试编译并运行以下代码时，会发生什么情况？

```cpp
#include <deque>
#include <iostream>
#include <algorithm>
#include <set>
using namespace std;
template<class T>struct Out {
    ostream & out; out(ostream & o): out(o){
    void operator()(const T & val ) { out<<val<<" " };
};
int main(){
    int t1[]={8, 10, 5, 1, 4, 6, 2, 7, 9, 3};
    int t2[]={1,2,3,4};
    deque<int> d1(t1,t+10);
    set<int> s1(t1,t+10);
    sort(d1.begin(),d1.end());
    out<<includes(s1.begin(),s1.end(), t1,t1+4)<<"includes(d1.begin(),d1.end(), t1,t1+4)"<<endl;
    return 0;
}
```

程序输出：

- A. 1 1
- B. 1 0
- C. 0 1
- D. 0 0

答案: A

解释：

## 题目编号: 197

当你尝试编译并运行以下代码时，会发生什么情况？

```cpp
#include <deque>
#include <vector>
#include <iostream>
using namespace std;

int main ()
{
    int t[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    vector<int> v1(t, t+10);
    deque<int> d1(t, t+10);
    vector<int>::iterator it1 = v1.begin();
    deque<int>::iterator it2 = d1.begin();
    d1.erase(it2+5);
    it2 = d1.begin();
    cout<<*(it2+5);
    v1.erase(it1+5);
    it1 = v1.begin();
    cout<<*(it1+5)<<endl;
}
```

- A. 程序输出: 7 7
- B. 程序输出: 6 6
- C. 编译错误
- D. 结果不可预测

答案: A

解释：

## 题目编号: 198

当你尝试编译并运行以下代码时，会发生什么情况？

```cpp
#include <iostream>
#include <set>
#include <vector>
using namespace std;

template<class T> void print(T start, T end) {
    while (start != end) {
        std::cout << *start << " ";
        start++;
    }
}
int main(){
    vector<int> v;
    set<int> s;
    for(int i=10; i>0; i--) {
        v.push_back(i);
        s.push_back(i);
    }
    print(v.begin(), v.end()); 
    print(s.begin(), s.end());
    cout<<endl;
    return 0;
}
```

输出将：

- A. 10 9 8 7 6 5 4 3 2 1 2 3 4 5 6 7 8 9 10
- B. 10 9 8 7 6 5 4 3 2 1
- C. 10 9 8 7 6 5 4 3 2 unpredictable 范围从 1 到 10
- D. 编译错误

答案: D

解释：

## 题目编号: 199

当你尝试编译并运行以下代码时，会发生什么情况？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <set>
using namespace std;

void myfunction(int i) {
cout << "" << i;
}
int main() {
    int t[] = { 1, 5, 2, 5, 2, 4, 4, 3, 3};
    vector<int> v1(t, t+10);
    set<int> s1(t, t+10);
    replace(v1.begin(), v1.end(), 1,10);
    replace(s1.begin(), s1.end(), 1,10);
    for_each(v1.begin(), v1.end(), myfunction);
    return 0;
}
```

程序输出：

- A. 10 5 2 5 2 4 4 3 3
- B. 1 10 2 5 2 4 4 3 10
- C. 编译错误
- D. 10 5 2 5 2 4 4 3 10

答案: C

解释：

## 题目编号: 200

当你尝试编译并运行以下代码时，会发生什么情况？



```cpp
#include <deque>
#include <iostream>
#include <algorithm>
#include <functional>
using namespace std;
template<class T>struct Out {
    ostream & out;
    Out(ostream & o): out(o){
    void operator() (const T & val) { out<<val<<" "; }
    }
};

struct Add : public binary_function<int, int, int> {
    int operator()(const int & a, const int & b) const {
        return a+b;
    }
};
int main() {
    int t[]={1,2,3,4,5,6,7,8,9,10};
    deque<int> d1(t, t+10);
    deque<int> d2(10);
    transform(d1.begin(), d1.end(), d2.begin(), bind(Add, 1));
    for_each(d2.rbegin(), d2.rend(), Out<int>(cout))cout<<endl;
    return 0;
}
```

程序输出：

- A. 1 2 3 4 5 6 7 8 9 10
- B. 2 3 4 5 6 7 8 9 10
- C. 10 9 8 7 6 5 4 3 2
- D. 11 10 9 8 7 6 5 4 2
- E. 编译错误

答案: D

解释：

题目编号: 201

当你尝试编译并运行以下代码时，会发生什么情况？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
template<class T>struct Out {
    ostream & out;
    Out(ostream & o): out(o){}
    void operator()(const T & val ) { out<<val<<" "; }
};
struct Sequence {
    int start;
    Sequence(int start):start(start){}
    int operator() { return 10+(start++); }
};
int main() {
    vector<int> v1(10);
    generate(v1.begin(),v1.end(), Sequence(0));
    unique(v1.begin(),v1.end());
    for_each(v1.begin(), v1.end(), Out<int>(cout))cout<<endl;
    return 0;
}
```

程序输出：

- A. 20 30 10 20 30 10 20
- B. 20 30 10
- C. 30 10 20
- D. 编译错误

答案: A

解释：

题目编号: 202

当你尝试编译并运行以下代码时，会发生什么情况？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <string>
using namespace std;
template<class T>struct Out {
    ostream & out;
    Out(ostream & o): out(o){}
    void operator()(const T & val) { out<<val<< "; }
};
int main() {
    string t[]={"aaa","aAa","aaA","bbb","Bbb","bbB"};
    vector<string> v1(t, t+8);
    sort(v1.begin(), v1.end());
    for_each(v1.begin(), v1.end(), Out<string>(cout))cout<<endl;
    return 0;
}
```

程序输出：

- A. aaa aAa aaA bbb Bbb bbB
- B. aAa aaA bbb Bbb bbB
- C. bbb Bbb bbB aaa aAa aaA
- D. aaa aAa aaA bbb Bbb bbB

答案: A

解释：

题目编号: 203

当你尝试编译并运行以下代码时，会发生什么情况？

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <set>
using namespace std;

int main() {
    int t[] = {1,2,3,2,3,5,1,2,7,3,2,1,10, 4,4,5};
    vector<int> v1(t, t + 15);
    set<int> s1(t, t + 15);

    pair<set<int>::iterator, vector<int>::iterator> resultSet = equal(s1.begin(), s1.end());
    cout<<resultSet.first<<""<<resultSet.second<<endl;
    return 0;
}
```

- A. 2 4
- B. 4 2
- C. 0 5
- D. 编译错误

答案: D

解释：

题目编号: 204

当你尝试编译并运行以下代码时，会发生什么情况？

```cpp
#include <deque>
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
class A {
    int a;
public:
    A(int a) : a(a) {}
    int getA() const { return a; } setA(int a) { this->a = a; }
    bool operator==(const A & b) { return a == b.a; }
};
struct Compare{
    bool operator()(const A & a, const A & b) {return a.getA()=b.getA();}
};

int main ()
{
    int t[] = {1,2,3,4,5,1,2,3,4,5};
    vector<A> v (t,t10);
    vector<A>::iterator it;
    A m1[] = {A(1), A(2), A(3)};
    it = find_end(v.begin(), v.end(), m1, m1+3, Compare());
    cout << <<Found at position: " << it?v.begin() << endl;
    return 0;
}
```

- A. 程序输出: 5
- B. 程序输出: 0
- C. 程序输出: 7
- D. 编译错误

答案: A

```cpp
int main() {
  int t[] = { 10, 5, 9, 6, 2, 4, 7, 8, 3, 1 };
  vector<int> v1(t, t+10);
  set<int> s1(t, t+10);
  deque<int> d1;
  d1.resize(s1.size());
  transform(s1.begin(), s1.end(), v1.begin(), d1.begin(), add);

  for_each(d1.begin(), d1.end(), myfunction);
  return 0;
}
```

程序输出：

A. 0 0 0 0 0 0 0 0
B. 11 7 12 10 7 10 14 16 12 11
C. 编译错误
D. 运行时异常
E. 20 10 18 12 4 8 14 16 6 2

答案： B

解释：

## 题号：206

当你尝试编译并运行以下代码时会发生什么？



```cpp
#include <deque>
#include <iostream>
#include <algorithm>
#include <set>
using namespace std;
template<class T>struct Out {
 ostream & out;
  Out(ostream & o):out(o){
  void operator() (const T & val) { out<<val<<"" "; }
  }
};
 int main() {
  char s[]={"qwerty"};
  char t1[]={"ert"};
  char t2[]={"ERT"};
  sort(s, s+6);
  cout<<includes(s,s+6, t1,t1+3)<<"" "<<includes(s,s+6, t2,t2+3)<<endl;
  return 0;
}
```

程序输出：

A. 0 0

B. 0 1

C. 1 0

D. 1 1

答案： C

解释：

## 题号：207

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <algorithm>
#include <deque>
using namespace std;
class A {
  int a;
public:
  A(int a) : a(a) { }
  int getA() const { return a; } void setA(int a) { this->a = a; }
}
struct Even {
  bool operator () (const A & a, const A &b) {
    return (a.getA() % 2)==b.getA() % 2;
  }
}
int main () {
  int t[] = {1,2,3,2,3,5,1,2,7,3,2,1,10,4,4,5};
  deque<int> d(t,t+15);
  deque<int>::iterator it = search_n(d.begin(), d.end(), 3, 2, Even());
  cout<< it?d.begin()<<endl;
  return 0;
}
```

程序输出：

A. 编译错误

B. 12

C. 3

D. 1

E. 15

答案： B

解释：

## 题号：208

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <map>
#include <vector>
#include <sstream>
#include <string>
using namespace std;
int main() {
  int t[] = { 3, 4, 2, 1, 6, 5, 7, 9, 8, 0 };
  vector<int> v(t, t + 10);
  map<int, string> m;
  for (vector<int>::iterator i = v.begin(); i != v.end(); i++) {
    stringstream s; s << *i << i << *i;
    m.insert(pair<int, string>(*i, s.str()));
  }
  pair<map<int, string>::iterator, map<int, string>::iterator> range;
  range = m.equal_range(6);
  for (map<int, string>::iterator i = range.first; i != range.second; i++) {
    cout << i->first << " " << i->second;
  }
  return 0;
}
```

A. 程序输出：6

B. 程序输出：5 7

C. 程序输出：6 7

D. 程序输出：1 5

E. 程序输出：6 5

答案： A

解释：

## 题号：209

当你尝试编译并运行以下代码时会发生什么？选择所有正确答案。

```cpp
#include <iostream>
using namespace std;

class C {
public:
  int _c;
  C():_c(0){}
  C(int c) {_c = c;}
  C operator+=(C & b) {
    C tmp; tmp._c = _c+b._c;
    return tmp;
  } 
};

ostream operator<<(ostream & c, const C & v) {
  c<<v._c; return c; }
}

template <class T>
class A {
  T _v;
public:
  A() { }
  A(T v):_v(v){}
  T getV() { return v; }
  void add(T & a) { _v+=a; }
};

int main()
{
  A<int> b(2);
  A<C>a(5);
  a.add(C);
  cout << a.getV() <<endl;
  return 0;
}
```

A. 程序将显示：5

B. 程序无法编译

C. 程序将编译

D. 程序将导致运行时异常

答案： A,C

解释：

## 题号：210

当你尝试编译并运行以下代码时会发生什么？选择所有适用项。

```cpp
#include <vector>
#include <iostream>
using namespace std;
int main ()
{
  vector<int>v1(10, 3);
  v1.push_back(3);
  cout<<v1.capacity()<<v1.size()<<endl;
  return 0;
}
```

A. 程序显示 4

B. 程序显示 10 3

C. `vector` `v1` 的大小为 11

D. `v1` 的所有元素都相同

答案： C,D

解释：

## 题号：211

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <list>
#include <iostream>
using namespace std;
bool mycomparison (int first, int second){return first<second;}
template<class T>
void print(T start, T end) {
  while (start != end) {
    std::cout << *start << " ";
  }
}

int main()
{
  int t1[] = { 1, 7, 8, 4, 5 };
  list<int> l1(t1, 5);
  int t2[] = { 3, 2, 6, 9, 0 };
  list<int> l2(t2, 5);
  l1.sort(mycomparison);
  l2.sort(mycomparison);
  l1.merge(l2,mycomparison);
  print(l1.begin(), l1.end());
  print(l2.begin(), l2.end()); cout<<endl;
  return 0;
}
```

A. 程序输出：9 8 7 6 5 4 3 2 1 0

B. 程序输出：9 8 7 6 5 4 3 2 1

C. 程序输出：9 8 7 6 5 4 3 2 1 0 3 2

. 程序输出.0 1 2 3 4 5 6 7 8 9

E. 程序输出：0 1 2 3 4 5 6 7 8 9

答案： A

解释：

## 题号：212

当你尝试编译并运行以下代码时，假设你输入序列：true true？

```cpp
#include <iostream>
#include <string>
using namespace std;

int main ()
{
  bool a,b;
  cin>>a>>b;
  cout<<a<<b<<endl;
  return 0;
}
```

A. truue

B. falsefalse

C. 1

D. 0

E. 以上均不是

答案： E

## 题号：213

当你尝试编译并运行以下代码时会发生什么？



```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <functional>

using namespace std;
class B { 
  int val;
public:
  B(int v=0):val(v){}
  int get() const {return val};
  B operator+(const B &b) { return B(val + b); }
}

ostream operator<<(ostream & o, const B & v) { out<<v(); return out; }
template<class T>struct Out {
  ostream & out;
  Out(ostream & o): out(o)
  void operator()(const T & val) { out<<val<< " "; }
}

template<typename A> struct Add : public_function<A, A> {
  A operator()const A & a, const A & b) const { return a+b; }
}

int main() {
  int t[]={1,2,3,4,5,6,7,8,9,10};
  vector<B> v1(t, t+10);
  vector<B> v2(10);
  transform(v1.begin(), v1.end(), v2.begin(), bind(Add<B>()));
  for_each(v2.begin(), v2.end(), Out<B>(cout));cout<<endl;
  return 0;
}
```

A. 1 2 3 4 5 6 7 8 9 10

B. 2 3 4 5 6 7 8 9 10

C. 10 9 8 7 6 5 4 3 2 1

D. 11 10 9 8 7 6 5 4 3 2

E. 编译错误

答案： E

## 题号：214

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
using namespace std;
class C {};

template <class T>
class A {
  T _v;
public:
  A() {}
  A(T v) : _v(v){}
  T getV() { return _v; }
  void add(T a) { _v+=a; }
};

int main() {
  A<int> b;
  A<C> a;
  a.add(C);
  cout << b.getV() << endl;
  return 0;
}
```

A. 程序显示：0

B. 程序无法编译

C. 程序将编译

D. 程序将导致运行时异常

答案： B

## 题号：215

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
#include <functional>
using namespace std;
class B { 
  int val;
public:
  B(int v):val(v){}
  int getV() const {return val;}
  bool operator > (const B& v) const { return val>v.val; }
  ostream operator<<(ostream& out, const B& v) { out<<v.getV(); return out; }
}
template<class T>struct Out {
  ostream & out;
  Out(ostream & o): out(o){
  void operator()(const T & val ) { out<<val<<" " }; }
}

int main() {
  B t[]={3,2,4,1,5,10,9,7,8,6};
  vector<B> v1(t,t+10);
  out<<*max_element(v1.begin(), v1.end(), greater<B>());
  cout<<endl;
  return 0;
}
```

A. 3

B. 1

C. 6

D. 10

E. 编译错误

答案： B

## 题号：216

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <deque>
#include <set>
#include <iostream>
#include <algorithm>
using namespace std;
class B { 
  int val;
public:
  B(int v):val(v)
  int getV() const {return val;} bool operator < (const B & v) const { return val<v.val; };
  ostream & operator<<(ostream & out, const B & v) { out<<v.getV(); return out; }
}

template<class T>struct Out {
  ostream & out;
  Out(ostream &o): out(o);
  void operator() (const T & val) { out<<val<< " "; }
}
```

```cpp
B(4))<<endl;
return 0;
}
```

程序输出为：

+   A. 1 0

B. 1 1

C. 0 0

D. 0 1

E. 编译错误

答案：B

解析：

# 题号：217

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <deque>
#include <iostream>
#include <algorithm>
```

```cpp
#include <functional>
using namespace std;
class B { int val;
public:
    B(int v):val(v){}
    int getV() const { return val; }
    bool operator >(const B & v) const { return val>v.val; }
    ostream & operator <<(ostream & out, const B & v) { out<<v.getV(); return out; }
    template<class T>struct Out {
    ostream & out; Out(ostream & o): out(o){}
    void operator()(const T & val ) { out<<val<<" "; } 
};

int main() {
    int t[]={20, 30, 10, 20, 30, 10, 20, 30, 10, 20};
    deque<B> d1(t, t+10);
    sort(d1.begin(), d1.end(), greater<B>());

    pair<deque<B>::iterator, deque<B>::iterator> result = equal_range(d1.begin(), d1.end(),
    greater<B>());

    for_each(result.first, result.second, Out<B>(cout));cout<<endl;
    return 0;
}
```

程序输出为：

+   A. 30 30 20 20 20 20 10 10 20

B. 20 20 20

C. 30 20 20 20 10

D. 20 20 20 20 10

E. 30 20 20 20 10

答案：B

解析：

# 题号：218

当你尝试编译并运行以下代码时，假设你输入了序列：one two three<enter>，会发生什么？

```cpp
#include <iostream>
#include <string>

using namespace std;

int main ()
{
    string a;
    getline(cin, a);
    cout<<a<<endl;
    return 0;
}
```

程序将输出：

+   A. one

B. one two three

C. 运行时异常

D. 编译错误

E. 结果未定义

答案：B

解析：

# 题号：219

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
```



```cpp
using namespace std;
template<class T>struct Out {
ostream & out;
Out(ostream &o): out(o){}
void operator()(const T & val ) {
    out<<val<<" ";
}
};

struct Sequence {
    int start;
    Sequence(int start):start(start){}
    int operator()() { return start++; };
};

int main() {
    vector<int> v1(10);
    vector<int> v2(10);
    generate(v1.begin(), v1.end(), Sequence(1));
    random(v1.begin(), v1.end());
    for_each(v1.begin(), v1.end(), Out<int>(cout));cout<<endl;
    return 0;
}
```

程序输出为：

+   A. 1 2 3 4 5 6 7 8 9 10
B. 10 9 8 7 6 5 4 3 2 1
C. 8 2 4 9 5 7 10 6 1 3
D. 编译错误

答案：D

解析：

# 题号：220

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
using namespace std;
int main()
{
    cout.setf(ios::oct, ios::base);
    cout<<100;
    cout.setf(ios::showbase);
    cout<<100;
    return 0;
}
```

程序输出为：

+   A. 144 0
B. 144 6
C. 0144 44
D. 144 100
E. 编译错误

答案：A

解析：

# 题号：221

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
template<class T>struct Out {
ostream & out;
Out(ostream & o): out(o){}
void operator()(const T & val ) { out<<val<<" "; }
};
struct Sequence {
    int start;
    Sequence(int start):start(start){}
    int operator()() { return start++; }
};
struct Odd { 
    bool operator()(int v) { return v%2==0; }
};
int main() {
    vector<int> v1(10);
    vector<int> v2(10);
    stable_partition(v1.begin(), v1.end(), Sequence(1));
    stable_partition(v1.begin(), v1.end(), Odd());
    for_each(v1.begin(), v1.end(), Out<int>(cout));cout<<endl;
    return 0;
}
```

程序输出为：

+   A. 1 2 3 4 5 6 7 8 9 10
B. 5 7 9 10 2 8 4 6
C. 10 2 8 4 6 5 7 3 9
D. 4 6 8 10 2 7 5 9
E. 2 4 6 8 10 1 3 5 7

答案：E

解析：

# 题号：222

当你尝试编译以下代码时会发生什么？

```cpp
#include <deque>
#include <vector>
#include <iostream>
using namespace std;
template<typename T>
int calculate(T start)

cout<<calculate(d1.rbegin(),d1.rend())<<" ";
cout<<calculate(t[0])<<" ";
cout<<endl;
return 0;
}
```

程序输出为：

+   A. 编译错误
B. 运行时异常
C. 55 17 55
D. 55 17

答案：A

解析：

# 题号：223

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <set>
#include <vector>
using namespace std;
int main(){
    int t[]={ 3, 4, 2, 1, 6, 5, 7, 9, 8, 0 };
    multiset<int> s1(t,t+10);
    s1.insert(s1.find(7), 3);
    for(multiset<int>::iterator i=s1.begin();i!=s1.end(); i++)
    cout<<*i<<" ";
    return 0;
}
```

程序输出为：

+   A. 0 1 2 3 4 5 6 7 8 9
B. 0 1 2 3 4 5 6 7 8 9
+   C. 0 1 2 3 4 5 6 7 8 9
D. 0 1 2 3 4 5 6 7 8 9
E. 运行时异常

答案：A

解析：

# 题号：224

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <string>

using namespace std;

template <class T>
class A {
    T _v;
public:
    A() {}
    A(T v) :_v(v){}
    T getV() { return _v; }
    void add(T & a);
    void add(string & a);
};

template<class T>
void A<T>::add(T & a) { _v+=a; }

void A<string>::add(string & a) {
    _v.insert(0, a);
}

int main()
{
    A<string>a("Hello");
    string s(" world!");
    a.add(s);
    cout << a.getV() <<endl;
    return 0;
}
```

程序输出为：

+   A. 程序显示: Hello world!
B. 编译错误
C. 程序显示: world!
D. 程序运行但无输出

答案：B

解析：

# 题号：225

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <vector>
#include <iostream>
#include <algorithm>

using namespace std;
template<class T>struct Out {
ostream & out;
Out(ostream &o) : out(o){}
void operator()(const T & val ) { out<<val<<" "; }
};
struct Add {
    int operator()(int & a, int & b) {
        return a+b;
    }
};
int main() {
    int t[]={1,2,3,4,5,6,7,8,9,10};
    vector<int> v1(t, t+10);
    vector<int> v2(10);
    transform(v1.begin(), v1.end(), v2.begin(), bind(1,Add()));
    for_each(v2.rbegin(), v2.rend(), Out<int>(cout));cout<<endl;
    return 0;
}
```

程序输出为：

+   A. 1 2 3 4 5 6 7 8 9 10
B. 2 3 4 5 6 7 8 9 10 11
C. 10 9 8 7 6 5 4 3 2
D. 10 9 8 7 6
E. 编译错误

答案：E

解析：

# 题号：226

当你尝试编译并运行以下代码时会发生什么？



```cpp
#include <vector>
#include <iostream>
#include <algorithm>

using namespace std;
void print(int v) { cout<<v; }
struct Sequence {
    int start;
    Sequence(int start):start(start){}
    int operator()() { return start++; }
};
int main() {
    vector<int> v1(10);
    generate_n(v1.begin(), 10, Sequence(1));
    remove(v1.begin(), v1.end(), 10);
    for_each(v1.begin(), v1.end(), print);
}
```

程序输出为：

+   A. 20 30 20 10

B. 20 30 20 10

+   C. 20 30 20 10

D. 编译错误

答案：`C`

解析：

## 题号：227

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <set>
#include <vector>
using namespace std;
int main(){
    int t[] = { 3, 4, 2, 1, 6, 5, 7, 9, 8, 0 };
    vector<int> v(t,t+10);
    set<int> s1(v.begin(),v.end());
    s1.insert(s1.find(7), 3);
    pair<set<int>::iterator,set<int>::iterator> range;
    range = s1.equal_range(6);
    cout<<range.first<<" "<<range.second<<endl;
    return 0;
}
```

输出将是：

+   A. 6

B. 5

C. 6

D. 1

E. 6

答案：`C`

解析：

## 题号：228

当你尝试编译并运行以下代码时会发生什么？

```cpp
#include <iostream>
#include <set>
#include <vector>
using namespace std;
int main(){
    int myints[] = { 3, 4, 2, 1, 6, 5, 7, 9, 8, 0 };
    vector<int> v(myints, myints+end());
    set<int> s1(v.begin(), v.end());
    set<int, greater<int>> s2(v.begin(), v.end());
    for(set<int>::iterator i=s1.begin();i!= s1.end(); i++) {
      cout<<*i<<" ";
    }
    for(set<int, greater<int>>::iterator i=s2.begin();i!=s2.end(); i++) {
      cout<<*i<<" ";
    }
    cout<<endl;
    return 0;
}
```

A. 程序输出： 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9

B. 程序输出： 9 8 7 6 5 4 3 2 1 0 9 8 7 6 5 4 3 2 1 0

C. 程序输出： 0 1 2 3 4 5 6 7 8 9 9 8 7 6 5 4 3 2 1 0

D. 编译错误
