
```
/*
 * show_opt.c - demonstrate option processing with load_defaults()
 * and handle_options()
 */

#include <my_global.h>
#include <my_sys.h>
#include <mysql.h>
#include <my_getopt.h>

static char *opt_host_name = NULL; /* server host (default=localhost) */
static char *opt_user_name = NULL; /* username (default=login name) */
static char *opt_password = NULL; /* password (default-none) */
static unsigned int opt_port_num = 0; /* port number (use built-in value) */
static char *opt_socket_name = NULL; /* socket name (use built-in value) */

static const char *client_groups[] = { "client", NULL };

static struct my_option my_opts[] = { /* option information structures */
{
{ "help", '?', "Display this help and exit", NULL, NULL, NULL,
GET_NO_ARG, NO_ARG, 0, 0, 0, 0, 0, 0 },
{ "host", 'h', "Host to connect to", (uchar **) &opt_host_name, NULL, NULL,
GET_STR, REQUIRED_ARG, 0, 0, 0, 0, 0, 0 },
{ "password", 'p', "Password", (uchar *) &opt_password, NULL, NULL,
GET_STR, OPT_ARG, 0, 0, 0, 0, 0, 0 },
{ "port", 'P', "Port number", (uchar *) &opt_port_num, NULL, NULL,
GET_UINT, REQUIRED_ARG, 0, 0, 0, 0, 0, 0 },
{ "socket", 'S', "Socket path", (uchar **) &opt_socket_name, NULL, NULL,
GET_STR, REQUIRED_ARG, 0, 0, 0, 0, 0, 0 },
{ "user", 'u', "User name", (uchar **) &opt_user_name, NULL, NULL,
GET_STR, REQUIRED_ARG, 0, 0, 0, 0, 0, 0 }
{ NULL, 0, NULL, NULL, NULL, NULL, GET_NO_ARG, NO_ARG, 0, 0, 0, 0, 0, 0 }
};

static my_bool
get_one_option (int optid, const struct my_option *opt, char *argument)
{
switch (optid)
{
case '?':
my_print_help (my_opts); /* print help message */
exit (0);
}
return (0);
}

int
main (int argc, char *argv[])
{
```

## 注意

`show_opt.c` 及本章后续几个程序的源代码在 MySQL 相关的数据结构中使用了 `uchar**` 类型。在 MySQL 5.1.20 之前，你会发现 MySQL 头文件使用的是 `opt*`，这会导致编译程序时出现警告。你可以忽略这些警告。

`show_opt.c` 中展示的选项处理方案涉及了几个任何使用 MySQL 客户端库处理命令选项的程序都常见的方面。在你自己的程序中，你也应该做同样的事情：

1. 除了我们已经包含的其他文件外，还需包含 `my_getopt.h`。`my_getopt.h` 定义了 MySQL 选项处理设施的接口。

2. 定义一个 `my_option` 结构体数组。在 `show_opt.c` 中，这个数组命名为 `my_opts`。数组中应包含程序所理解的每个选项的一个结构体。每个结构体提供诸如选项的短名称和长名称、其默认值、值是数字还是字符串等信息。

3. 在调用 `load_defaults()` 读取选项文件并设置参数向量后，通过调用 `handle_options()` 来处理选项。`handle_options()` 的前两个参数是你的程序参数计数和向量的地址。（与 `load_options()` 类似，你传递的是这些变量的地址，而不是它们的值。）第三个参数指向 `my_option` 结构体数组。第四个参数是指向辅助函数的指针。`handle_options()` 例程和 `my_option` 结构体的设计使得大多数选项处理操作可以由客户端库自动为你执行。然而，为了允许库不处理的特殊操作，你的程序也应该定义一个供 `handle_options()` 调用的辅助函数。在 `show_opt.c` 中，这个函数名为 `get_one_option()`。

`my_option` 结构体定义了程序所理解的每个选项必须指定的信息类型：

```c
struct my_option
{
    const char *name;         /* option's long name */
    int         id;           /* option's short name or code */
    const char *comment;      /* option description for help message */
    uchar       **value;      /* pointer to variable to store value in */
    uchar       *u_max_value; /* The user defined max variable value */
    struct st_typeelib *typeelib; /* pointer to possible values (unused) */
    ulong       var_type;     /* option value's type */
    enum get_opt_arg_type arg_type; /* whether option value is required */
    longlong    def_value;    /* option's default value */
    longlong    min_value;    /* option's minimum allowable value */
    longlong    max_value;    /* option's maximum allowable value */
    longlong    sub_size;     /* amount to shift value by */
    long        block_size;   /* option value multiplier */
    void        *app_type;    /* reserved for application-specific use */
};
```

`my_option` 结构体的成员使用方式如下：

- `name` 是长选项名称。这是选项的 `--name` 形式，不包括前导破折号。例如，如果长选项是 `--user`，则在 `my_option` 结构中将其列示为 `user`。

- `id` 是短（单字符）选项名称，或者如果选项没有单字符名称，则是与该选项关联的代码值。例如，如果短选项是 `-u`，则在 `my_option` 结构中将其列示为 `'u'`。对于只有长名称而没有对应单字符名称的选项，你应该制定一组选项代码值，用于内部作为短名称使用。这些值必须唯一，且不同于所有单字符名称。（为满足后一个约束，使代码值大于 255，即最大的可能单字符值。关于此技术的示例，请参见第 7.6 节，“编写包含 SSL 支持的客户端”。）

- `comment` 是描述选项用途的解释字符串。这是你希望在帮助消息中显示的文本。
