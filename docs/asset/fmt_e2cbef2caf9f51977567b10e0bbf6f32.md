
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
