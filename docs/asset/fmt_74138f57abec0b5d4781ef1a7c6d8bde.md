
# 图形化配置 BIND

即使使用图形化工具配置 BIND，建议也阅读前面的章节“配置 BIND”，以了解工具正在操作的配置选项。

除了安装 `bind` 软件包、`bind-utils` 软件包及其软件依赖项外，如果想使用图形配置工具，请安装 `system-config-bind` RPM 软件包。

要启动该工具，从桌面顶部的系统中选择管理、设置、域名系统。或者，执行 `system-config-bind` 命令。如果你尚未以 root 用户身份登录，必须输入正确的 root 密码才能使用该工具。

应用程序附带了详细的 PDF 格式说明，位于 `/usr/share/doc/system-config-bind/sc_manual.pdf` 文件。本节强调了其部分功能，但应参考手册以获取完整说明。

## 第 16 章 使用 BIND 进行主机名解析

首次启动应用程序时，将显示如图 16.1 所示的默认设置。在显示默认设置之前，会出现一条消息说明在 `/etc/named.conf` 文件未找到默认配置。如果你点击消息上的“确定”，则会创建一个带有默认值的 `/etc/named.conf` 文件。

![](img/60a952f475fd10259ba425768b115659_355_0.png)

图 16.1 默认设置

要添加、编辑或删除属性，请从主窗口的列表中选择一个项目，并在其上点击右键查看操作菜单。菜单会根据所选内容而变化。

### 导入定义的主机

工具栏上的“导入”（Import）按钮可用于导入 `/etc/hosts` 文件格式的 IP 地址列表及其主机名。点击该按钮后，使用“打开”（Open）按钮选择要导入主机的文件。

要导入所选文件中列出的所有主机，点击“确定”，注意这些主机将出现在主窗口的区域（zone）中。可以对从给定文件导入的主机列表进行过滤，以便只导入匹配模式或不匹配模式的主机。要设置过滤器，请从“新列表元素”（New List Element）中选择一种类型。“编辑列表元素”（Edit List element）元素中的输入字段会根据选择的过滤器类型而变化。例如，选择“IPv4 地址过滤器”将使“编辑列表元素”框显示如下：

对于任何类型的过滤器，输入要匹配的模式并在“编辑列表元素”框中点击“确定”，将其添加到过滤器列表（Filter List）。当过滤器添加后，如果点击“编辑列表元素”框中输入字段左侧的无标签按钮，则会显示一个感叹号而不是匹配过滤器的主机标签，且匹配模式的主机将不会被添加。如果选了“匹配所有过滤器”（Match ALL Filters），则仅当主机匹配列表中的所有模式时才会添加。如果选了“匹配任意过滤器”（Match ANY Filters），则当主机匹配至少一个过滤器时就会添加。配置好过滤器后，点击窗口右下角的“确定”，将所需的主机添加到主窗口的区域列表中。

### 日志连接

![](img/60a952f475fd10259ba425768b115659_356_0.png)

图 16.2 导入定义的主机

### 保存更改

配置 DNS 服务器或更改设置后，点击主窗口工具栏上的“保存”（Save）按钮。已修改并保存的配置文件版本将保存为 `<filename>.<timestamp>`，例如 `named.conf.2006-17_0.0`。如果服务正在运行，将重启以启用更改。

### 启动和停止服务器

要启动服务器，从区域列表中选择“DNS Server”，并在其上点击右键显示菜单。从菜单中选择“启动”（Start Server）。如果服务正在运行，可用选项为重启（restart）、重载（reload）或停止服务器（stop server）。

### 日志连接

默认情况下，`named` 服务将日志消息写入 `/var/log/messages`。可以通过 `named.conf` 中的 `logging` 语句自定义日志。如果 `named.conf` 语法错误，关于错误的消息将进入 `/var/log/messages` 或标准错误，无论 `logging` 语句如何设置。日志消息的位置可以通过 `logging` 语句内部定义一个或多个 `channel` 语句来修改。列表 16.1 显示了带有强制和可选语句的基本语法。

logging 语句的基本语法

```
logging {

  channel <channel-name> {

    <destination>;

  }

  severity <sev>;

```
列表 16.1 继续

```
print-category <value>;

print-severity <value>;

print-time <value>;

category <category-name> <channel-list>;
```
列表 16.2 定义了日志的四个预定义通道。

```
channel default_syslog {

  syslog daemon;   // 发送到 syslog 进程

  severity info;   // 仅发送 info 及以上优先级的消息

};
```
```
channel default_debug {
  file "named.run"; // 写入工作目录下的 named.run
  // 注意：如果服务器使用 '-f' 选项启动，则使用 stderr
  severity dynamic;  // 记录当前 debug 级别的日志
};
```
```
channel default_stderr {

  stderr;          // 写入 stderr

  severity info;   // 仅发送 info 及以上优先级的消息

};
```
```
channel null {

  null;           // 丢弃发送到此通道的所有内容

};
```

你也可以定义自定义通道。在创建用户定义通道时，将列表 16.1 中的 `<destination>` 替换为以下内容之一：

- 将消息发送到文件：

```
file <filename> versions <num> size <num>
```

只需要 `filename`。可选地设置磁盘上保留 `<num>` 个旧日志文件。将 `<num>` 设置为 `unlimited` 以保留所有旧日志文件。如果没有配置 `versions`，则不备份日志文件。如果设置了 `size` 且 `versions` 大于0，当文件达到指定大小时将创建一个新日志文件，旧文件重命名为 `<filename>`。日志文件将留在磁盘上，但在达到指定大小后不再写入。必须手动重命名或以某种方式减小文件大小以继续日志。如果没有设置 `size`，日志文件的大小不受限制。设置时，数字后应接 `k`（千字节）、`m`（兆字节）等，例如 `10m` 表示 10 兆字节。

- 将消息发送到特定的 syslog 设施：

```
syslog <facility>
```

将 `<facility>` 替换为要使用的 syslog 设施：`auth`、`authpriv`、`cron`、`daemon`、`kern`、`lpr`、`mail`、`news`、`syslog`、`user`、`local0` 到 `local7`。该列表也在 `syslog.conf` 页面中。必须修改 `/etc/syslog.conf` 文件来决定 syslog 如何通过设置的设施处理消息。

此方法通常仅用于 named 在前台运行且你正在监控 stderr 时（例如调试期间）。

- 将消息发送到标准错误：

```
stderr
```

可选，如果将消息写入文件，可以使用 `logging` 语句中的 `severity <sev>` 语句来确定每个通道处理的消息类型。如果使用了 syslog，其优先级也会考虑在内。

在自定义日志时，可以将 `print-category`、`print-severity` 和 `print-time` 语句可选设置为 `yes` 或 `no`。如果 `print-category` 设置为 `yes`，则记录消息的类别。如果 `print-severity` 设置为 `yes`，则记录每条消息的严重性。如果 `print-time` 设置为 `yes`，则每条消息都会写入时间戳。logging 语句内部的 `category` 语句用于将通道与日志消息类别关联。如列表 16.1 所示，该语句接受：

```
category <category-name> <channel-list>
```
