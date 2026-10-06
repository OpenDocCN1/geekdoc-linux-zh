

## 高质量的随机数生成

要添加该服务，请执行命令：

```
chkconfig --add name
```

其中 name 是服务的名称。chkconfig 程序会根据 init.d 脚本中的注释创建所需的符号链接。

## 删除服务

要删除一个服务，请执行命令：

```
chkconfig --del name
```

其中 name 是服务的名称。chkconfig 程序会删除关联的符号链接。

## 将服务与运行级别（Runlevels）关联

要将服务与一个或多个运行级别关联，请执行命令：

```
chkconfig name reset
```

其中 name 是服务的名称。chkconfig 程序会根据 init.d 脚本中的注释创建所需的符号链接。如果你愿意，可以忽略关联的 init.d 脚本的内容，显式地设置服务在指定级别上运行或不运行。要指定服务应该运行的级别，请执行命令：

```
chkconfig --level levels1 name on
```

其中 name 是服务的名称，levels1 是指定运行级别的一系列数字。例如，命令

```
chkconfig --level 35 lunch on
```

该命令指定 lunch 服务将在级别 3 和 5 下运行。要指定服务不运行的级别，请执行命令：

```
chkconfig --level levels1 name off
```

其中 name 是服务的名称，levels1 是指定运行级别的一系列数字。例如，命令

```
chkconfig --level 24 lunch off
```

该命令指定 lunch 服务不在级别 2 和 4 下运行。

现在，尝试练习 14.3，该练习要求你使用 chkconfig。

## 练习 14.3
### 将服务与运行级别关联

RHCE 考试可能要求你配置服务在指定的级别运行。请执行以下操作以验证你的能力：

- 1. 使用 chkconfig 确定哪些服务在哪些运行级别运行。
- 2. 在安装了 Apache 的系统上，配置 httpd 服务仅在运行级别 5 下运行。
- 3. 使用 init 命令更改当前运行级别，以便验证你的更改是否成功。

如果有必要，请回看章节，但要准备好在 RHCE 考试中不借助帮助的情况下使用 chkconfig。

## /etc/rc.d/rc.local 脚本

/etc/rc.d/rc.local 脚本是由与运行级别 2、3 和 5 关联目录中的符号链接运行的特殊脚本。它的起点是 99，这意味着它在所有其他运行级别脚本之后运行。默认情况下，它会创建

- /etc/issue 文件
- /etc/issue.net 文件

当用户通过本地控制台登录时，会显示 /etc/issue 文件。默认情况下，该文件报告 Red Hat Linux 的版本和内核版本：

Red Hat Linux release 6.0 (Hedwig)
Kernel 2.2.25-15 on an i686

当用户通过远程控制台登录时（例如通过启动 Telnet 会话），会显示 /etc/issue.net 文件。默认情况下，该文件报告 Red Hat Linux 的版本和内核版本：

Red Hat Linux release 6.0 (Hedwig)
Kernel 2.2.25-15 on an i686

更改 /etc/issue.net 的内容是一个良好的做法，这样黑客获取的系统信息就会更少。你可能还想显示一个说明系统使用限制的横幅。

你可以轻松地修改 /etc/rc/rc.local 脚本，在 /etc/issue.net 中放入不同的消息或执行其他主机特定的初始化。由于脚本是执行的，当脚本执行时，所有与当前运行级别关联的其他系统服务都应该是正常的。
要了解更多关于 rc.local 脚本的信息，请完成练习 14.4。

## 练习 14.4
### /etc/rc.d/rc.local 脚本

系统管理员修改 rc.local 脚本来自定义启动。要了解更多启动信息，请检查已配置 Red Hat Linux 系统的 /etc/rc.d/rc.local 脚本，查看系统管理员对脚本做了哪些修改。

## 总结

在本章中，你学习了系统初始化。涵盖了最重要的主题：

- **系统初始化**：当系统启动时，它会运行 /etc/rc.d/rc.sysinit 脚本来初始化文件系统和设备，然后运行 /etc/rc.d/rc.rc 脚本来初始化服务。

- **/etc/rc.d/rc.sysinit 脚本**：/etc/rc.d/rc.sysinit 脚本执行二十多项操作，范围从设置网络到保存启动日志。

- **/etc/rc.d/rc 脚本**：/etc/rc.d/rc 脚本运行与默认运行级别关联的一系列脚本。通过位于 /etc/rc.d/rc?d 目录中的符号链接实现，其中 ? 是默认运行级别。

- **运行级别 (Runlevels)**：Red Hat Linux 定义了七个运行级别，编号从 0 到 6。系统操作通常在运行级别 3 或 5 下进行。其他级别用于故障和修复。

- **运行级别脚本**：运行级别脚本位于 /etc/rc.d/init.d。它们通常接受 start、restart、status、init 参数。

- **指向运行级别的符号链接**：指向运行级别脚本的符号链接格式为 XNN，其中 X 是 K 或 S，NN 指定运行级别。K 脚本用于停止服务，S 脚本用于启动服务。

- **函数**：/etc/rc.d/init.d 包含了有用的函数。它被运行级别脚本调用。

- **配置服务**：你可以使用 chkconfig、ksys、ntsys 和 tksys 等工具将服务与运行级别关联。

- **/etc/rc.d/rc.local 脚本**：/etc/rc.d/rc.local 脚本用于本地初始化。

## 关键术语

在进入下一章之前，确保你熟悉以下术语：

- 优先级 (Priority)
- 运行级别 (Runlevel)

## 附加信息

如果你想获得有关本章主题更多信息，可以参考《Red Hat 参考指南》。

## 复习题

- 1. 下列文件系统首先挂载？
  - A. 非根文件系统，只读模式
  - B. 非根文件系统，读写模式
  - C. 根文件系统，只读模式
  - D. 根文件系统，读写模式
- 2. 哪个脚本调用运行级别脚本？
  - A. /etc/rc.d/rc
  - B. /etc/rc.d/rc.local
  - C. /etc/rc.d/rc.serial
  - D. /etc/rc.d/rc.sysinit
- 3. 如果以下脚本位于同一个目录下，哪个脚本将首先执行？
  - A. K05alpha
  - B. K10beta
  - C. S01delta
  - D. S05gamma
- 4. 查看与 lunch 服务关联的运行级别，必须执行哪个命令？
  - A. chkconfig
  - B. chkconfig lunch
  - C. chkconfig --lunch
  - D. chkconfig --list
- 5. 下列工具只能在 X 下使用？
  - A. chkconfig
  - B. ksysys
  - C. ntsys
  - D. tksys
- 6. 更改放在 /etc/issue.net 中的信息，应该修改哪个文件？
  - A. /etc/rc.d/rc
  - B. /etc/rc.d/rc.local
  - C. /etc/rc.d/rc.serial
  - D. /etc/rc.d/rc.sysinit

# 复习题答案

1. C. 系统首先以只读模式挂载根系统；随后以读写模式挂载所有文件系统。
2. A. rc 脚本调用 /etc/rc.d/r?.d 目录中的脚本。
3. A. kill 脚本在启动脚本之前执行；在同一类型内，脚本按优先级执行。
4. D. --list 命令导致 chkconfig 列出服务及其关联的运行级别。
5. B, D. ksysv 程序需要 X。tsysv 程序使用 TK 小部件集且仅在 X 下运行。
6. B. rc.local 文件构建 /etc/issue.net 文件。

