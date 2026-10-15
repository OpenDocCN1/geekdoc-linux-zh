
### 术语表

* **子程序 (subroutine)** — 参见 shell 函数。
* **test 命令** — 用于创建一个条件，该条件返回真（成功）或假（失败）退出状态。
* **tr 命令** — 用于从数据字符串中替换或删除字符。
* **until** — 一种循环控制结构，重复性地执行一系列命令，直到某个条件返回真（成功）退出状态。
* **变量 (variable)** — 存储在内存中并由 Linux shell 使用的值。
* **变量替换操作符 (variable substitution operators)** — 用于修改 shell 变量的内容。
* **while** — 一种循环控制结构，重复性地执行一系列命令，直到某些条件返回真（成功）退出状态。

### 复习题

1. 使用 `sh myscript` 命令执行名为 `mscript` 的 shell 脚本，至少需要什么权限？

2. 使用 `myscript` 命令执行名为 `mscript` 的 shell 脚本，至少需要什么权限？

3. 要仅通过文件名执行 shell 脚本，它必须存在于变量 `variable` 列出的目录中。

4. 下列哪个命令将打印今天的日期？
   a. `echo Today is "date"`
   b. `echo Today is (date)`
   c. `echo Today is [date]`
   d. `echo Today is 'date'`

5. 下列哪个命令会将值 `5` 放入变量 `NUM` 中？（选择所有适用。）
   a. `NUM=`expr 2 + 3``
   b. `let NUM="2 + 3"`
   c. `NUM$(2+3)`
   d. `NUM$[2+3]`

6. 下列哪个命令会将数字 `5` 放入变量 `NUM` 中？
   a. `echo ${NUM-5}`
   b. `echo ${NUM=5}`
   c. `echo ${NUM*5}`
   d. `echo ${NUM%5}`

7. 下列哪个等于以下代码？
   ```
   if test -d $DIR
   then
       cd $DIR
   ```
   a. `test -d $DIR | cd $DIR`
   b. `test -d $DIR && cd $DIR`
   c. `test -d $DIR || cd $DIR`
   d. 此脚本将产生错误。

8. 哪个数字退出状态表示成功结果？

9. 下面 shell 脚本将给出什么输出？
   ```
   COUNT=1

   while test $COUNT -gt 0 -a $COUNT -lt 3
   do
       COUNT=`expr $COUNT + 1`
   done

   echo "COUNT=$COUNT"
   ```
   a. `1`
   b. `2`
   c. `3`
   d. `4`

10. `**)` 符号应该用在 `case` 控制结构的开头。对或错？

11. `case` 控制结构中的每个表达式必须用什么结束？
    a. `\`
    b. `\\`
    c. `-`
    d. `;;`

12. 如果在 shell 脚本中使用参数执行函数，函数中的命令如何访问这些参数？\_\_\_\_\_\_\_\_\_\_\_\_\_\_

13. 下面 shell 脚本将生成什么输出？
    ```bash
    sortlist ()
    {
      ls -1 | sort -r
      echo Program finished.
    }
    ```
    a. 文本 `"Program finished."`
    b. 当前目录的反向排序输出
    c. 当前目录的反向排序输出后跟文本 `"Program finished."`
    d. 此脚本将产生错误。

14. 哪个命令可以在执行期间退出循环控制结构？

15. 哪个 `sed` 命令将搜索 `phonedata` 文件的内容并删除任何包含 `bob` 的条目？\_\_\_\_\_\_\_\_\_\_\_\_\_\_

### 探索练习

![](img/501a26f547021936f65b9bd40bb47394_327_0.png)

## 测试表达式

有效的 shell 脚本需要深入了解...

```c
#include <stdio.h>

int main(void)
{
    char name[80];

    printf("Please enter your name: ");
}
```

# 第 7 章 从源码编译软件

```c
scanf("%s", name);
printf("Your name is: %s\n", name);
return(0);
```

该程序提示用户输入姓名，然后它会打印出 `Your name is:` 以及用户输入的姓名。

以下是对每一行的描述：

* `#include <stdio.h>`
  这一行是一个预处理器指令。在实际的源代码被编译成二进制文件之前，预处理器会对该文件进行处理。在这个示例中，该指令指示预处理器包含 `stdio.h` 文件。
  像 `stdio.h` 这样的文件包含了程序稍后将使用的函数信息。这是 C 语言的一个典型特征。每个变量或函数在使用之前都必须进行声明。
  包含函数声明的文件称为头文件，其文件名通常以 `.h` 结尾。

* `main(void)`
  这一行开始了程序的 `main` 函数。这是程序启动时最初被调用的函数。程序可以包含更多函数，但必须至少有一个 `main` 函数。
  函数头通常包含三个部分：
  * 第一，确定返回值的类型；在本例中，是 `int`，即整数。
  * 接下来是函数名。`main` 函数的名称总是 `main`。
  * 最后，在括号中列出函数的参数。关键字 `void` 意味着该函数不期望任何参数。

* `{`
  所有属于函数的内容都包含在花括号中。这一行开始了 `main` 函数的块。

* `char name[80];`
  这一行声明了一个变量 `name`。变量的类型是 `char`，一种用于单个字符的变量类型。在这个示例中，由于你需要在变量中存储多个一个字符，因此声明了 `80` 个 `char` 变量 `[80]`。
  这显示了 C 语言的另一个特征。在使用变量之前，仅仅声明变量是不够的，你还需要指定变量的类型。在上面的示例中，该变量无法存储整数等其他数据。

## 理解 C 语言基础 317

另一个重要元素是行尾的分号。C 语言中的每个声明和每个函数调用都必须以分号结束。

* `printf("Please enter your name: ");`
  这一行打印消息 `Please enter your name:`。它为此使用了 `printf` 函数。这一行也展示了 C 语言典型的函数调用。参数在函数名后的括号中给出。

* `scanf("%s", name);`
  在这一行中使用 `scanf` 函数读取用户的输入。该函数接受两个参数：格式字符串 `%s`，它决定了函数处理输入的方式；以及变量名，输入将存储在该变量中。

* `printf("Your name is: %s\n", name);`
  这一行再次使用 `printf` 函数打印用户输入的姓名。该函数接受两个参数——在本例中是字符串 `Your name is:` 以及持有用户姓名的变量名。
  `name` 的内容被输出在 `%s` 格式字符串的位置，在这种情况下它充当了占位符的作用。

* `return(0);`
  这一行使用 `return` 函数将 `0` 作为函数的返回值。因为这是 `main` 函数，它也决定了整个程序的返回值。

* `}`
  这个花括号结束了 `main` 函数和整个程序。C 程序的代码应该保存在以 `.c` 结尾的文件中。在这个示例中，使用了文件名 `my_name.c`。

# 如何编译一个简单的 C 程序

要执行之前描述的程序，需要将其编译成二进制文件。为此，你需要一个 C 编译器。Linux 中的标准 C 编译器是 `gcc`，即 Gnu 编译器。

要编译简单的示例程序，你通过以下命令调用编译器：

```bash
gcc my_name.c -o my_name
```

首先，将包含源代码的文件名传递给 `gcc`，然后是 `-o` 选项和输出二进制文件的文件名。

# 第 7 章 从源码编译软件

编译完成后，可以像其他命令行程序一样启动二进制文件，如下：

```bash
./my_name
Please enter your name: Florian
Your name is: Florian
```

# 练习 7-1 编译一个简单的 C 程序

在练习中，你将通过以下步骤编译一个简单的 C 程序：

![](img/501a26f547021936f65b9bd40bb47394_335_0.png)

作为第 1 节 `SLES 9` 安装练习的一部分，你已经安装了编译 C 源码所需的包（C/C++ 编译器和工具）。如果你没有成功完成，请在开始练习之前使用 `YaST` 安装和删除软件模块安装此软件。

1. 打开终端窗口。
2. 将 `3038` 课程 DVD 插入光驱。
3. 输入以下命令将示例应用程序的源码包拷贝到 `/tmp` 目录：
   `cp /media/mount_point/exercises/section_7/my_name.c /tmp`（其中 `mount_point` 是 `cdrom`）
4. 进入目录 `/tmp`。
5. 输入以下命令编译程序：
   `gcc my_name.c -o my_name`
6. 编译完成后，输入以下启动程序：
   `./my_name`
7. 验证程序运行正常。
8. 关闭终端。

# 目标 2：理解构建工具

在练习中，你将通过以下步骤编译一个简单的 C 程序：

作为第 1 节 `SLES 9` 安装练习的一部分，你已经安装了编译 C 源码所需的包（C/C++ 编译器和工具）。如果你没有成功完成，请在开始练习之前使用 `YaST` 安装和删除软件模块安装此软件。

## 理解共享库的概念

## 安装构建环境所需的包

执行上述描述的构建过程需要许多不同的软件。安装所有所需包的最简单方法是在 `YaST` 包管理器中选择“C/C++ 编译器和工具”（C/C++ Compiler and Tools）。

要访问预定义的选择，请从过滤器下拉列表中选择“选择”（Selections），如图7-1 所示。

![](img/501a26f547021936f65b9bd40bb47394_338_0.png)

图 7-1

## 目标 3 理解共享库的概念

系统的许多任务由多个应用程序完成。例如，`PNG` 图像文件的打开和显示是由 Web 浏览器、图形程序和其他应用程序完成的。

在每个操作中重新实现打开 `PNG` 文件的功能是没有意义的。因此，程序功能可以存储在共享库中。

在打开和显示 `PNG` 这种的情况下，该功能由共享库 `libpng` 提供。

从物理上讲，共享库是硬盘上的一个文件，会被加载到主内存中。查找和加载所需库的任务由程序完成。

## 第 7 节从源码编译软件

图 7-2 展示了共享库的工作原理。

![](img/501a26f547021936f65b9bd40bb47394_339_0.png)

图 7-2

通常，一个共享库有两个基本部分：

* 共享库文件本身，当程序需要相应库的函数时会被加载。这些文件的文件名以 `.so`（共享对象）结尾。
* 库的头文件，包含库的函数声明。这些文件的文件名以 `.h`（头文件）结尾。

正如本节开头描述的，C 语言要求程序中使用的每个函数都必须经过声明。

这意味着，为了编译使用该库函数的软件，需要在系统上安装该库的头文件。要运行已经编译好的软件，只需要共享库文件。

由于随 `SLES 9` 附的软件已经经过编译，因此默认情况下不会安装某些库的头文件。这些库被分成两个包：包含头文件的软件包在包名后会附有 `-devel` 后缀。

例如，`libpng` 包包含共享库，而 `libpng-devel` 包包含相应的头文件。

当你运行 `configure` 脚本时，它有时会提示你缺少应该安装在系统上的库。如果你使用 `YaST` 安装了所需的包，你必须确保同时选择了共享库和相应的 `devel` 包。

## 执行标准构建过程

## 目标 执行标准构建过程

在此目标中，将从源码归档编译并安装 `xpenguins` 程序，以此作为标准构建过程的示例。

`xpenguins` 程序可以被下载到一个名为 `xpenguins-2.2.tar.gz` 的 `tar` 归包中。

在开始构建过程之前，你需要通过输入以下命令来提取 `tar` 归包：

```bash
tar xzf xpenguins-2.2.tar.gz
```

* 某些 `tar` 归包以 `.bz` 结尾。在这种情况下，归包使用 `bzip` 压缩，需要使用 `xjf` 选项进行解压。

**注意**

解压归包后，你需要通过输入以下命令切换到创建的源码目录：

```bash
cd xpenguins-2.2/
```

在源码目录中，你需要使用以下命令运行 `configure` 脚本：

```bash
./configure
```

输出如下：

```text
creating cache ./config.cache
checking for a BSD compatible install... /usr/bin/install -c
checking for build environment is sane... yes
checking whether make sets $ {MAKE}... yes
checking for working aclocal... found
checking for working autoconf... found
checking for working automake... found
checking for working autoreader... found
checking for working makeinfo... missing
checking for gcc... gcc
checking whether the C compiler (gcc ) works... yes
checking whether the C compiler (gcc ) is a cross-compiler... no
checking whether we are using GNU C... yes
checking whether gcc accepts... yes
checking for a BSD compatible install... /usr/bin/install -c
checking how to run the C preprocessor... gcc -E
checking for X... libraries /usr/X11R/lib, headers
/usr/X11R/include
checking for dnet_ntoa in -ldnet... no
checking for dnet_ntoa in -ldnet_stub... no
checking for gethostbyname... yes
checking for connect... yes
checking for remove... yes
checking for shmat... yes
checking for IceConnectionNumber in -LICE... yes
checking for XpmFileToData in -lX... yes
checking for XpmFree in -lpm... yes
checking for ANSI C header... yes
checking for unistd.h... yes
checking whether time.h and sys/time.h may both be included
y
checking return type of signal handlers... void
checking for select... yes
checking for strdup... yes
updating cache ./config.cache
creating ./config.status
creating Makefile
creating src/Makefile
```

在输出的最后几行，你可以看到 `Makefile` 已创建。如果 `configure` 脚本没有报告任何错误，你可以通过输入以下命令开始编译过程：

```bash
make
```

执行 `make xpenguins` 的输出如下：
