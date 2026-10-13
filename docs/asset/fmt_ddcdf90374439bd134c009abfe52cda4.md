
> **注意**
> 所有已定义的 CGI 环境变量也允许作为包含变量使用。

> **注意**
> 在您的配置文件（或 `.htaccess` 中），您可以指定 `Options IncludesNOEXEC` 来禁用 `exec` 指令，因为这是 SSI 指令中安全性最低的。当 Web 用户能够创建内容（如来宾簿或讨论板）并且这些选项被启用时，请特别注意！

由 `var` 和 `value` 设置属性的变量也可以在其他地方与以下某些指令一起使用。

## 流程控制

使用由 `set` 指令设置的各种环境变量和包含变量，可以使用有限的流程控制语法在服务端解析页面上生成一定量的动态内容。

`if/else` 函数的语法如下：

```
<!--#if expr="test_condition" -->
<!--#elif expr="test_condition" -->
<!--#else -->
<!--#endif -->
```

`expr` 可以是一个字符串，如果非空则被视为真；也可以是两个字符串之间的各种比较。可用的比较运算符为 `=`、`!=`、`<`、`<=`、`>` 和 `>=`。如果第二个字符串的格式为 `/string/`，则字符串将通过正则表达式进行比较。可以使用 `&&`（与）和 `||`（或）将多个比较串联起来。`if/elif/else` 指令之间的任何文本都将显示在生成的页面上。此类流程结构的示例如下：

```
<!--#set var="agent" value="$HTTP_USER_AGENT" -->
<!--#if expr="$agent"= /Mozilla/" -->
Mozilla!
<!--#else -->
Something else!
<!--#endif -->
```

如果您使用的浏览器在其 `USER_AGENT` 字符串中包含 Mozilla，此代码将显示 Mozilla!；否则显示 Something else!。

## Apache 图形界面配置

可以通过 Red Hat 的 `system-config-httpd`（X Window 系统的 GUI 工具）配置 Apache 的一些基本行为。这提供了一种轻松配置设置的方式，例如 Apache 的用户和组名称、PID 和进程锁文件的位置，或性能设置（如最大连接数），而无需手动编辑配置文件。

> **警告**
> 如果您使用 `system-config-httpd`，请不要尝试手动编辑 `httpd.conf` 文件。如果您再次使用 `system-config-httpd`，手动更改将被 GUI 客户端覆盖！

您可以通过 X 桌面面板中“服务器设置”的“HTTP 服务器”菜单项，或从 X 终端窗口的命令行启动此客户端，如下所示：

```
$ system-config-httpd &
```
