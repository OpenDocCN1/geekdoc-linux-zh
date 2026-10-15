
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
