
该元素可以是以下之一：

- `config` 允许你设置有关如何处理文档解析的各种配置选项。由于页面是从上到下解析的，`config` 指令应该出现在 HTML 文档的顶部。使用此命令可以设置三种配置：
  - `errrmsg` 如果解析文档时出现错误，则设置返回给客户端的错误消息。通常是 `[error occurred while processing this directive]`，但可以使用此指令将其设置为任何内容。
  - 示例：`<!--#config errMsg="[It's broken, dude]"-->`
  - `sizefmt` 设置用于显示文件大小的格式。你可以将值设置为 `bytes` 以显示精确的字节大小，或者缩写为以 KB 或 MB 显示大小。
  - 示例：`<!--#config sizefmt="bytes"-->`
- `timefmt` 设置用于显示时间的格式。该值的格式与 C（以及 Perl）中用于显示日期的 `strftime` 函数相同，如下表所示。

| 占位符 | 说明 |
| :--- | :--- |
| `%a` | 星期缩写 |
| `%A` | 星期 |
| `%b` | 月份缩写 |
| `%B` | 月份 |
| `%c` | ctime 格式: Sat Nov 19 21:05:57 1994 |
| `%d` | 月中的数字日期 |
| `%e` | DD |
| `%D` | MM/DD/YY |
| `%h` | 月份缩写 |
| `%H` | 小时，24 小时制，前导零 |
| `%I` | 小时，12 小时制，前导零 |
| `%j` | 年中的第 |
| `%k` | 小时 |
| `%l` | 小时，12 小时制 |
| `%m` | 月份，从 01 开始 |
| `%M` | 分钟，前导零 |
| `%n` | 换行 |
| `%o` | 华丽日期—1st, 2nd, 25th 等 |
| `%p` | AM 或 PM |
| `%r` | 时间格式: 09:05:57 PM |
| `%R` | 时间格式: 21:05 |
| `%S` | 秒，前导零 |
| `%t` | 制表符 |
| `%T` | 时间格式: 21:05:57 |
| `%U` 以星期日为每周的第一天的周数 |
| `%w` | 星期几，数字形式；星期日 == 0 |
| `%W` 以星期一为每周的第一天的周数 |
| `%x` | 日期格式: 11/19/94 |
| `%X` | 时间格式: 21:05:57 |
| `%y` | 年（两位） |
| `%Y` | 年（四位） |
| `%Z` | ASCII 时区，例如 PST |

- `echo` 显示此处列出的任何一个嵌套变量。时间将按 `fmt` 指定的格式格式显示。要显示的变量由 `var` 属性指定。

- `DATE_GMT` 格林尼治标准时间的当前日期。
- `DATE_LOCAL` 本地区的当前日期。
- `DOCUMENT_NAME` 文件名
- `DOCUMENT_URI` 文档的 URL。
- `LAST_MODIFIED` 文档的最后修改日期。
- `PATH_INFO` 文档的路径信息。
- `QUERY_STRING` 传递给文档的查询字符串。
- `REQUEST_METHOD` 文档的请求方法。
- `SERVER_SOFTWARE` 服务器软件名称。
- `USER_AGENT` 客户端的用户代理字符串。

- `cgi` 要执行的程序。
- `cmd` 要执行的 shell 命令。
- `fsize` 文件大小。
- `file` 的文件系统路径。
- `virtual` 文件的 URL 路径。

- `printenv` 显示所有存在的变量。没有属性。
- `set` 设置变量的值。属性为 `var` 和 `value`。

- `include` 包含文件的内容。
- `cgi` 要执行的程序。
- `file` 的文件系统路径。
- `virtual` 文件的 URL 路径。

```
<!--#set var="agent" value="$HTTP_USER_AGENT" -->
```

```
<!--#if expr="$agent = /Mozilla/" -->
Mozilla!
<!--#else -->
Something else!
<!--#endif -->
```

# 启动和停止服务器

此时，你已经安装并按照你的要求配置了 Apache 服务器。现在是首次启动它了。

## 手动启动服务器

Apache 服务器 (`httpd`) 有几个命令行选项可用于设置某些默认值，指定 `httpd` 读取其配置指令的位置。Apache `httpd` 可执行文件理解以下选项：

```
httpd [-d directory] [-f file]
  -C "directory" -c "directory"
  -v [-V] -h [-l] [-L] [-S] [-t]
```

`-d` 选项验证 `ServerRoot` 目录的位置。它将 `ServerRoot` 变量（Apache 服务器安装的目录）的初始值设置为你指定的路径。此默认值通常从 `httpd.conf` 中的 `ServerRoot` 指令中读取。

`-f` 标志指定主配置文件 `conf/httpd.conf` 的位置。它在启动时读取并执行 `ConfigurationFile` 中找到的配置命令。如果 `Configuration` 不是绝对路径（不以 `/` 开头），则其位置被认为相对于 `httpd.conf` 中 `ServerRoot` 指令所指定的路径。默认情况下，此值为 `ServerRoot/httpd.conf`。

`-v` 选项打印 Apache 服务器的开发版本并终止进程。

`-V` 选项显示服务器在编译时生效的所有设置。

`-h` 选项打印服务器的以下用法：

```
Usage: httpd [-d directory] [-f file]
  -C "directory" [-c "directory"
```
