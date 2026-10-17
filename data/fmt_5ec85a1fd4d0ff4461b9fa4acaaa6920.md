
| | `IP6_PKTOPS` | | * | 接收数据包信息 | * | int |

### 检查选项是否支持并获取默认值

### 声明可能值的联合体

我们的联合体包含 `getsockopt` 返回的每个可能值的其中一个成员。

### 定义函数原型

我们为四个函数定义了函数原型，这些函数被用于打印特定 socket 选项的值。

### 定义结构体并初始化数组

我们的 `sock_opts` 结构体包含了为每个 socket 选项调用 `getsockopt` 并打印其值所需的所有信息。最后一个成员 `opt_val_str` 是指向四个函数之一的指针，用于打印该值。我们分配并初始化了这些这些结构体的数组，数组中的每个元素对应一个 socket 选项。

并不是所有实现都支持所有的 socket 选项。确定给定选项是否被支持的方法是使用 `#ifdef` 或 `#if defined`，正如我们在 `SO_REUSEPORT` 中所示的那样。为了完整性，数组的每个元素都应该按照类似于我们展示 `SO_REUSEPORT` 的方式进行编译，但我们省略了这，因为 `#ifdef` 已经解释了我们展示的代码的合理性，且对讨论没有额外帮助。

图 7.3 显示了我们的主函数。

```c
47 int
48 int main(int argc, char **argv)
49 {
50 int fd, len;
51 struct sock_opts *ptr;
52 fd = Socket(AF_INET, SOCK_STREAM, 0);
53 for (ptr = sock_opts; ptr->opt_str != NULL; ptr++) {
54 printf("%s: %s\n", ptr->opt_str);
55 if (ptr->opt_val_str == NULL)
56 printf("<undefined>\n");
57 else {
58 len = sizeof(val);
59 if (getsockopt(fd, ptr->opt_level, ptr->opt_name,
60 &val, &len) == -1) {
61 err_ret("getsockopt error");
62 }
63 } else {
64 
65 printf("default = %s\n", (ptr->opt_val_str) (&val, len));
66 }
67 }
68 exit(0);
```

图 7.3 用于检查所有 socket 选项的主函数。

![](img/aeda3be9ee318bedd42850d461da0f28_192_0.png)

### 创建 TCP socket，遍历所有选项

我们创建一个 TCP socket，然后遍历我们数组中的所有元素。如果 `opt_val_str` 指针为空，则表示该选项未被实现定义（我们已经展示过对于 `SO_REUSEPORT` 来说这是可能的）。

调用 `getsockopt`

我们调用 `getsockopt`，但在返回错误时不终止程序。许多实现定义了某些 socket 选项名称，尽管它们并不支持该选项。不支持的选项应该包含一个 `ENOPROTOOPT` 错误。

### 打印选项的默认值

如果 `getsockopt` 返回成功，我们调用函数将选项值转换为字符串并打印该字符串。

在图 72 中，我们展示了四个函数原型，每个原型对应一种返回的值类型。图 7.4 显示了这些函数之一的 `sock_str_flag`，它用于打印标志（flag）选项的值。其他三个函数也是类似的。

```c
69 static char strres[128];
70 sock_str_flag(union val *ptr, int len)
72 {
73     if (len != sizeof(int))
74         sprintf(strres, sizeof(strres), "%d", not sizeof(int), len);
75     else
76         sprintf(strres, sizeof(strres), "%s", (ptr->l_val == 0) ? "off" : "on");
77 
78 return(strres);
79 }
```

图 7.4 `sock_str_flag` 函数：将标志选项转换为字符串。

回 `getsockopt` 的最后一个参数是一个值-结果型参数。我们做的第一个检查是 `getsockopt` 返回的值的大小是否符合预期。返回的字符串是 `off` 或 `on`，取决于标志选项是 0 还是非零。

在 AIX 4.2 下运行此程序得到如下结果：

```
SO_BROADCAST: default = off
SO_DEBUG: default = off
SO_DONTROUT: default = off
SO_ERROR: default = 0
SO_KEEPALIVE: default = off
SO_LINGINGER: default = 1_onoff = 0, 1_linger = 0
SO_GOOBLINE: default = off
SO_RCVBUF: default = 16384
SO_SNDBUF: default = 16384
```

`SO_RCVLOW`: default = 1

`SO_SNDLOW`: default = 4096

`SO_RCVTIMEO`: default = 0 sec, 0 use

`SO_SNDTIMEO`: default = 0 sec, 0 use

`SO_LINGER`: default = off

`SO_REUSEPORT`: (undefined)

`SO_TYPE`: default = 1

`SO_USEADDRACK`: default = off

`IP_TOS`: default = 0

`IP_TTL`: default = 60

`TCP_MAXSEG`: default = 512

`TCP_NODELAY`: default = off
