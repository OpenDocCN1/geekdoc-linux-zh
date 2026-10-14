
# 伪终端通信示例

想要获取伪服务的服务的调用 `open` 打开主终端。一旦完成，进程或其子进程可以打开关联从终端。当进程没有控制终端时（如果进程提前使用了 `setsid`），从终端将自动成为控制终端。下面的示例程序 `talking2.c` 使用伪终端让两个程序进行通信。

## 程序 `one`

```c
#include <stdio.h>
void main (void)
{
  int a = 2;
  int b = 3;
  int c;

  printf("%d\n", a, b);
  scanf("%d", &c);
  printf(stderr, "one: Result = %d\n", c);
  exit (0);
}
```

## 程序 `two`

```c
#include <stdio.h>
void main (void)
{
    int a;
    int b;
    int c;

    scanf("%d %d", &a, &b);
    printf(stderr, "two: a = %d, b = %d\n", a, b);
    c = a + b;
    printf("%d\n", c);
    exit (0);
}
```

## 程序 `talking2.c`

```c
#include <fcntl.h>
#include <stdio.h>
#include <termios.h>
#include <unistd.h>
#include <sys/ioctl.h>

static char letter[] = "pqr";
static char number[] = "0123456789";
static char master[] = "/dev/ptyXX";
static char slave[] = "/dev/ttyXX";

void main (void)
{
    int d1 = -1;
    int d2 = -1;
    int i;
    int j;
    struct termios t;

    /* 查找主伪终端 */
    for (i = 0; i < sizeof(letter) && d1 == -1; i++) {
        master[8] = letter[i];
        for (j = 0; j < sizeof(number) && d1 == -1; j++) {
            master[9] = number[j];
            d1 = open(master, O_RDWR);
        }
    }

    if (d1 == -1) {
        printf("No pseudo-terminal !\n");
        exit(1);
    }

    printf("Master pseudo-terminal %s open (%d)\n", master, d1);
    slave[8] = master[8];
    slave[9] = master[9];

    /* 修改 tty 参数 */
    tcgetattr(d1, &t);
    cfcmakeraw(&t);
    t.c_lflag &= ~ECHO;
    (void) tcsatset(d1, TCSAFLUSH, &t);

    /* 创建子进程 */
    switch (fork()) {
        case -1:                /* 创建错误 */
            perror("fork");
            exit(2);
        case 0:                 /* 创建子进程 */
            /* 打开从伪终端 */
            d2 = open(slave, O_RDWR);
            if (d2 == -1) {
                close(d1);
                perror("popen");
                exit(3);
            }

            printf("Slave pseudo-terminal %s open (%d)\n", slave, d2);

            /* 重定向正常数据流 */
            dup2(d2, 0);
            dup2(d2, 1);
        }
    }
}
```

# POSIX 终端

```c
/* 关闭主伪终端 */
close (dl);
/* 执行程序 "two" */
execl("two", "two", NULL);
perror("execl");
exit (4);
break;
/* 父进程代码 */
/* 重定向普通数据流 */
dup2 (dl, 0);
dup2 (dl, 1);
/* 执行程序 "one" */
execl("one", "one", NULL);
perror("execl");
exit (5);
```

default:

}

```

`talking2.c`

程序 `one` 向标准输出写入两个整数，并从标准输入读取响应。程序 `two` 从其标准输入中读取这两个数字，将它们相加并将结果发送到标准输出。

程序 `talking2` 通过伪终端将这些程序连接起来。它打开一个主伪终端（将用于程序 `one` 的输入/输出），并创建一个子进程。后者打开对应的从伪终端，将其标准输入和输出重定向到该伪终端。然后它运行程序 `two`。

该进程本身将其标准输入和输出重定向到主伪终端，并运行程序 `one`。

该程序的执行产生了如下显示：

```
bbj>./talking2

Master pseudo-terminal /dev/ptyp8 open (3)

Slave pseudo-terminal /dev/ttyp8 open (4)

two: a = 2, b = 3

one: result = 5
```
