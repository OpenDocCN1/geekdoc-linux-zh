
6. 使用 `strtok` 将指针插入参数数组。

```c
free(t);
else {
  strcpy(t, s);
  *argvp = strtok(t, delimiters);
  for (int i = 1; i < numtokens; i++) {
    (*argvp)[i] = strtok(NULL, delimiters);
  }
  return numtokens;
}
(*argvp)[numtokens] = NULL; /* 放入最后的 NULL 指针 */
```

# 示例 2.19 freemakeargv.c

以下函数释放由 `makekargv` 分配的参数数组的所有内存。如果数组中的第一个元素不是 NULL，则释放该元素也会释放为所有字符串分配的内存。接下来会释放参数数组。请注意，释放参数数组后再访问第一个元素是错误的。

```c
#include <stdlib>

void freemakeargv(char **argv) {
  if (argv == NULL) {
    return;
  }
  if (*argv != NULL) {
    free(*argv);
  }
  free(argv);
}
```

### 2.7 线程安全的函数

`strtok` 并不是你应该在程序中模拟的模型。由于它的定义（第 35 页），它必须使用一个内部静态变量来跟踪字符串中下一个待解析标记的当前位置。然而，当在同一个程序中对不同的字符串调用 `strtok` 时，各自字符串的解析可能会相互干扰，因为位置信息只有一个变量。

程序 2.3 显示了如何使用 `strtok` 计算每行的平均单词数。`wordaverage` 函数通过使用 `strtok` 找到下一行来确定每行的平均单词数。然后它调用 `count` 来统计该行的单词数。遗憾的是，`wordcount` 使用了 `strtok`，这次是用来解析该行的单词。如果另一个函数不调用它，这两个函数都是正确的，但 `strtok` 会为第二行调用 `wordaverage`；此时 `strtok` 的内部状态信息已被 `wordcount` 重置。

导致 `wordaverage` 失败的行为使其无法在多线程程序中被安全地使用。如果一个线程正在使用 `strtok`，而另一个线程调用了它，POSIX 定义了一个线程安全的函数 `strtok_r` 用来代替 `strtok`。`_r` 代表可重入（reentrant），这个术语表示函数在之前的调用完成之前可以被重新重入（再次调用）。

### 程序 2.3 wordaverage.c

一种错误使用 `strtok` 来确定每行的平均单词数。

```c
#include <string.h>
#define LINE_DELIMITERS "\n"
#define WORD_DELIMITERS " "

static int wordcount(char *s) {
    int count = 1;
    char *lasts;

    if (strtok_r(s, WORD_DELIMITERS, &lasts) == NULL) {
        return 0;
    }
    while (strtok_r(NULL, WORD_DELIMITERS, &lasts) != NULL) {
        count++;
    }
    return count;
}

double wordaverage(char *s) { /* 返回 s 中单词的平均大小 */
    char *lasts;
    int linecount = 1;
    char *nextline;
    int words;

    nextline = strtok_r(s, LINE_DELIMITERS, &lasts);
    if (nextline == NULL)
      return 0.0;
    words = wordcount(nextline);
    while ((nextline = strtok_r(NULL, LINE_DELIMITERS, &lasts)) != NULL) {
      words += wordcount(nextline);
      linecount++;
    }
    return (double)words/linecount;
}
```

### 程序 2.4 wordaverage.c

`strtok_r` 函数的行为与 `strtok` 类似，多了一个参数 `lasts`，这是一个用户提供的指针，`strtok_r` 用它来存储下次解析的起始地址。

```c
#include <string.h>
char *strtok_r(char *restrict s, const char *restrict sep, char **restrict lasts);
```

每次调用 `strtok_r` 都会返回下一个标记的开头，并在返回的标记结尾插入一个 '\0'。当 `strtok_r` 到达 `s` 的末尾时返回 NULL。程序 2.4 通过使用 `strtok_r` 修正了 2.3。请注意，每个函数使用的标识符 `lasts` 是不同的，因此这两个函数为 `strtok_r` 的第三参数使用了不同的变量，互不干扰。

### 2.8 静态变量的使用

虽然在多线程的情况下使用静态变量时必须小心，但静态变量是有用的。例如，静态变量可以在函数调用之间保存内部状态信息。

程序 2.5 显示了一个名为 `bubblesort` 的函数，以及一个用于跟踪交换次数的辅助函数。变量 `count` 具有静态存储类，因为它是在任何块之外声明的。`static` 修饰符强制该变量具有内部链接，保证了 `bubblesort.c` 中的任何函数都无法直接访问 `count` 变量。`clearcount` 函数和 `onepass` 函数中的交换是修改 `count` 的唯一片段。内部链接允许其他与 `bubblesort.c` 链接的函数使用相同的标识符 `count`，而不会与此文件中的整数 `count` 冲突。

`clearcount`、`getcount` 和 `bubblesort` 这三个函数具有外部链接，可以从外部访问。注意 `onepass` 的 `static` 修饰符使该函数具有内部链接，因此无法从该文件外部访问。通过使用适当的存储类和链接类，`bubblesort` 向其调用者隐藏了它的实现细节。

### 程序 2.5 bubblesort.c

一个对整数数组进行排序并统计过程中交换数的函数。

```c
static int count = 0;

static int onepass(int a[], int n) { /* 如果发生了交换则返回 true */
    int i;
    int interchanges = 0;
    int temp;

    for (i = 0; i < n - 1; i++)
        if (a[i] > a[i+1]) {
            temp = a[i];
            a[i] = a[i+1];
            a[i+1] = temp;
            interchanges = 1;
            count++;
        }
    return interchanges;
}

void clearcount(void) {
    count = 0;
}

int getcount(void) {
    return count;
}

void bubblesort(int a[], int n) {
    int i;
    for (i = 0; i < n; i++) {
        if (!onepass(a, n))
            break;
    }
}
```

### 2.9 静态对象的结构

（注：原文此部分存在大量重复的文本，已根据要求翻译并保持结构）

静态变量在 C 程序中非常常用。此节实现了一个列表对象。该列表的实现既具有挑战性又有趣。列表的每个元素包含一个类型和一个任意长度的字符串。用户可以在列表中存储项并遍历列表以检查内容。用户不能修改放入列表的数据。该列表对于记录已执行的命令列表的操作非常有用。（此处省略后续重复内容，翻译逻辑保持一致）

```c
#include <time.h>

typedef struct data_struct {
    time_t time;
    char *string;
} data_t;

int accessdata(void);
int adddata(data_t data);
int freekey(int key);
int getdata(int key, data_t *xtap);
```

项目 2.7 展示了一个列表对象的实现。`adddata` 函数将数据项的副本插入到列表末尾。`getdata` 函数使用 `data_t` 将列表遍历中的下一个项拷贝到用户提供的缓冲区中。`getdata` 函数为该数据缓冲区中 `string` 字段的副本分配内存，由调用者负责释放该内存。

`accessdata` 函数返回一个用于遍历数据列表的整数键（key）。每个键值都会产生一个从列表开始的独立遍历。当不再需要该键值时，调用者可以通过调用 `freekey` 释放键值资源。当 `getdata` 为 *xtap* 的 `string` 字段返回 `NULL` 指针时，表示没有更多条目待检查，键值也会被释放。在到达列表末尾后请勿调用 `freekey`。

如果成功，`accessdata` 返回一个有效的非键值。其他函数在成功时返回 0。如果失败，这些函数将返回 -1 并设置 `errno`。

### 项目 2.7 listlib.c

一个列表对象的实现。

```c
#include <stdlib>
#include <string.h>
#include "listlib.h"
#define TRAV_INIT_SIZE 8
```

```c
typedef struct list_struct {
    data_t item;
    struct list_struct *next;
} list_t;
```

```c
static list_t *headptr = NULL;
static list_t *tailptr = NULL;
static list_t **varptrs = NULL;
static int travpparams_size = 0;
```

```c
int accessdata(void) {
    int i;
    list_t **newptrs;
    /* 如果成功则返回一个非负键 */
    if (headptr == NULL) { /* 无法访问完全空的列表 * }
        errno = -1;
        return -1;
    }
    if (travptrs_size == 0) { /* 第一次遍历 * }
        travptrs = (list_t **)calloc(TRAV_INIT_SIZE, sizeof(list_t));
        if (travptrs == NULL) { /* 无法为遍历键分配空间 * }
            return -1;
        }
        travptrs[0] = headptr;
        travptrs_size = TRAV_INIT_SIZE;
        return 0;
    }
    for (i = 0; i < travptrs_size; i++) { /* 为键寻找空位 * }
        if (travptrs[i] == NULL) {
            travptrs[i] = headptr;
            return 1;
        }
    }
    newptrs = realloc(travptrs, 2*travptrs_size*sizeof(list_t));
    if (newptrs == NULL) { /* 无法扩展遍历键数组 * }
        return -1;
    }
    travptrs = newptrs;
    travptrs[travptrs_size] = headptr;
    travptrs_size *= 2;
    return travptrs_size/2;
}

int adddata(data_t data) { /* 为数据分配节点并添加到列表末尾 * }
    list_t *newnode;
    int nodesize;

    nodesize = sizeof(list_t) + strlen(data.string) + 1;
    if ((newnode = (list_t *)(malloc(nodesize))) == NULL) { /* 无法添加节点 * }
        return -1;
    }
    newnode->time = data.time;
    newnode->item.string = (char *)newnode + sizeof(list_t);
    strncpy(newnode->item.string, data.string);
    newnode->next = NULL;
    if (headptr == NULL) {
        headptr = newnode;
    } else {
        tailptr->next = newnode;
        tailptr = newnode;
    }
    return 0;
}

int getdata(int key, data_t *datap) { /* 拷贝下一个项并设置 datap->string * */
    list_t *t;

    if ((key < 0) || (key >= travptrs_size) || (travptrs[key] == NULL)) {
        errno = EINVAL;
        return -1;
    }
    if (travptrs[key] == &endlist) { /* 列表结束，将 datap->string 设为 NULL * }
        datap->string = NULL;
    }
    travptrs[key] = NULL;
    return 0;
    /* 到达列表结束的自然情况，不是错误 */
    t = travptrs[key];
    datap->string = (char*)malloc(strlen(t->item.string) + 1);
    if (datap->string == NULL) /* 无法为返回的字符串分配空间 * }
        return -1;
    datap->time = t->item.time;
    strcpy(datap->string, t->item.string);
    if (t->next == NULL)
        travptrs[key] = &endlist;
    else
        travptrs[key] = t->next;
    return 0;
}

int freekey(int key) { /* 释放键对应的列表项 * }
    if ((key < 0) || (key >= travptrs_size)) { 
        errno = EINVAL; /* 键越界 * }
        return -1;
    }
    travptrs[key] = NULL;
    return 0;
}
```

项目 2.7 的实现没有假设 `data_t` 中 `string` 字段的上限限制。`adddata` 函数向包含数据的内部列表结构追加内容。`malloc` 在一个连续块中为 `list_t` 及其字符串数据分配空间。`adddata` 失败的唯一方法是资源无法提供额外的访问流。`accessdata` 函数如果传递的键无效或已释放，也会失败。`freekey` 在键无效时会失败。到达列表遍历末尾是一个自然现象，而不是错误。`getdata` 函数将 *datap* 的字符串字段设为 `NULL` 以指示结束。

项目 2.7 的实现使用键作为遍历数组的索引。指针以较小的初始大小动态分配数组。当遍历次数超过数组大同时，`accessdata` 调用 `realloc` 来扩展数组。

该对象的数据结构和列表的访问函数位于同一个文件中。随后的多个项目使用了此列表对象或类似的对象。在对象表示法中，外部调用者不应访问对象的内部表示。例如，它们不应该意识到该对象使用的是链表而不是数组或其他抽象数据结构的实现。

项目 2.7 的实现允许嵌套或递归调用以向列表添加数据或独立地遍历列表。然而，这些函数包含在多线程环境中必须保护的临界区域。第 13.2.3 节和 13.6 节讨论了如何这样做。

### 练习 2.21

如果在项目 2.7 中尝试访问空列表会发生什么？

### 答

`accessdata` 返回 -1，表示发生错误。

```c
if (system(cmd) == -1) /* command could not be executed at all */
    return -1;
return execute;
}
```
