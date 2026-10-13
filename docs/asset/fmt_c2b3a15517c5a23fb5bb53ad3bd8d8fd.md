
Starting program: `/home/ray/testaddme./.addem` `supercalifragilisticizowie`

cn't open file `supercalififra` please try again

Program exited with code `01`.

`(gdb)`

```
```

所以基本上说的是同样的话。但一定还有更多你可以发现的东西。尝试查看代码，看看你是否能找出那个奇怪的截断是从哪里。

```c

(gdb) 1

14 int `argc`;

15 char *`argv`[];

16 {

17 int i;

18 char `infile`[8];

19 int `_`;

20 FILE *`infile`;

21 char `number`[100];

22 char *`filename2`=`filename`;

23 `strcpy`(`filename2`,`argv`[1]);

(gdb)

24 i=0; j=0;

25 `infile` = `fopen`(`filename2`,"r");

26

27 if(`infile`==NULL)

28 {

29 `printf`("couldn't open file %s please try again\n",

30 --`filename2`);

31 `exit`(1);

32 }

33 i=0;

(gdb)

```

第 29 行似乎是错误消息的来源。设置一个断点看看会发生什么。

```bash

(gdb) b 29

Breakpoint 1 at 0x2374: file `addme.c`, line 29.

(gdb) r

Starting program: `/home/ray/testaddme./.addem` `addme.c`

Breakpoint 1, `main`(`argc`=2, `argv`=0x7ff2c) at `addme.c`:29

`printf`("couldn't open file %s please try again\n",

--`filename2`);

(gdb)

```

第 29 行似乎是错误消息的源头。等等发生了什么？在执行处 `infilename2` 应该是 `supercalifragistic`。

这里非常不对劲！是时候回到第 23 行断点，从往下观察发生了什么。

```bash

(gdb) b 23

Breakpoint 2 at 0x2374: file `addme.c`, line 23.

(gdb) r

Starting program: `/home/ray/testaddme./.addem` `addme.c` `supercalifragisticizowie`

Breakpoint 2, `main`(`argc`=2, `argv`=0x7ff2c) at `addme.c`:23

  `strcpy`(`filename2`,`argv`[1]);

(gdb) p `argv`[1]

$1 = 0xff7ff "supercalifragisticowie"

(gdb)

```

所以之前的元凶不是这里。这里没有阻止文件名进入程序。

```bash

(gdb) p `filename2`

$2 = "\000\000\000\000"

(gdb)

```

这里没什么有趣的。看看下一行发生了什么——使用 `gdb` 命令 `n` 跳到下一行。当你跳到下一行时，这一行执行了，所以你应该预期在向前执行后看到结果。

```bash

(gdb) n

24    i=0; j=0;

(gdb) p `filename2`

$1 = 0xfffff6b0 "supercalifragisticowie"

(gdb)

```

正如预期的那样，`filename2` 包含了那个著名的长文件名。这里没有问题。当它到达 29 行时，它坏了，所以再次向前执行看看会发生什么。

```bash

(gdb) n

25    `infile` = `fopen`(`filename2`,"r");

(gdb) p `filename2`

$3 = 0xfffff6b0 "supercalifragifra"

(gdb)
