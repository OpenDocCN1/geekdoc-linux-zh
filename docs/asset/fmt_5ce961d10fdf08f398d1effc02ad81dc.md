
图 6.5 显示了一个 `hello.c` 程序的 DDD 会话，该程序包含为局部变量赋值赋值的代码。源代码位于源代码窗口中。绿色箭头指向下一个执行的源代码行，因此我们可以看到我们刚刚执行了将值 5 存储到 `stack_int` 变量的代码。

# GNU 调试器 (GDB) 第 6 章

`GDB: /home/user/bin/gdb --shared-library-path ...`

文件 编辑 查看 程序 命令 状态 数据 帮助

`(gdb) x/16xwisp`

`0x00018420 0x00000005 0xbffffe28 0x00400d17`

`0xbfff2270 0x00000001 0xbfff2fbc 0x004019b4`

`0xbfff2280 0x00000001 0x004082a0 0x004082a1`

`0xbfff2281 0x0040833c 0x00000001 0xbfff22b4`

```c
int main ( ) {
    int stack_int = 3;
    printf("DDD is a wonderful GUI frontend to GDB!\n");
    stack_int = ;
    return (0);
}
```

```
0x00408345 <main+9>:  mov     $0, %eax
0x0040834a <main+14>:  sub     $0x10, %esp
0x0040834e <main+18>:  mov     $0x3,%ffffffff(%esp)
0x00408353 <main+27>:  push    0x004082c0
0x00408357 <main+32>:  mov     %eax,(%di)
0x0040835c <main+36>:  add     $0x10, %esp
0x00408363 <main+43>:  mov     $0x5,%ffffffff(%esp)
0x0040836e <main+46>:  mov     %esp,%eax
0x0040836f <main+47>:  leave
0x00408370 <main+52>:  ret
```

`(gdb) print "x/16xwisp"`
`(gdb) next`
`(gdb) next`
`DDD is a wonderful GUI frontend to GDB!`
`(gdb) stepi`
`> Updating status displays...done.`

图 6.5 原始堆栈跟踪

## 6.12 数据显示调试器 (DDD)

### 6.12.2 查看复杂数据结构

数据窗口在显示和组织复杂数据结构方面也非常强大。链表是计算机科学的一种基础数据结构，但当特定的实现变得非常复杂时，调试它们可能会困难。图 6.6 显示了一个 DDD 会话，该会话在我们的 `hello.c` 源文件中添加了一个简单的链表实现。源代码如下：

```c
#include <stdio.h>
struct linked_list_struct {
    int list_node;
    int data;
    struct linked_list_struct *pNext;
}
```

```c
int main ( void ) {
```

```c
int stack_int = 3;
char stack_string[16];
struct linked_list_struct *node1 = (struct
    linked_list_struct*)malloc(sizeof(
    struct linked_list_struct ) );
struct linked_list_struct *node2 = (struct
    linked_list_struct*)malloc(sizeof(
    struct linked_list_struct ) );
struct linked_list_struct *node3 = (struct
    linked_list_struct*)malloc(sizeof(
    struct linked_list_struct ) );
node1->list_node = 1;
node1->data = 9234;
node1->pNext = node2;
node2->list_node = 2;
node2->data = 2342;
node2->pNext = node3;
node3->list_node = 3;
node3->data = 7987;
node3->pNext = node1;
printf(" DDD is a wonderful GUI frontend to GDB!\n" );
stack_int = 5;
return ( 0 );
```
