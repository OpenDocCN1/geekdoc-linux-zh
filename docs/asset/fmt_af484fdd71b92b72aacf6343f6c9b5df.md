
```
                        puts("*");

                    else

                        putchar('\n');

                }

            }

            else

                for (m = 0, choice = option->choices; m > 0; m--, choice++)

                {

                    printf("%s (%s) = %d\n", choice->choice, choice->text);

                    if (strcmp(option->defchoice, choice->choice) == 0)

                        puts("*");

                    else

                        putchar('\n');

                }

            }

        }

    }

}
```

## 列表 14.4 延续

```
ppd->profiles[j].matrix[0][2], ppd->profiles[j].matrix[1][0],
ppd->profiles[j].matrix[1][1], ppd->profiles[j].matrix[1][2],
ppd->profiles[j].matrix[2][0], ppd->profiles[j].matrix[2][1],
ppd->profiles[j].matrix[2][2];
printf("num_fonts = %d\n", ppd->num_fonts);
for (j = 0; j < ppd->num_fonts; j ++)
    printf("fonts[%d] = %s\n", ppd->fonts[j]);
ppdClose(ppd);
return (0);
```

# 查找选项

调用 `ppdFindOption()` 函数在 PPD 文件中查找选项：
`#include <cups/ppd.h>`

```
...
ppd_file_t *ppd;
ppd_option_t *option;
...
option = ppdFindOption(ppd, "name");
```

该参数是一个指向 `ppd_file_t` 结构的指针。`name` 参数是选项的名称。如果该选项存在，则返回指向 `ppd_option_t` 结构的指针。否则，返回一个 `NULL` 指针。

# 查找选择

调用 `cupsFindChoice()` 函数查找特定的选项选择：
`ppd_option_t *option;`
`ppd_option_t *choice;`

```
...
choice = cupsFindChoice(option, "Custom");
```

第一个参数是由 `ppdFindOption()` 返回的指向 `ppd_option_t` 结构的指针。第二个参数是选择的名称。

返回值是指向该命名选择的 `ppd_choice_t` 结构的指针，如果该选择不存在，则返回 `NULL`。

类似的函数是 `cupsFindMarkedChoice()`，它用于查找该选项当前被标记的选择：

# 第三部分 使用 CUPS 编程

```
ppd_file_t *pppd;
ppd_choice_t *choice;
...
```

```
choice = ppdFindMarkedChoice(ppd, "PageSize");
```

第一个参数不是解析选项指针，而是一个指向 `ppd_file_t` 结构的指针。紧接着是选项名称。

返回值是指向第一个被标记选择的 `ppd_choice_t` 结构的指针；如果没有选择被标记或者该选项不存在，则返回 `NULL`。

# 标记选项

每个选项都有一个关联的标记状态。被标记的选项可以发送到打印机或显示给用户。

在标记您的自定义选项之前，调用 `ppdMarkDefaults()` 函数标记来自 PPD 文件的默认选项：

```
#include <cups/ppd.h>
..
ppd_file_t *ppd;
..
ppdMarkDefaults(ppd);
```

然后调用 `ppdMarkOption()` 函数来标记单个选项：

```
#include <cups/ppd.h>
..
ppd_file_t *ppd;
int conflicts;
..
conflicts = ppdMarkOption(ppd, "name", "value");
```

`name` 和 `value` 字符串分别选择特定的选项和值。如果选择没有产生任何冲突，则返回 0。

CUPS 还提供了 `cupsMarkOptions()` 函数，用于标记打印机选项中的所有选项：

```
#include <cups/ppd.h>
..
ppd_file_t *ppd;
int num_options;
cups_option_t *options;
int conflicts;
..
conflicts = cupsMarkOptions(ppd, num_options, options);
```

`cupsMarkOptions()` 函数还处理 IPP 选项到 PPD 选项的映射。
返回值为存在的冲突数量。

# 冲突

PPD 文件支持指定不同选项之间的冲突条件。冲突存储在 `pp_conflict_t` 结构中，这些结构指定了相互冲突的选项。

`ppdMarkOption()` 和 `cupsMarkOptions()` 函数返回与当前标记选项冲突的数量。

您还可以调用 `ppdConflicts()` 函数，在标记所有选项后获取冲突数量：

```
#include <cups/cups.h>
ppd_file_t *ppd;
int conflicts;
conflicts = ppdConflicts(ppd);
```

返回值为冲突选项的数量，如果不存在冲突，则返回 0。由于这些冲突的对称性（A 与 B 冲突，因此 B 与 A 冲突），冲突计数始终是一个偶数。

# 页面尺寸

PPD 文件指定了所有的页面尺寸及其相关的物理边距。这些尺寸存储在 `ppd_size_t` 结构中，并可以在 `ppd_file_t` 结构的 `num_sizes` 成员可用。您可以使用 `ppdPageWidth(int)`、`ppdPageLength(int)` 和 `ppdPageSize()` 函数查找特定的页面尺寸：

```
#include <cups/cups.h>
ppd_size_t *size;
float width;
float length;
size = ppdPageSize(ppd, "size");
width = ppdPageWidth(ppd, "size");
length = ppdPageLength(ppd, "size");
```

尺寸字符串是命名的页面尺寸选项。宽度和长度以磅（points）计算；每英寸 72 磅。`ppd_size_t` 结构包含宽度、长度。

# 尺寸（表 14.4 PPD 结构成员）

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| size | char | 命名的页面尺寸选项 |
| width | float | 宽度（磅） |
| length | float | 长度（磅） |

该尺寸字符串是命名的页面尺寸选项。宽度和长度以磅计算；每英寸 72 磅。`ppd_size_t` 结构包含宽度、长度。

# 自定义尺寸

- `HTTP_ENCRYPT_IF_REQUESTED`: 仅当服务器请求时加密
- `HTTP_ENCRYPT_NEVER`: 从不加密
- `HTTP_ENCRYPT_REQUIRED`: 在发送请求前升级加密
- `HTTP_ENCRYPT_ALWAYS`: 一旦连接服务器即使用加密

# 临时文件

当 CUPS 配置加密时，应用程序需要临时文件。`TMPDIR` 环境变量决定了临时文件的位置，CUPS 使用 `/var/tmp`。如果 `TMPDIR` 变量设置，则使用 `/tmp`。

# 使用 CUPS 函数

CUPS 提供了几个函数来访问和设置当前文件名。

```c
char filename[124];
```

获取临时文件：

```c
if (cupsTempFile(filename, sizeof(filename)) == NULL)
    puts("无法创建临时文件!");
```

```c
fp = fopen(filename, "w");
```

如果临时文件已创建，`cupsTempFile()` 返回文件描述符。否则，它返回 -1。

# 加密支持

当 CUPS 支持加密时，它可以加密发送和接收的所有请求。CUPS 提供了查询和设置默认加密模式的函数。

```c
encryption_t encryption;
...
encryption = cupsEncryption();
```加密值是一个枚举，指定了何时执行加密：

- `HTTP_ENCRYPT_IF_REQUESTED`: 仅当服务器请求时
- `HTTP_ENCRYPT_NEVER`: 从不加密
- `HTTP_ENCRYPT_REQUIRED`: 在发送请求前升级加密
- `HTTP_ENCRYPT_ALWAYS`: 一旦连接服务器即使用加密

`HTTP_ENCRYPT_ALWAYS` 值用于使用 SSL 协议加密，而 `HTTP_ENCRYPT_REQUIRED` 和 `HTTP_ENCRYPT_IF_REQUESTED` 值使用 TLS 协议。默认设置是 `HTTP_ENCRYPT_IF_REQUESTED`，但可以通过 `CUPS_ENVIRONMENT` 环境变量以及 `client.conf` 或 `~/.clientre` 中的加密指令进行覆盖。

`cupsSetEncryption()` 函数设置加密模式。例如，要让本章之前的打印程序始终使用加密，只需在 `main()` 函数顶部添加以下行：

```c
cupsSetEncryption(HTTP_ENCRYPT_REQUIRED);
```

`lp` 和 `lpr` 程序在命令行指定 `-E` 时启用加密。

# 用户、服务器和端口

CUPS 提供了几个函数来访问和设置其他 API 函数使用的当前用户名、服务器和端口号。

# 获取和设置当前用户名

当前用户名通常是您的登录用户名。`cupsUser()` 函数返回当前用户名：

```c
const char *username;
...
username = cupsUser();
```

如所见，接口并不复杂。您将获得当前用户名，如果当前用户名未知，将获得字符串“unknown”。

使用 `cupsSetUser()` 函数更改当前用户名：

```c
cupsSetUser("johndoe");
```

再次，接口并不复杂，您唯一的义务是提供用户名字符串。

# 获取和设置当前服务器

当前服务器通常是“localhost”，但可以通过 `CUPS_SERVER` 环境变量或 `client.conf` 和 `~/.clientre` 文件进行更改。`cupsServer()` 函数返回当前服务器：

```c
const char *server;
...
server = cupsServer();
```

`cupsServer()` 函数永远不会返回空指针。
使用 `cupsSetServer()` 函数可以更改当前服务器：

```
cupsSetServer("foo.bar.com");
```

服务器名称字符串可以是主机名或 IP 地址。

# 获取和设置 IPP 端口

当前的 IPP 端口通常为 631，这是互联网打印协议（Internet Printing Protocol）的默认端口号。该端口可以通过 `IPP_PORT` 环境变量或通过在 `/etc/services` 文件中添加 "ipp" 条目来覆盖。`ippPort()` 函数返回当前的端口号：

```c
int port;
...
port = ippPort();
```

使用 `ippSetPort` 函数更改默认端口：

```c
ippSetPort(8631);
```

# 回调函数

CUPS 支持对任何请求进行验证，包括提交打印作业。获取用户名和密码的默认机制是使用登录用户和来自控制的密码。

为了支持其他类型的应用程序，特别是图形用户界面（GUI），CUPS API 提供了回调机制。

`cupsSetPasswordCB()` 函数用于在程序中设置密码回调。任何时间只能使用一个函数。回调函数接受一个参数（密码提示），并必须返回指向密码字符串的指针，如果操作员取消了操作则返回 NULL。

当与 `cupsUser()` 函数结合时，密码回调可以为验证提供用户名和密码：

```c
#include <cups/cups.h>
...
const char *    /* O - 密码 */
my_password_cb(const char *prompt) /* I - 密码提示 */
{
  char user[65];                    /* 用户名字符串 */
  /* 显示密码提示 */
  puts(prompt);
  /* 从用户获取用户名 */
  printf("Username: ");
  if (fgets(user, sizeof(user), stdin) == NULL)
    return (NULL);
  /* 去除字符串中的换行符并设置用户 */
  user[strlen(user) - 1] = '\0';
  cupsSetUser(user);
  /* 使用 getpass() 询问密码... */
  return (getpass("Password: "));
}
...
cupsSetPasswordCB(my_password_cb);
```

# 错误处理

如果任何 CUPS API 打印函数返回错误，可以通过调用 `cupsLastError()` 和 `ippErrorString()` 找到错误原因。`ippError` 函数返回遇到的最后一个 IPP 错误代码。`ippErrorString()` 将错误代码转换为适用于展示给用户的消息字符串：

```c
#include <cups/cups.h>
...
int jobid;
...
if (jobid == 0)
  printf("Unable to print file: %s\n", cupsErrorString(cupsLastError()));
```
