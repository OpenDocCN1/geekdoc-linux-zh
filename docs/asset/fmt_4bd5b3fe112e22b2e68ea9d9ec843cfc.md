
```c
/* dict.cpp - main, initw, nextin, insertw, deletew, lookupw */

#include <stdio.h>
#include <ctype.h>
#include <string.h>

#define MAXWORDLEN 50 /* * 命令或单词的最大长度 */
#define DICTSSIZ 100 /* * 字典中条目的最大数量.*/
char dict[DICTSSIZ][MAXWORDLEN+1];/* 单词字典存储*/
int nwords = 0; /* * 字典中的单词数 */

int nextin(char *, char *), initw(), insertw(const char *);
int deletew(const char *), lookupw(const char *);

/*
 * main - 按照指定在字典中插入、删除或查找单词
 */
int
main(int argc, char *argv[]) {
	char word[MAXWORDLEN+1]; /* 存储输入行中单词的空间*/
	char cmd;
	int wrdlen; /* * 输入单词的长度 */

	while (1) {
		wrdlen = nextin(&cmd, word);
		if (wrdlen < 0)
		exit(0);
		word[wrdlen] = '\0';
		switch (cmd) {
```

### 22.5 步骤 1：构建应用程序（继续）

```c
/* nextin - 从下一行读取命令（以及可能的单词） */
int nextin(char *cmd, char *word) {
    int i, ch;
    while ((ch = getchar()) != EOF) {
        if (isspace(ch)) {
            if (i > 0) {
                word[i] = '\0';
                *cmd = ch;
                return i;
            }
            continue;
        }
        if (i >= MAXWORDLEN) {
            printf("error: word too long.\n");
            exit(1);
        }
        word[i++] = ch;
    }
    return -1;
}

/* initw - 初始化字典不包含任何单词 */
int initw() {
    nwords = 0;
    return 0;
}

/* insertw - 在数组末尾插入新单词 */
int insertw(const char *word) {
    strcpy(dict[nwords], word);
    nwords++;
    return 1;
}

/* deletew - 查找要删除的单词。如果找到，
 * 用字典中的最后一个单词替换它并减少 nwords。 */
int deletew(const char *word) {
    int i;
    for (i = 0; i < nwords; i++) {
        if (strcmp(dict[i], word) == 0) {
            strcpy(dict[i], dict[nwords-1]);
            nwords--;
            return 1;
        }
    }
    return 0;
}

/* lookup - 顺序查找数组以确定指定的单词是否存在 */
int lookup(const char *word) {
    int i;
    for (i = 0; i < nwords; i++) {
        if (strcmp(dict[i], word) == 0)
            return 1;
    }
    return 0;
}
```

## 22.6 步骤 2：将程序分为部分

一旦构建并测试了常规应用程序，就可以将其划分为本地和远程组件。程序员在划分程序之前，必须对程序的调用图有一个概念模型。例如，图 22.2 显示了原始字典应用程序的过程组织。

![](img/7fd1ea9db2b1f52482f69f28c8dd336d_300_0.png)

图 22.2 解决字典问题的原始常规程序的调用图。调用图表示程序的过程组织。

在考虑将程序移动到远程机器时，程序员必须考虑每个程序所需的设施。例如，`nextin` 程序在每次调用时都会读取并解析下一行输入。由于它需要访问程序的标准输入文件，`nextin` 必须与主程序放在一起。总结来说：

执行 I/O 或其他方式访问文件描述符的程序无法轻易移动到远程机器。

## 第 22.6 节 第 2 ：将程序分为两部分

程序员还必须考虑每个过程访问的数据的位置。例如，`lookup` 过程需要访问整个单词数据库。如果 `lookup` 在字典所在的机器以外的机器上发生，那么用于 `lookup` 的 RPC 调用必须将整个字典作为参数传递。

将大型数据结构作为参数传递给远程过程是非常低效的，因为 RPC 机制必须为每个远程过程调用读取并编码整个数据结构。通常情况下：

过程应该在与其访问的数据相同的机器上执行。将大型数据结构作为参数传递给远程过程是低效的。

在考虑了原始字典程序以及每个过程访问的数据后，显而易见，`insertw`、`deletew`、`initw` 和 `lookupw` 属于字典本身所在的机器。

假设程序员决定将字典存储和相关过程移动到远程机器。为了帮助理解将某些过程移动到远程机器的结果，程序员通常会对分布式程序和数据结构建立构想，甚至画一张草图。图 22.3 展示了字典应用程序的新结构，其中数据和访问过程已移动到远程机器。

![](img/7fd1ea9db2b1f52482f69f28c8dd336d_301_0.png)

图 22.3 字典程序分为本地和远程组件的概念性划分。远程组件包含字典的数据以及访问和搜索数据的过程。

像图 22.3 这样的简单图形可以帮助程序员思考将程序分为本地和远程组件。程序员必须考虑每个过程是否能够访问其所需的数据和服务，并且必须考虑每个远程过程将所需的参数，以及跨网络传递这些信息的成本。最后，该图可以帮助程序员评估网络延迟将如何影响程序性能。

假设程序员选择了一种概念性的划分并决定继续，下一步是将源程序分为两个组件。程序员识别每个组件使用的常量和数据结构，并将每个组件放在单独的文件中。以字典为例，这种划分非常直接，因为原始源文件可以在 `nextin` 过程和 `insertive` 过程之间进行划分。文件 `dict1.cpp` 包含主程序和 `nextin` 过程：

```cpp
/* dict1.cpp - main, nextin */
```

```cpp
#include <stdlib.h>
#include <stdio.h>
#include <ctype.h>
```

```cpp
#define MAXWORDLEN 50    /*一个命令或单词的最大长度 */
```

```cpp
int nextin(char *, char *), initw(void), insertw(char *),
deletew(char *), lookupw(char *);
```

```cpp
/*-----------------------------------------------------------------
* main - 按指定在字典中插入、删除或查找单词
------------------------------------------------------------------------------*/
```
