

## STEP 5

有趣的数学内容出现在你调用 C++ 数学库时。该头文件包含数十个数学函数以及其他运算。从计算余弦到带两个参数的反正切，再到 Pi 的值。你可以用以下方式调用该头文件：

```
#include <iostream>
#include <cmath>
using namespace std;

int main()
{ 
}
```

![](img/f80199d101da92d953f18eaa6205b48e_138_0.png)

## STEP 6

首先获取一个数的平方根：

```
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
    float number = 134;
    cout << "The square root of " << number << " is: " << sqrt(number) << "\n";
}
```

![](img/f80199d101da92d953f18eaa6205b48e_138_1.png)

## STEP 7

这里我们创建了一个名为 number 的新 float，并使用 sqrt(number) 函数来显示 134 的平方根，即变量 number 的值。构建并运行代码，你的答案为 11.5758。

![](img/f80199d101da92d953f18eaa6205b48e_138_2.png)

## STEP 8

计算数的幂可以用：

```
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
    float number = 12;
    cout << number << " to the power of 2 is " << pow(number, 2) << "\n";
    cout << number << " to the power of 3 is " << pow(number, 3) << "\n";
    cout << number << " to the power of 0.8 is " << pow(number, 0.8) << "\n";
}
```

![](img/f80199d101da92d953f18eaa6205b48e_138_3.png)

## STEP 9

这里我们创建了一个名为 number 的 float，其值为 12，而 pow(variable, power) 就是计算发生的地方。当然，你可以在不使用变量的情况下计算幂和平方根。例如，pow(12, 2) 输出的值与代码中第一个 cout 行相同。

![](img/f80199d101da92d953f18eaa6205b48e_138_4.png)

## STEP 10

Pi 的值也存储在 cmath 头文件库中。它可以用 M_PI 函数调用。输入 cout << M_PI; 到代码中，你会得到 3.14159；或者你可以用它来计算：

```
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
    double area, radius = 1.5;
    area = M_PI * radius * radius;
    cout << area << "\n";
}
```

![](img/f80199d101da92d953f18eaa6205b48e_138_5.png)

## User Interaction

没有什么比创建一个响应你的程序更令人满意的了。这种基本的用户交互是任何语言中最常教授的方面之一，有了它，你就能做得远不止简单地按名字问候用户。

## HELLO, DAVE

你已经在我们的代码中贯穿始终地使用了 cout，标准输出流。现在你将使用 cin，标准输入流，来提示用户响应。

## STEP 1

你希望用户输入到程序中的任何内容都需要存储在系统内存中的某个位置，以便检索和使用。因此，任何输入都必须首先声明为变量，以便用户可以使用。先创建一个空白的 C++ 文件并添加头文件。

```
userinteraction.cpp
1 #include <iostream>
2 using namespace std;
3 
4 int main()
5 {
6 
7 
8 
9 }
10
```

## STEP 2

变量的数据类型还必须与你希望从用户那里获得的输入类型相匹配。例如，要询问用户的年龄，你会使用这样的整数：

```
#include <iostream>
using namespace std;

int main ()
{
    int age;
    cout << "what is your age: ";
    cin >> age;
    cout << "\nYou are " << age << " years old.\n";
}
```

```
userinteraction.cpp
1 #include <iostream>
2 using namespace std;
3 
4 int main()
5 {
6     int age;
7     cout << "What is your age: ";
8     cin >> age;
9     
10    cout << "\nYou are " << age << " years old.\n";

12 
13 }
14
```

## STEP 3

cin 命令的工作方式与 cout 命令相反。使用第一个 cout 行，你将‘What is your age’输出到屏幕上，如尖括号所示。Cin 使用相反方向的尖括号，表示输入。输入被放入整数 age 中，并在第二个 cout 命令中调用。构建并运行代码。

![](img/f80199d101da92d953f18eaa6205b48e_139_0.png)

## STEP 4

如果你要提问，就需要将输入存储为字符串；要询问用户的姓名，你会使用：

```
#include <iostream>
using namespace std;

int main ()
{
    string name;
    cout << "what is your name: ";
    cin >> name;
    cout << "\nHello, " << name << ", I hope you’re well today?\n";
}
```

```
userinteraction.cpp
1 #include <iostream>
2 using namespace std;
3 
4 int main()
5 {
6     string name;
7     cout << "What is your name: ";
8     cin >> name;
9     
10    cout << "\nHello, " << name << ", I hope you’re well today?\n";
11 
12 }
13 

14
```

## STEP 5

原理与之前的代码相同。用户的输入，即他们的姓名，被存储在一个字符串中，因为它包含多个字符，并在第二个 cout 行中检索。只要变量‘name’不改变，你就可以在代码中的任何地方调用它。

![](img/f80199d101da92d953f18eaa6205b48e_140_0.png)

## STEP 6

你可以将输入请求链接给用户，但只要确保一开始有有效的变量来存储输入即可。假设你希望用户输入两个整数：

```
#include <iostream>
using namespace std;

int main ()
{
    int num1, num2;

    cout << "Enter two whole numbers: ";
    cin >> num1 >> num2;

    cout << "you entered " << num1 << " and " << num2 << "\n";
}
```

![](img/f80199d101da92d953f18eaa6205b48e_140_1.png)

## STEP 7

同样，一旦你将数据存储在变量中，就可以对其进行操作。例如，询问用户两个数字并对它们进行一些数学运算：

```
#include <iostream>
using namespace std;

int main ()
{
    float num1, num2;

    cout << "Enter two numbers: \n";
    cin >> num1 >> num2;

    cout << num1 << " + " << num2 << " is: " << num1 + num2 << "\n";
}
```

![](img/f80199d101da92d953f18eaa6205b48e_140_2.png)

## STEP 8

虽然 cin 对于大多数输入任务都适用，但它确实有一个限制。Cin 总是把空格视为终止符，所以它设计用于单个单词而不是多个单词。然而，getline 将 cin 作为第一个参数，变量作为第二个参数：

```
#include <iostream>
using namespace std;

int main ()
{
    string mystr;
    cout << "Enter a sentence: \n";
    getline(cin, mystr);
    cout << "Your sentence is: " << mystr.size() << " characters long.\n";
}
```

![](img/f80199d101da92d953f18eaa6205b48e_140_3.png)

## STEP 9

构建并执行代码，然后输入一个带空格的句子。完成后，代码会读取字符数。如果你删除 getline 行并用 cin >> mystr 替换它然后再试一次，结果会显示到第一个空格为止的字符数。

![](img/f80199d101da92d953f18eaa6205b48e_140_4.png)

## STEP 10

Getline 通常是新 C++ 程序员忘记包含的命令。当你无法弄清楚为什么代码无法工作时，终止空白会很烦人。简而言之，最好以后使用 getline(cin, variable)：

```
#include <iostream>
using namespace std;

int main ()
{
    string name;
    cout << "Enter your full name: \n";
    getline(cin, name);
    cout << "\nHello, " << name << ".\n";
}
```

## The Hobbit

你知道吗...

1982 年为各种平台发布，Melbourne House 的《霍比特人》是一项编程天才之作。由 Philip Mitchell 和 Dr. Veronika Megler 开发，《霍比特人》独特地使用了一种名为‘Inglish’的解析器，允许玩家输入完整的句子，例如“Take sword from Gandalf, and kill goblin with it.”

此外，游戏中每个对象都有特定的大小、重量和坚固度；所以如果你坐在凳子上，而有人拿起凳子或扔掉它，那么你的角色也会随之被带走。

character would be taken along with it. 此外，在游戏的早期版本中，非玩家角色经常在地图上移动，并在玩家甚至还没有到达该阶段之前就互相捕获并杀死对方。游戏开始时还设置了一个随机事件，任何角色都可能从任何位置拿起随机对象。这意味着，潜在地，Thorin 可以把你捡起来并在整个冒险中携带你。对于一个占用内存不到 38KB 的游戏来说，这真是令人惊叹。

![](img/f80199d101da92d953f18eaa6205b48e_141_0.png)

