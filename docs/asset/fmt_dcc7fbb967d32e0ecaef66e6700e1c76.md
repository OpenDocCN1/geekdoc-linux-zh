
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
