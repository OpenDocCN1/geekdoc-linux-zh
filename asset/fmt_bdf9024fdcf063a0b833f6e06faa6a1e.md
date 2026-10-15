
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
