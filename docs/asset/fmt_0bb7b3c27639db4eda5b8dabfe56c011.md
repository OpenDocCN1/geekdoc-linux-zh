
```c
update_employee_name(&rec, "Fred Smith" );

print_employee_rec( rec);

return 0;

}
```

程序的基本流程是创建一个名为 "Fred" 且序列号为 25 的员工记录。接下来，程序将员工姓名更新为 "Fred Smith"，但没有触碰序列号。运行程序产生如下输出：

```
penguin> employee

Name: Fred

Number: 25

Updating employee's name ...

Name: Fred Smith

Number: 26740
```

如果程序在更改姓名时不应该更新序列号，为什么它会变更为 26740 呢？这种错误是内存损坏的迹象。如果你已经检查了源代码，可能已经知道问题所在，但让我们使用 GDB 和监视点来告诉我们问题是什么。我们知道在第一次打印员工记录之后发生了某些事情，所以让我们在该处对结构体的 `serial_num` 成员设置一个监视点：

需要注意的是，GDB 能够成功地为该监视点启用硬件。GDB 通过此指示这一点。如果没有出现“Hardware”字样，说明由于某种，GDB 将回退到软件监视点。对于内存损坏，GDB 将确切告诉你损坏发生在何和何时，以便你轻松修复问题。

硬件监视点允许 GDB 正常运行，但在变化发生时（如果发生）会立即通知 GDB。

为了演示监视点，让我们使用一个模拟员工记录系统的简单程序。源代码如下：

（此处代码块与上文相同，保持不翻译）

（注：此处翻译逻辑遵循前文，由于代码块不翻译，此处略过重复代码块展示，下方不再重复翻译完全相同的代码块，逻辑已在正文中出现过）

## 6.6 执行

请注意双等号——这与你在 C 语言编程中用于表达式的表示符号相同。
使用 `info breakpoint` 命令验证断点的设置是否正确：

```
(gdb) info breakpoint

Num Type Disp Enb Address What

1 breakpoint keep y 0xb048832a in main at common.c:10

2 breakpoint keep y 0xb0488312 in common_func at common.c:3

   stop only if num == 345
```

当继续执行程序时，编号号为 2 的断点只有在 `num` 的值为 345 时才会被触发：

```
(gdb) cont

Continuing.

Breakpoint 2, common_func (num=345) at common.c:3

   int foo = num;
```

如果程序是用 `-g` 编译的，你可以在下一个示例中为代码的特定行设置断点：

```
(gdb) break hang2.C:20

Breakpoint 1 at 0xb048467: file hang2.C, line 20.

(gdb) run user

Starting program: /home/wilding/src/Linuxbook/hang2 user
```

```
Breakpoint 1, main (argc=2, argv=0xbffefc4) at hang2.C:20

20   if (!strcmp(argv[1], "user") )

(gdb)
```

如果你没有源代码，也可以如下所示在特定地址设置断点：

```
(gdb) break * 0xb04843c

Breakpoint 2 at 0xb04843c

(gdb) cont

Continuing.
```

```
Breakpoint 2, 0xb04843c in main () ()

(gdb)
```

请注意地址前的 `*`；当 `break` 命令的参数为地址时，会使用该符号。

若要删除断点，请使用 `delete` 命令并将断点号作为参数。

## 6.6.4 监视点 (Watchpoints)

监视点（Watchpoints）顾如其名，用于监视程序中的数据，特别是在特定地址的数据发生变化时向你报警。如果你程序中的某个变量由于某种奇怪且未知的原因发生变化，这可能是内存损坏的征象。由于内存损坏问题可能发生在症状（例如陷阱或异常行为）出现很久之前，因此追踪这类问题是极其困难的。通过监视点，你可以告诉 GDB 监视指定的变量，并在其变化时立即通知你。对于内存损坏，GDB 会确切告诉你损坏发生在何时和何时，以便你轻松解决问题。

监视点有两种类型——硬件和软件。例如，x86 硬件专门为监视点提供了内置支持，GDB 将利用这种支持。如果不存在该支持或不满足使用硬件的条件，GDB 将回退到软件监视点。软件监视点比硬件监视点慢得多。这是因为 GDB 必须在每条汇编指令后停止程序执行，并检查每个监视点是否有变化。相反，硬件监视点允许 GDB 正常运行，但在变化发生时（如果发生）会立即通知 GDB。

为了演示监视点，让我们使用一个模拟员工记录系统的简单程序。源代码如下：

```c
#include <stdio.h>

struct employee {
    char name[8];
    int serial_num;
}

void print_employee_rec( struct employee rec )
{
    printf("Name: %s\n", rec.name);
    printf("Number: %d\n", rec.serial_num);
    return;
}

void update_employee_name( struct employee *rec, char *name)
{
    strcpy(rec->name, name);
    return;
}
```

```c
void add_employee( struct employee *rec, char *name, int num ) {
    strcpy( rec->name, name );
    rec->serial_num = num;
    return;
}

int main( void ) {
    struct employee rec;
    add_employee(&rec, "Fred", 25 );
    print_employee_rec( rec);
    printf("\nUpdating employee's name ...\n\n" );
    update_employee_name(&rec, "Fred Smith" );
    print_employee_rec( rec);
    return 0;
}
```

程序的基本流程是创建一个名为 "Fred" 且序列号为 25 的员工记录。接下来，程序将员工姓名更新为 "Fred Smith"，但没有触碰序列号。运行程序产生如下输出：

```
penguin> employee

Name: Fred

Number: 25

Updating employee's name ...

Name: Fred Smith

Number: 26740
```
