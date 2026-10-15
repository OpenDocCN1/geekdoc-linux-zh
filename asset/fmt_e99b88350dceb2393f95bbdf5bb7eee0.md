
与线性搜索不同，二进制搜索要求输入数组已经排序。这里的缺点是，如果添加了元素，必须先重新排序数组才能进行搜索。（当元素被移除时，数组的剩余内容仍需向下移动填补空缺。这不像重新排序那么昂贵，但仍可能涉及大量数据移动。）

二进制搜索的优点，而且这是一个显著的优点，是它快得惊人，最多需要 $\log_2(N)$ 次比较，其中 $N$ 是数组中的元素数量。`bsearch()` 函数声明如下：

```c
#include <stdlib.h>  /* ISO C */
void *bsearch(const void *key, const void *base, size_t nmemb,
              size_t size, int (*compare)(const void *, const void *));
```

这些参数及其作用与 `qsort()` 的相似：

- `const void *key`

  这是在数组中搜索的对象。

- `const void *base`

  这是数组的起始位置。

- `size_t nmem`

  这是数组中的元素数量。

- `size_t size`

  这是每个元素的大小，通过 `sizeof` 获取。

- `int (*compare)(const void *, const void *)`

  这是比较函数。它必须像 `qsort()` 的比较函数一样工作，根据第一个参数小于/等于/大于第二个参数，返回负数/零/正数。

如果未找到该对象，`bsearch()` 返回 `NULL`。否则，它返回指向找到的对象的指针。如果有多个数组元素与 `key` 匹配，返回哪一个是不确定的。因此，与 `qsort()` 一样，请确保比较函数考虑了所搜索数据结构的所有相关部分。

`ch06-searchemp.c` 展示了 `bsearch()` 的实际应用，扩展了之前使用的 `struct employee` 示例。

```c
1 /* ch06-searchemp.c -- Demonstrate bsearch(). */
2
3 #include <stdio.h>
4 #include <errno.h>
5 #include <stdlib.h>
6
7 struct employee {
8     char lastname[30];
9     char firstname[30];
10    long emp_id;
11    time_t start_date;
12 };
13
14 /* emp_id_compare --- compare by ID */
15
16 int emp_id_compare(const void *e1p, const void *e2p)
17 {
18     const struct employee *e1, *e2;
19
20     e1 = (const struct employee *) e1p;
21     e2 = (const struct employee *) e2p;
22
23     if (e1->emp_id < e2->emp_id)
24         return -1;
25     else if (e1->emp_id == e2->emp_id)
26         return 0;
27     else
28         return 1;
29 }
30
31 /* print_employee --- print an employee structure */
32
33 void print_employee(const struct employee *emp)
34 {
35     printf("%s %s\t%d\t%s", emp->lastname, emp->firstname,
36            emp->emp_id, ctime(&emp->start_date));
37 }
```

第 7–12 行定义了 `struct employee`；它与之前相同。第 16–29 行作为比较函数，适用于 `qsort()` 和 `bsearch()`。它仅比较员工 ID 号。第 33–37 行定义了 `print_employee()`，这是一个便利函数，用于打印结构体，因为这是从多个地方进行的。

```c
39 /* main --- demonstrate sorting */
40
41 int main(int argc, char *argv)
42 {
43     #define NPRES 10
44     struct employee presidents[NPRES];
45     int i, npres;
46     char buf[BUFSIZ];
47     struct employee *the_pres;
48     struct employee key;
49     int id;
50     FILE *fp;
51
52     if (argc != 2) {
53         fprintf(stderr, "usage: %s datafile\n", argv[0]);
54         exit(1);
55     }
56
57     if ((fp = fopen(argv[1], "r")) == NULL) {
58         fprintf(stderr, "%s: %s: could not open: %s\n", argv[0],
59                 argv[1], strerror(errno));
60         exit(1);
61     }
62
63 /* Very simple code to read data: */
64 for (npres = 0; npres < NPRES && fgets(buf, BUFSIZ, fp) != NULL;
65 npres++) {
66 scanf(buf, "%s %s %ld %ld",
67 presidents[npres].lastname,
68 presidents[npres].firstname,
69 & presidents[npres].emp_id,
70 & presidents[npres].start_date);
71 }
72 fclose(fp);
73
74 /* npres is now number of actual lines read. */
75
76 /* First, sort by id */
77 qsort(presidents, npres, sizeof(struct employee), emp_id_compare);
78
79 /* Print output */
80 printf("Sorted by ID:\n");
81 for (i = 0; i < npres; i++) {
82 putchar('\t');
83 print_employee(& presidents[i]);
84 }
85
86 for (;;) {
87 printf("Enter ID number: ");
88 if (fgets(buf, BUFSIZ, stdin) == NULL)
89 break;
90
91 scanf(buf, "%d\n", & id);
92 key_emp_id = id;
93 the_pres = (struct employee *) bsearch(& key, presidents, npres,
94 sizeof(struct employee), emp_id_compare);
95
96 if (the_pres != NULL) {
97 printf("Found: ");
98 print_employee(the_pres);
99 } else
100 printf("Employee with ID %d not found!\n", id);
101 }
102
103 putchar('\n\n'); /* Print a newline on EOF. */
104
105 exit(0);
106 }
```

`main()` 函数以参数检查开始（第 52–55 行）。然后，它从指定文件中读取数据（第 57–72 行）。不能将标准输入用于员工数据，因为标准输入被保留用于提示用户输入要搜索的员工 ID。

第 77–84 行对数据进行排序，然后打印它们。然后程序进入一个循环，从第 86 行开始。它提示输入员工 ID 号，在遇到文件结尾时退出循环。为了搜索数组，我们使用名为 `key` 的 `struct employee`。只需设置其 `emp_id` 字段为输入的 ID 号即可；比较中不使用其他字段（第 92 行）。
