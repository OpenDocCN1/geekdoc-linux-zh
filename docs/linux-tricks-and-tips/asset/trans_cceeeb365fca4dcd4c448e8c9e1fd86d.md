
## 用户交互

没有什么比创建一个能够对你做出响应的程序更令人满足的了。这种基本的用户交互是任何编程语言中最常教授的内容之一，通过它，你能做的远不止简单地用名字问候用户。

### 你好，戴夫

你已经在我们的代码中多次使用了 `cout`（标准输出流）。现在，你将使用 `cin`（标准输入流）来提示用户响应。

- **步骤 1**  
  任何你想让用户输入到程序中的内容都需要存储在系统内存的某个地方，以便之后检索和使用。因此，任何输入都必须首先声明为一个变量，以便随时供用户使用。首先，创建一个带有头文件的空白 C++ 文件。

![](img/4aefeb2d095f688b34af6207870c5f39_59_0.png)

- **步骤 2**  
  变量的数据类型还必须与你想从用户那里获取的输入类型相匹配。例如，若要询问用户的年龄，你会使用类似以下的整数：

```cpp
#include <iostream>
using namespace std;

int main ()
{
    int age;
    cout << "What is your age: ";
    cin >> age;
    
    cout << "\nYou are " << age << " years old.\n";
}
```

![](img/4aefeb2d095f688b34af6207870c5f39_59_1.png)

- **步骤 3**  
  `cin` 命令的工作方式与 `cout` 命令相反。在第一行 `cout` 中，你将“What is your age?”（你多大了？）输出到屏幕上，如尖括号所示。`cin` 使用方向相反的尖括号，表示输入。该输入被放入整数变量 `age` 中，并在第二个 `cout` 命令中调用。编译并运行代码。

![](img/4aefeb2d095f688b34af6207870c5f39_59_2.png)

- **步骤 4**  
  如果你要问一个问题，你需要将输入存储为字符串。要询问用户的名字，你会使用：

```cpp
#include <iostream>
using namespace std;

int main ()
{
    string name;
    cout << "What is your name: ";
    cin >> name;
    
    cout << "\nHello, " << name << ". I hope you're well today?\n";
}
```

![](img/4aefeb2d095f688b34af6207870c5f39_59_3.png)

- **步骤 5**  
  其原理与前一段代码相同。用户的输入（他们的名字）被存储在一个字符串中，因为它包含多个字符，并在第二行 `cout` 中被调出。只要变量 `name` 不发生改变，你就可以在代码中的任何地方调用它。

![](img/4aefeb2d095f688b34af6207870c5f39_59_4.png)

- **步骤 6**  
  你可以向用户连续提出多个输入请求，但只需确保你有一个有效的变量来开始存储输入即可。假设你想让用户输入两个整数：

```cpp
#include <iostream>
using namespace std;

int main ()
{
    int num1, num2;
    
    cout << "Enter two whole numbers: ";
    cin >> num1 >> num2;
    
    cout << "You entered " << num1 << " and " << num2 << "\n";
}
```

![](img/4aefeb2d095f688b34af6207870c5f39_60_1.png)

- **步骤 7**  
  同样，一旦将数据存储到变量中，就可以对其进行操作。例如，向用户索要两个数字并对它们进行一些数学运算：

```cpp
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

![](img/4aefeb2d095f688b34af6207870c5f39_60_2.png)

- **步骤 8**  
  虽然 `cin` 在大多数输入任务中表现良好，但它确实有一个局限性。`cin` 始终将空格视为终止符，因此它专为单个单词设计，而非多个单词。然而，`getline` 将 `cin` 作为第一个参数，将变量作为第二个参数：

```cpp
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

- **步骤 9**  
  编译并执行代码，然后输入一个包含空格的句子。完成后，代码读取字符数量。如果你移除 `getline` 并用 `cin >> mystr` 替换它，再试一次，结果将显示直到第一个空格之前的字符数量。

![](img/4aefeb2d095f688b34af6207870c5f39_60_3.png)

- **步骤 10**  
  `getline` 通常是新 C++ 程序员常常忘记包含的命令。当你无法弄清楚代码为什么不起作用时，末尾的空白字符就很烦人。简而言之，将来最好使用 `getline(cin, variable)`：

```cpp
#include <iostream>
using namespace std;

int main ()
{
    string name;
    
    cout << "Enter your full name: \n";
    getline(cin, name);
    
    cout << "\nHello, " << name << "\n";
}
```

![](img/4aefeb2d095f688b34af6207870c5f39_60_4.png)

## 霍比特人

**你知道吗……** 于 1982 年发布在各个平台上的墨尔本屋（Melbourne House）出品的《霍比特人》是一部编程杰作。由 Philip Mitchell 和 Veronika Megler 博士开发，《霍比特人》独特地使用了名为“Inlish”的解析器进行编码，允许玩家输入完整的句子，例如“从甘道夫手中拿走剑，并用它杀死哥布林”。

此外，游戏中的每个物体都有特定的大小、重量和硬度；因此，如果你坐在凳子上，而某人拿起或扔掉了凳子，那么你的角色也会随之移动。而且，在游戏早期版本中，非玩家角色（NPC）经常会在地图上移动，甚至在玩家到达该阶段之前就会捕捉并杀死彼此。游戏中还设有一个随机化事件，每次游戏开始时，任何角色都可以从任何位置拾取一个随机物体。这意味着，有可能，索林会把你拾起并在整个冒险过程中携带你。对于一款占用内存不到 38KB 的游戏来说，这非常了不起。

![](img/4aefeb2d095f688b34af6207870c5f39_61_0.png)

## 先锋 48K ZX Spectrum

![](img/4aefeb2d095f688b34af6207870c5f39_62_0.png)

### 霍比特人

《霍比特人》是一个超级程序，是计算机软件史上的里程碑。你将以文字和图形的形式面临危险、刺激和冒险。与《霍比特人》中的所有角色见面，并用普通英语与他们交谈！《霍比特人》程序为你带来一个激动人心且充满挑战的奇幻未来！

#### 墨尔本屋

霍比特人，1982 年高级编码的奇迹。

## 常见编码错误

当你开始接触新事物时，你不可避免地会犯错，这纯粹是由于经验不足，而这些错误本身就是极好的老师。然而，即使是专家也会偶尔出错。关键在于，尽可能地从错误中吸取教训。

### X = 错误，输出 Y

程序员需要意识到许多陷阱，这里无法一一列举。能够识别错误并修复它是你开始进入更高级领域并成为更好编码者的标志。每个人都会犯错，即使是拥有三十年以上经验的程序员也是。从这些基本且常见的错误中吸取教训有助于建立更好的编码基础。

### 小模块

如果能像《黑客帝国》电影中的 Neo 那样工作就好了。只需询问，你的操作员就会将其加载到你的内存中，你立刻就会了解关于该主题的一切。遗憾的是，我们无法做到这一点。第一个主要陷阱是有人试图学得太多、太快。因此，要分小块学习编码，并从容不迫。

![](img/4aefeb2d095f688b34af6207870c5f39_63_0.png)

### 易读变量

为变量赋予有意义的名称是消除常见编码错误的关键。使用字母表中的字母是可以的，但如果代码显示 x 变量存在问题怎么办。给变量命名并不太难，例如 `lives`（生命）、`money`（金钱）、`player1`（玩家1）等等。

```javascript
var points = 1023;
var lives = 3;
var totalTime = 45;
write("Points: "+points);
write("Lives: "+lives);
write("Total Time: "+totalTime+" secs");
write("--------------------------------");
var totalScore = 0;
write("Your total Score is: "+totalScore);
```

### // 注释

使用注释。这是一个简单的概念，但给你的代码添加注释，当你下次回顾代码时会节省很多麻烦。插入注释行有助于你快速筛选出导致问题的代码部分；如果你需要审查较旧的代码段，这也很有用。

```c
52    orig am 2;
53    target = 2;
54    --Fj

56    #endif
57    if (m == 0)
58        return;
59
60    //
61    // Loop unrolling.  Here be dragons.
62    //
63
64    // (n & (~3)) is the greatest multiple of 4 le
65    // in the while loop ahead, orig will move ov
66    // increments (4 elements of 2 bytes).
67    // end makes our barrier for not falling out
68    char const * const end = orig + 2 * (n & (~3)

70    // See if we're aligned for writing in 64 o
71    #if ARCH_SIZEOF_LONG == 8 & \
72        ((defined( x_amd64 ) || defined( x_86_64
```

### 提前规划

虽然某天早晨醒来决定编码一个经典文本冒险游戏很棒，但没有良好的计划并不总是可行的。短小的代码片段可以在不太多加思考的情况下编写，但更长、更深入代码需要遵循良好的工作计划来帮助消除错误。

![](img/4aefeb2d095f688b34af6207870c5f39_63_1.png)

![](img/4aefeb2d095f688b34af6207870c5f39_63_2.png)

