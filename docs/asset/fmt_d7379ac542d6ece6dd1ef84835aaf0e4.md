
## C++ 练习题

**77.**
输出是什么？

```cpp
    cout<<flag<<endl;

    return 0;

}
```

+ A. 0
- B. 1
- C. 2
- D. 3

**78.**
输出是什么？

```cpp
#include <iostream>
using namespace std;

int main() {
  float x=3.6; int y;
  y=(int)x;
  cout<<y<<endl;
  return 0;
}
```

+ A. 3
- B. 4
- C. 5
- D. 6

**79.**
输出是什么？

```cpp
char str[10];
str = "Hello";
cout<<str<<endl;
```

+ A. Hello!
- B. `str[10]`
- C. `false`
- D. Logic error

**80.**
下列哪个代码定义了指针？

+ A. `int &pointer`
- B. `int *pointer`
- C. `int ~pointer`
- D. `int $pointer`

**81.**
输出是什么？

```cpp
#include <iostream>
using namespace std;

int main() {
    int a=100, b=200;
    int *pointer1, *pointer2;
    pointer1=&a;
    pointer2=&b;
    cout<<pointer1<<" "*pointer2<<endl;
    return 0;
}
```

+ A. 0 0
- B. 100 100
- C. 100 200
- D. 200 200

**82.**
下列哪个代码定义了引用？
`int a;`

+ A. `int &b;`
- B. `int *b;`
- C. `int &b=a;`
- D. `int *b=a;`

**83.**
输出是什么？

```cpp
#include <iostream>
using namespace std;

int main() {
    int a=10;
    int &b = a;
    a=a*a;
    b=b/5;
    cout<<a<<endl;
    return 0;
}
```

+ A. 100
- B. 80
- C. 60
- D. 20

**84.**
输出是什么？

```cpp
#include <iostream>
using namespace std;

class Time {
public:
    int hour;
};

int main() {
    Time timeObject;
    timeObject.hour=int(16.9999);
    cout<<timeObject.hour<<endl;
    return 0;
}
```

+ A. 15
- B. 16
- C. 17
- D. 18

**85.**
找出错误的代码。

```cpp
#include<iostream>
using namespace std;

int main() {
    int a, b; //Line 1
    a=100, b=200; //Line 2
    c = a + b; //Line 3
    cout<<"c = "300"<<endl;
    return 0;
}
```

+ A. Line 1
- B. Line 2
- C. Line 3
- D. Line 4

**86.**
输出是什么？

```cpp
#include<iostream>
using namespace std;

int main(){
    int a=3, b;
    b = (int)(a+7.5)%2+(a=5);
    cout << b << endl;
    return 0;
}
```

`b` 的值是多少？

+ A. 3
- B. 4
- C. 5
- D. 6

**87.**
输出是什么？

```cpp
#include<iostream>
using namespace std;

int main(){
  int a=12;
  a+=a-=a*=a;
  cout<<a<<endl;
  return 0;
}
```

`a` 的值是多少？

+ A. 0
- B. 1
- C. 2
- D. 3

**88.**
`#include <stdexcept>` 意味着什么？

+ A. 包含另一个名为 `stdexcept.cpp` 的文件
- B. 包含 `exception.cpp`
- C. 包含可以识别抛给 `catch` 块的异常的类
- D. 以上所有

**89.**
下列运算符优先级最高？

+ A. `+=`
- B. `!=`
- C. `++`
- D. `( )`

**90.**
`getline()` 函数从输入流读取，其语法是？

+ A. `getline(input, str);`
- B. `getline(cin, str);`
- C. `getline(enter, str);`
- D. `getline(type, str);`

**91.**
输出是什么？

```cpp
#include<iostream>
using namespace std;

int main(){
    int a;
    double x=5.8;
    a=x;
    cout<<a<<endl;
    return 0;
}
```

+ A. 5
- B. 6
- C. 7
- D. 8

**92.**
下列哪个表达式不正确？

+ A. `int a[3]={1,2};`
- B. `int a[3]={1,2,3,4};`
- C. `int a[]={1,2,3};`
- D. `int a[3]={1,2,3};`

**93.**
输出是什么？

```cpp
#include <iostream>
using namespace std;

int main() {
    int a[4]={-3,-6,50,26};
    int max=a[0];
    for (int i=1; i<4; i++){
        if (a[i]>max) max=a[i];
    }
    cout<<"max=" << max << endl;
    return 0;
}
```

+ A. -3
- B. -6
- C. 50
- D. 26

**94.**
输出是什么？

```cpp
#include <iostream>
using namespace std;

int main() {
    int a=0, b;
    int a[3]={6,7};
    int *p=a;
    *p=b;
    for (int i=0; i<3; i++) {
        cout<<a[i]<<endl;
    }
    return 0;
}
```

*(注：原文代码94存在多处语法及逻辑错误，此处按要求保留格式并翻译描述)*

+ A. 20
- B. 21
- C. 22
- D. 23

**95.**
输出是什么？

```cpp
#include<iostream>
using namespace std;

int main(){
    char str[10];
    int n=0;
    str="hello";
    try {
    }
    catch {
    }
    while (str[n] != '\0') {
        n++;
    }
    cout<<n;
    return 0;
}
```

+ A. 3
- B. 4
- C. 5
- D. 6

**96.**
下列哪个关键字是访问修饰符？

+ A. `public`
- B. `private`
- C. `protected`
- D. `friend`

**97.**
输出是什么？

```cpp
#include <iostream>
using namespace std;

int main() {
    int a;
    int n=0;
    a=n++;
    while (n++<5) {
        n++;
    }
    cout<<a;
    return 0;
}
```

+ A. 0
- B. 1
- C. 2
- D. 3

**98.**
下列哪个语句是正确的？

```cpp
#include <iostream>
using namespace std;

int main() {
    int a=5;
    int &b=a;
    b=10;
    cout<<a;
}
```

*(注：原题选项似乎有误，此处保留原意)*

+ A. `public`
- B. `private`
- C. `protected`
- D. `friend`

**99.**
输出是什么？

```cpp
#include <iostream>
using namespace std;

int main() {
    int a=0;
    int flag=true;
    a++;
    cout<<a;
    return 0;
}
```

+ A. 0
- B. 1
- C. 2
- D. 3

# HTML CSS 100

## 100 道 HTML CSS

请选择最佳答案。答案在最后一页。

**(1)**

```html
<html>
<strong>这是一段加粗的文本。 </strong><br>
<b>这是一段加粗的文本。 </b><br>
<em>这是一段斜体文本。 </em><br>
<i>这是一段斜体文本。 </i><br>
<img fill in here = = "flower.jpg" width="100" height="80" alt="这是一朵花。 is a flower."> <!-- - 分配图像的地址 - -->
</html>
```
A. `id` B. `name` C. `import` D. `src`

**(2)**

```html
<html>
<style type = "fill in here"> <!-- - 声明一个内部 css - -->
h3#a {color: blue}
p#b {font-size: 16pt; color: orange }
h3.c{color:green}
p.d {font-size: 16pt; color: purple }
</style>
<body>
<h3 id="a"> 这是蓝色的 </h3>
<p id="b"> 这是橙色的 </p>
<h3 class="c"> 这是绿色的 </h3>
<p class="d"> 这是紫色的 </p>
</body>
</html>
```
A. `style` B. `text/css` C. `text/js` D. `text/html`

**(3)**

```html
<html>
<style type="text/css">
#try{font-family:arial black; color: blue}
</style>
<body>
<fill in here id = "A"> <!-- - 有序列表 - -->
<li>HTML</li>
<li>JAVA</li>
<li>AJAX</li>
<li>LAMP</li>
<li>RUBY</li>
</fill in here>
</body>
</html>
```
A. `li` B. `ul` C. `ol` D. `dl`

**(4)**

```html
<html>
<fill in here border="1" > <!-- - 声明一个表格 - -->
<tr>
<td colspan = 3 align = center>单元格 1</td>
</tr>
<tr>
<td>单元格 4</td>
<td>单元格 5</td>
<td>单元格 6</td>
</tr>
</fill in here >
</html>
```
A. `table` B. `form` C. `diagram` D. `chart`

**(5)**

```html
<html>
<style type="text/css">
a:link {color: black; font-family: arial;}
a:visited {color: purple;font-family:Times New Roman; }
a:hover {color: orange;font-style: italic;}
a:active {color: yellow;font-size: 18px;}
</style>
<body>
<a fill in here="http://www.Google.com" target="_blank">欢迎来到 Google </a> <!-- 指定一个 url - -->
</body>
</html>
```
A. `link` B. `hyperlink` C. `href` D. `url`

**(6)**

```html
<html>
<style type="text/css">
#fill in here { font-family: Arial Black; font-size: 20px; font-style: italic; font-weight: normal; font-variant: normal; color: orange }
<!-- - 为指定的 id 设置 css 样式 - -->
</style>
<div id="f">这是一个使用不同样式的练习。</div>
</html>
```
A. `tag` B. `f` C. `id` D. `class`

**(7)**

```html
<html>
<p>冬季</p>
<fill in here data="winter.jpg" type="image/jpeg" width="120" height="90"> [JPG 文件] </fill in here > <!-- 将资源嵌入到 html 文档中 --></p>
</html>
```
A. `embed` B. `src` C. `import` D. `object`

**(8)**

```html
<html>
你最喜欢的运动是什么？
<form action="myFile.php">
篮球 <input type="radio" name="rd" value="Basketball">
排球 <input type="radio" name="rd" value="Volleyball">
棒球 <input type="radio" name="rd" value="Baseball">
足球 <input type="radio" name="rd" value="Football">
<input fill in here = "submit" name="sbmt" value="提交" <!-- 指定一个 input 类型 - -->
</form>
</html>
```
A. `type` B. `id` C. `attribute` D. `method`

**(9)**

```html
<html>
<fill in here > <!-- 嵌入脚本代码 - -->
var myVariale = "Hello World";<br>
alert (myVariable); <br>
</fill in here >
<var>myVariable</var> 是 JavaScript 中的一个变量。
</html>
```
A. `script` B. `embed` C. `code` D. `program`

**(10)**

```html
<html>
<style type = "text/css">
#b{fill in here : solid; border-width: 10px; } <!-- 为边框设置样式 -->
</style>
<body>
<p id = "b">这是实线边框。</p><br>
</body>
</html>
```

**(11)**

```html
<html>
<style type = "text/css">
fill in here {color: blue} // 为标签设置样式
p {font-size: 16pt}
</style>
<h2>CSS</h2>
<p>非常好！</p>
</html>
```

**(12)**

```html
<html>
<fill in here type = "disc"> <!-- 无序列表 - -->
<li>AAAA</li>
<li>BBBB</li>
<li>CCCCC</li>
</fill in here >
```

**(13)**

```html
<html>
<table fill in here = yellow border = 1> 设置背景颜色 -->
<tr>
<td>单元格 1</td>
<td>单元格 2</td>
<td>单元格 3</td>
</tr>
</table>
```
A. `background` B. `color` C. `bgcolor` D. `set`

**(14)**

```html
<html>
<body>
<a href="fill in here: alert('Hello!')">点击</a> <!-- 到 JavaScript 函数 -->
</body>
</html>
```
