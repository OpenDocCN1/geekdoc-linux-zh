
为了获得最大的可移植性，我们使用了`difftime()`，它返回两个`time_t`值之间的差值（以秒为单位）。对于这个特定情况，像这样的转换

```
return (int) difftime(e1->start_date, e2->start_date);
```

应该也能奏效，因为`time_t`的值在合理范围内。尽管如此，为了安全起见，我们仍然使用完整的三路`if`语句。

以下是一个示例数据文件，列出了五位美国总统：

```
$ cat presdata.txt
Bush George 43 980013600  Last name, first name, president number, inauguration
Clinton William 42 727552800
Bush George 41 601322400
Reagan Ronald 40 348861600
Carter James 39 222631200
```

`ch06-sortemp.c`展示了一个简单的程序，该程序将此文件读入一个`struct employee`数组，然后使用刚才展示的两个不同的比较函数进行排序。

```c
1  /* ch06-sortemp.c ---  Demonstrate qsort() with two comparison functions. */
2
3  #include <stdio.h>
4  #include <stdlib.h>
5  #include <time.h>
6
7  struct employee {
8      char lastname[30];
9      char firstname[30];
10     long emp_id;
11     time_t start_date;
12 };
13
14 /* emp_name_id_compare ---  compare by name, then by ID */
15
16 int emp_name_id_compare(const void *e1p, const void *e2p)
17     {
... as shown previously, omitted to save space ...
39     }
40
41 /* emp_seniority_compare ---  compare by seniority */
42
43 int emp_seniority_compare(const void *e1p, const void *e2p)
44     {
... as shown previously, omitted to save space ...
58     }
59
60 /* main ---  demonstrate sorting */
61
62 int main(void)
63 {
64 #define NPRES 10
65 struct employee presidents[NPRES];
66 int i, npres;
67 char buf[BUFSIZ];
68
69 /* Very simple code to read data: */
70 for (npres = 0; npres < NPRES && fgets(buf, BUFSIZ, stdin) != NULL; npres++)
71 {
72   sscanf(buf, "%s %s %ld %ld", presidents[npres].lastname,
73          presidents[npres].firstname,
74          & presidents[npres].emp_id,
75          & presidents[npres].start_date);
76 }
77
78 /* npres is now number of actual lines read. */
79
80 /* First, sort by name */
81 qsort(presidents, npres, sizeof(struct employee), emp_name_id_compare);
82
83 /* Print output */
84 printf("Sorted by name:\n");
85 for (i = 0; i < npres; i++)
86 {
87   printf("%s %s\t%d\t%s", presidents[i].lastname,
88          presidents[i].firstname,
89          (int) presidents[i].emp_id,
90          ctime(& presidents[i].start_date));
91 }
92
93 /* Now, sort by seniority */
94 qsort(presidents, npres, sizeof(struct employee), emp_seniority_compare);
95
96 /* And print again */
97 printf("Sorted by seniority:\n");
98 for (i = 0; i < npres; i++)
99 {
100   printf("%s %s\t%d\t%s", presidents[i].lastname,
101          presidents[i].firstname,
102          (int) presidents[i].emp_id,
103          ctime(& presidents[i].start_date));
104 }
105
106 return 0;
107 }
```

第 70–77 行读取数据。请注意，任何使用`scanf()`的代码都需要输入数据“行为良好”。例如，如果任何姓名超过 29 个字符，就会出现问题。在这种情况下，我们是安全的，但在生产代码中必须更加小心。

第 82 行按姓名和员工 ID 对数据排序，然后第 84–91 行打印排序后的数据。类似地，第 94 行重新排序数据，这次按资历排序，第 97–103 行打印结果。编译并运行该程序后，输出结果如下：

### 6.2 排序和搜索函数

### 6.2.1 排序：`qsort()`

```bash
$ ch05-sortemp < presdata.txt
Sorted by name:

| Bush George | 41 | Fri Jan 20 13:00:00 1989 |
| Bush George | 43 | Sat Jan 20 13:00:00 2001 |
| Carter James | 39 | Thu Jan 20 13:00:00 1977 |
| Clinton William | 42 | Wed Jan 20 13:00:00 1993 |
| Reagan Ronald | 40 | Tue Jan 20 13:00:00 1981 |

Sorted by seniority:

| Carter James | 39 | Thu Jan 20 13:00:00 1977 |
| Reagan Ronald | 40 | Tue Jan 20 13:00:00 1981 |
| Bush George | 41 | Fri Jan 20 13:00:00 1989 |
| Clinton William | 42 | Wed Jan 20 13:00:00 1993 |
| Bush George | 43 | Sat Jan 20 13:00:00 2001 |
```

（我们使用下午 1:00 作为所有总统开始就职时间的近似值。²）

有一点值得一提：`qsort()`会重新排列数组中的数据。如果每个数组元素都是大型结构体，在排序过程中大量的数据会被来回复制。相反，建立一个小数组来存储指针可能更划算，每个指针指向原数组中的一个元素。然后使用`qsort()`对指针数组进行排序，并通过排序后的指针访问未排序的数据。
