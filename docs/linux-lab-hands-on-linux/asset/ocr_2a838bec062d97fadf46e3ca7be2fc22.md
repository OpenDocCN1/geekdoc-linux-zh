# **Listing 2**

```
```
#include<iostream>
using namespace std;
class test
{
public: int i;
public:
 test(int x);
 ~test()
 {
 cout<<"The value of i is "<<<<"\n";
 };
};
test::test(int x)
{
 i=x;
};
int main()
{
 test t(6);
 return 0;
}
```
```

The code appears in the text editor, as shown in Figure 8:

![](bbox=[0.3, 0.49, 0.77, 0.77])

# **▲ Figure 8**

+   3. Click the File menu and select the Save As option, as shown in Figure 9: