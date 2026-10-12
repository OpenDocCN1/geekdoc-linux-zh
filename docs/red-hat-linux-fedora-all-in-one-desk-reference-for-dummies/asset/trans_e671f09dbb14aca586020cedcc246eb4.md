
| 宏 | 定义 |
|---|---|
| __LINE__ | 这是一个十进制整数，其值等于当前源文件中的行号。 |
| __STDC__ | 该宏展开为十进制常量 1，用以表示 C 编译器符合 ANSI 标准。 |
| __TIME__ | 该字符串显示开始编译源文件的时间。其格式为 HH:MM:SS（例如，21:59:45）。 |

## 变量的声明与定义

在 C 语言中，你必须在使用变量和函数之前先定义或声明它们。变量的定义指定了三件事：

- 其 *visibility*，表示变量可以使用的确切位置（是定义在程序的所有文件中、当前文件，还是仅在某个函数中）。
- 其 *lifetime*，决定变量是临时存在（例如函数中的局部变量）还是永久存在（只要程序在运行）。
- 其 *type*（在某些情况下还有其 *initial value*）。例如，初始化为 1 的整数变量 x 是这样定义的：

```c
int x = 1;
```

如果你使用在另一个源文件中定义的变量，则使用 extern 关键字声明该变量，如下所示：

```c
extern int message_count;
```

你必须在至少一个源文件中不带 extern 限定符地定义此变量。程序构建时，链接器会解析对 message_count 变量的所有引用，并确保它们都使用同一个变量。

## 基本数据类型

C 有四种基本数据类型：char 和 int 用于存储字符和整数，而 float 和 double 用于浮点数。你可以以直接的方式为这些基本数据类型定义变量：

```c
char c;
int i, j, bufsize;
float volts;
double mean, variance;
```

你可以通过使用 long、short 和 unsigned 限定符作为前缀，将基本数据类型扩展为更大的集合。long 和 short 限定符是大小修饰符。例如，long int 至少为 4 字节长，而 short int 的最小大小仅为 2 字节。int 的大小取决于系统，但它肯定至少与 short 一样大。

unsigned 限定符仅保留给 int 和 char 类型。通常，这些类型同时保存负值和正值。这是这些数据类型的默认 signed 形式。当你希望变量仅保存正值时，可以使用 unsigned 限定符。以下是使用 short、long 和 unsigned 限定符的一些示例：

```c
unsigned char mode_select;
unsigned char printer_status;
short record_number; /* Same as "short int" */
long offset; /* Same as "long int" */
unsigned int i, j, msg_id; /* Same as "unsigned int" */
unsigned short width, height; /* Same as "unsigned short int" */
unsigned long file_pos; /* Same as "unsigned long int" */
long double result;
```

当 short、long 和 unsigned 限定符与 int 类型一起使用时，可以在声明中省略 int。你也可以使用 long 前缀扩展 double 数据类型。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_771_0.png)

GCC 附带了预定义的头文件 — limits.h 和 float.h — 它们在这些头文件中定义了各种数据类型的确切大小以及值的范围。你可以在 Red Hat Linux 系统的 /usr/include 目录中检查这些文件，以确定 GCC 编译器支持的基本数据类型的大小。

## 枚举

你可以使用 enum 数据类型定义自己的枚举列表——一组固定的命名整数常量。例如，你可以使用 enum 如下声明一个名为 BOOLEAN 的布尔数据类型：

/* Declare an enumerated type named BOOLEAN */
enum BOOLEAN {false = 0, true = 1, stop = 0, go = 1,
    off = 0, on = 1};

/* Define a BOOLEAN called "status" and initialize it */
enum BOOLEAN status = stop;

此示例首先声明 BOOLEAN 为枚举类型。大括号内的列表显示了 enum BOOLEAN 变量的有效枚举常量。你可以按自己的选择初始化每个常量，并且多个常量可以使用相同的值。在此示例中，常量 false、stop 和 off 被设为 0，而 true、go 和 on 被初始化为 1。该示例随后定义了一个名为 status 的枚举 BOOLEAN 变量，其初始值设为常量 stop。

## 结构体、联合体和位域

使用 struct 将相关的数据项组合在一起，并通过名称引用该组合。例如，用于保存队列变量的结构声明可能如下所示：

/* Declare a structure */
struct QUEUE
{
    int count;    /* Number of items in queue */
    int front;    /* Index of first item in queue */
    int rear;     /* Index of last item in queue */
    int elemsize; /* Size of each element of data */
    int maxsize;  /* Maximum capacity of queue */
    char *data;   /* Pointer to queued data */
};

/* Define two queues */
struct QUEUE rcv_q, xmit_q;

QUEUE 结构内部的元素称为其成员。你可以使用成员选择运算符（.）访问这些成员。例如，rcv_q.count 指的是 rcv_q 结构的 count 成员。

union 类似于 struct，但与 struct 将相关数据项组合在一起不同，union 为多个数据项分配存储空间，使其从同一位置开始。因此，union 的所有成员共享相同的存储位置。你可以使用 union 以不同的方式查看相同的数据项。假设你使用的是支持 4 字节 long 数字的编译器，并且想要访问单个 long 整数的 4 个单独字节。以下 union 让你能够实现这一点：

```c
union
{
    long file_type;
    char bytes[4];
} header_id;
```

使用此定义，header_id.file_type 指的是 long 整数，而 header_id.bytes[0] 是该 long 整数的第一个字节。

## 数组

数组是一组一个或多个相同的数据项。你可以声明任何类型的数据的数组，包括结构体和由 typedef 定义的类型。例如，要定义一个包含 80 个字符的数组，你可以编写如下内容：

```c
char string[80];
```

string 数组中的字符占据连续的存储位置，从位置 0 开始。因此，在此示例中，string[0] 指的是该数组中的第一个字符，而 string[79] 指的是最后一个字符。你可以类似地定义其他数据类型和结构体的数组：

```c
struct Customer   /* Declare a structure */
{
 int id;
 char first_name[40];
 char last_name[40];
};
struct Customer customers[100]; /* Define array of structures */
int index[64];   /* An array of 64 integers */
```

你也可以定义多维数组。例如，要表示一个 80 列乘 25 行的文本显示屏，你可以使用二维数组如下：

```c
unsigned char text_screen[25][80];
```

text_screen 的每个项都是一个包含 80 个 unsigned char 的数组，而 text_screen 包含 25 个这样的数组。换句话说，二维数组是通过在内存中按行顺序排列来存储的。你可以使用表达式 text_screen[0][0] 引用第一行中的第一个字符，并使用 text_screen[24][79] 引用显示屏最后一行的最后一个字符。更高维度的数组以类似方式定义：

```c
float coords[3][2][5];
```

此示例将 coords 定义为包含三个数据项的三维数组：每个项都是一个包含两个数组的数组，每个数组又是一个包含五个 float 变量的数组。因此，你将多维数组解释为“数组的数组”。

## 指针

指针是一个变量，可以保存除位域之外任何类型数据的地址。例如，如果 p_i 是指向整数变量的指针，你可以按如下方式定义和使用它：

```c
/* Define an int pointer and an integer */
int *p_i, count;

/* Set pointer to the address of the integer "count" */
p_i = &count;
```

在这种情况下，编译器将为 int 变量 count 和指向整数的指针 p_i 分配存储空间。表示指针所需的字节数取决于底层系统的寻址方案。
