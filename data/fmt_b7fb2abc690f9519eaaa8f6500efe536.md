
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
