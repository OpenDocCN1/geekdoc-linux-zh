

fprintd stderr, "ERROR: Unable to open %s\n", argv[1]);
    return(1);
}

fprintf(stdout, "DUMP OF FILE %s\n", strupr(argv[1]));

counter = 0;

while(1)
{
    /* Set buffer to zero bytes */
    memset(vl, 0, 20);

    /* Read buffer from file */
    x = __read(fl, &vl, 16);

    /* x will be 0 on EOF or -1 on error */
    if (x < 1)
        break;

    /* Print file offset to stdout */
    fprintf(stdout, "%06d(%05x) ", counter, counter);

    counter += 16;

    /* print hex values of buffer to stdout */
    for(n = 0; n < 16; n++)
        fprintf(stdout, "%02x ", vl[n]);

    /* Print ascii values of buffer to stdout */
    for(n = 0; n < 16; n++)
    {
        if ((vl[n] > 31) && (vl[n] < 128))
            fprintf(stdout, "%c", vl[n]);
        else
            fputs(".", stdout);
    }

    /* Finish the line with a new line */
    fputs("\n", stdout);
}

/* successful termination */
return(0);
}

## 字符串

C 语言拥有通用计算机语言中最强大的字符串处理能力之一。字符串是一个由零字节（null byte）终止的一维字符数组。字符串可以通过两种方式进行初始化：一是在源代码中直接赋值常亮值，例如：

```c
int main() {
    char *p = "System 5";
    char name[] = "Test Program";
}
```

或者在运行时通过 `strcpy()` 函数进行初始化，其函数原型为：

```c
char *strcpy(char *destination, char *source);
```

`strcpy()` 函数将源字符串复制到目标位置，如下例所示：

```c
#include <stdio.h>

int main()
{
    char name[50];

    strcpy(name, "Servile Software");

    printf("\nName equals %s", name);
}
```

C 语言还允许直接访问字符串中的每一个字节：

```c
#include <stdio.h>

int main()
{
    char name[50];

    strcpy(name, "Servile Software");

    printf("\nName equals %s", name);

    /* Replace first byte with lower case 's' */
    name[0] = 's';

    printf("\nName equals %s", name);
}
```

某些 C 编译器包含用于将字符串转换为大写和小写的函数，但这些函数并未在 ANSI 标准中定义。然而，ANSI 标准确实定义了 `toupper()` 和 `tolower()` 函数，它们分别将整数参数转换为大写和小写。通过利用这些函数，你可以创建符合 ANSI 标准的自定义版本：

```c
#include <stdio.h>

void strupr(char *source)
{
    char *p;

    p = source;
    while (*p)
    {
        *p = toupper(*p);
        p++;
    }
}

void strlwr(char *source)
{
    char *p;

    p = source;
    while (*p)
    {
        *p = tolower(*p);
        p++;
    }
}

int main()
{
    char name[50];

    strcpy(name, "Servile Software");
    printf("\nName equals %s", name);

    strupr(name);

    printf("\nName equals %s", name);

    strlwr(name);

    printf("\nName equals %s", name);
}
```

与其他计算机语言不同，C 语言没有规定字符串的最大长度限制。不过，某些 CPU 对内存块的最大尺寸有特定限制。以下是一个示例程序，用于反转字符串中所有字符的顺序：

```c
#include <stdio.h>
#include <string.h>

char *strrev(char *s)
{
    /* Reverses the order of all characters in a string except the null */
    /* terminating byte */

    char *start;
    char *end;
    char tmp;

    /* Set pointer 'end' to last character in string */
    end = s + strlen(s) - 1;

    /* Preserve pointer to start of string */
    start = s;

    /* Swop characters */
    while(end >= s)
    {
        tmp = *end;
        *end = *s;
        *s = tmp;
        end--;
        s++;
    }
    return(start);
}

int main()
{
    char text[100];
    char *p;

    strcpy(text, "This is a string of data");

    p = strrev(text);

    printf("\n%s", p);
}
```

### strtok()

`strtok()` 函数是从单个字符串中提取子字符串的非常强大的标准 C 特性。它适用于子字符串由已知分隔符（例如以下示例中的逗号）分隔的情况：

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char data[50];
    char *p;

    strcpy(data, "RED,ORANGE,YELLOW,GREEN,BLUE,INDIGO,VIOLET");

    p = strtok(data, ",");
    while(p)
    {
        puts(p);
        p = strtok(NULL, ",");
    };
}
```

可以使用 `for()` 循环编写该程序的一个变体：

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char data[50];
    char *p;

    strcpy(data, "RED,ORANGE,YELLOW,GREEN,BLUE,INDIGO,VIOLET");

    for(p = strtok(data, ", "); p; p = strtok(NULL, ", "))
    {
        puts(p);
    };
}
```

首先，你调用 `strtok()` 并传入要解析的字符串变量名称，以及包含已知分隔符的第二个字符串。然后，`strtok()` 返回指向第一个子字符串起始位置的指针，并将第一个分隔符替换为零字符。随后可以在循环中多次调用 `strtok()`，传入 `NULL` 作为要解析的字符串；`strtok()` 将返回后续的子字符串。由于 `strtok()` 在第二个参数字符串中可以接受多个分隔符字符，因此可以将其作为简单的单词计数程序的基础：

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void main(int argc, char *argv[])
{
    FILE *fp;
    char buffer[256];
    char *p;
    long count;

    if (argc != 2)
    {
        fputs("\nERROR: Usage is wordcnt <file>\n", stderr);
        exit(0);
    }

    /* Open file for reading */
    fp = fopen(argv[1], "r");

    /* Check the open was okay */
    if (!fp)
    {
        fputs("\nERROR: Cannot open source file\n", stderr);
        exit(0);
    }

    /* Initialize word count */
    count = 0;

    do
    {
        /* Read a line of data from the file */
        fgets(buffer, 255, fp);

        /* check for an error in the read or EOF */
        if (ferror(fp) || feof(fp))
            continue;

        /* count words in received line */
        /* Words are defined as separated by the characters */
        /* \t(tab) \n(newline) , ; : . ! ? ( ) - and [space] */
        p = strtok(buffer, "\t\n,;:!.?() - ");
        while(p)
        {
            count++;
            p = strtok(NULL, "\t\n,;:!.?() - ");
        }
    } while(!ferror(fp) && !feof(fp));

    /* Finished reading. Was it due to an error? */
    if (ferror(fp))
    {
        fputs("\nERROR: Reading source file\n", stderr);
        fclose(fp);
        exit(0);
    }

    /* Reading finished due to EOF, quite valid so print count */
    printf("\nFile %s contains %ld words\n", argv[1], count);
    fclose(fp);
}
```

## 数字与字符串之间的转换

所有 C 编译器都提供将数字转换为字符串的功能，例如 `sprintf()`。然而，`sprintf()` 是一个多功能函数，意味着它的体积较大且运行速度较慢。可以使用 `ITOS()` 函数来替代，因为它接受两个参数：第一个是有符号整数，第二个是指向字符字符串的指针。然后将整数复制到字符指针所指向的内存中。与 `sprintf()` 一样，`ITOS()` 也不检查目标字符串是否足够长以容纳转换结果。一个将带符号整数复制到字符串的示例函数如下：

```c
void ITOS(long x, char *ptr)
{
    /* Convert a signed decimal integer to a string */

    long pt[9] = { 100000000, 10000000, 1000000, 100000, 10000, 1000, 100, 10, 1 };
    int n;

    /* Check sign */
    if (x < 0)
    {
        *ptr++ = '-';
        /* Convert x to absolute */
        x = 0 - x;
    }
    for (n = 0; n < 9; n++)
    {
        if (x >= pt[n])
        {
            *ptr++ = '0' + x / pt[n];
            x %= pt[n];
        }
    }
    *ptr = '\0';
    return;
}
```

要将字符串转换为浮点数，C 语言提供了两个函数：`atof()` 和 `strtod()`；`atof()` 的原型为：

```c
double atof(const char *s);
```

而 `strtod()` 的原型为：

```c
double strtod(const char *s, char **endptr);
```

这两个函数都会扫描字符串并尽可能地进行转换，直到遇到它们无法理解的字符为止。这两个函数的区别在于，如果给 `strtod()` 传入参数 `endptr` 的字符指针，它会设置该指针指向终止转换的第一个字符。由于通过 `endptr` 提供了更好的错误报告机制，`strtod()` 通常比 `atof()` 更受青睐。

要将字符串转换为整数，可以使用 `atoi()`；其原型为：

```c
int atoi(const char *s);
```

请注意，`atoi()` 不检查溢出，且结果未定义。`atol()` 函数与之类似，但返回类型为 long。或者，可以使用 `strtol()` 和 `strtoul()` 代替，以获得更好的错误检查。

## 文本处理

人类将信息记录为“文本”，由单词、数字和标点符号组成；单词由大写字母和小写字母组合构成，具体取决于其语法用法。因此，使用计算机处理文本是一项困难但又常见的需求。ANSI C 定义包含字符串处理函数，这些函数天然区分大小写；也就是说，大写字母 A 被视为与小写字母 a 不同。这是程序员必须克服的第一个问题。幸运的是，Borland 的 Turbo C 编译器和 Microsoft 的 C 编译器都包含不区分大小写的字符串函数形式。

例如，`stricmp()` 是 `strcmp()` 的不区分大小写形式，而 `strnicmp()` 是 `strncmp()` 的不区分大小写形式。如果你担心编写可移植的代码，则必须限制自己仅使用 ANSI C 函数，并使用提供的工具编写自己的不区分大小写函数。

