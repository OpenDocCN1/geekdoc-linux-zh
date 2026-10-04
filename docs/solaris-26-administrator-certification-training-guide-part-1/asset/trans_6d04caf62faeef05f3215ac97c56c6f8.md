
3. 在“串行端口”窗口中，选择将与调制解调器一起使用的端口，如图 12-2 所示。

### Figure 12-2
串行端口窗口。

![](img/85737305a4c9aeecbcadd9986d604c02_229_0.png)

4. 选择“编辑”，“修改”，如图 12-3 所示。修改串行端口窗口出现。

### Figure 12-3
串行端口编辑菜单。

![](img/85737305a4c9aeecbcadd9986d604c02_229_1.png)

修改串行端口窗口以“基本详细信息”模式出现。要输入更多详细信息，请选择“更多”或“专家详细信息”模式。

5. 从下拉“模板”列表中，选择满足或最接近您调制解调器服务的调制解调器配置模板（见图 12-4）。

### Figure 12-4
修改串行端口模板列表。

![](img/85737305a4c9aeecbcadd9986d604c02_230_0.png)

每个调制解调器选择的描述可在表 12-1 中找到。

### Table 12-1 The Modem Template
| 调制解调器配置 | 描述 |
|---|---|
| 仅拨入 | 用户可以拨入调制解调器，但不能拨出。 |
| 仅拨出 | 用户可以从调制解调器拨出，但不能拨入。 |
| 双向 | 用户可以从调制解调器拨入或拨出。 |

6. 从“波特率”下拉列表中选择正确的波特率，如图 12-5 所示。

### Figure 12-5
波特率下拉列表。

![](img/85737305a4c9aeecbcadd9986d604c02_230_1.png)

图 12-6 显示了一个已完成的修改串行端口窗口。已选择专家详细信息模式以显示所有可配置的选项。

### Figure 12-6
已完成的修改串行端口窗口。

![](img/85737305a4c9aeecbcadd9986d604c02_231_0.png)

表 12-2 描述了图 12-6 中显示的每个可配置选项。

### Table 12-2 Modify Serial Port Window Items
| 项目 | 描述 |
|---|---|
| 端口 | 列出您从串行端口主窗口中选择的端口或端口。 |
| 服务 | 指定端口的服务已打开（启用）。 |
| 波特率 | 指定用于与终端通信的线路速度。线路速度代表 /etc/ttydefs 文件中的一个条目。 |
| 终端类型 | 显示终端类型的缩写——例如 ansi 或 vt100。类似的缩写可在 /etc/termcap 中找到。此值在 $TERM 环境变量中设置。 |
| 选项：仅初始化 | 指定端口软件已初始化但未配置。 |
| 选项：双向 | 指定端口线路在两个方向上使用。 |
| 选项：软件载波 | 指定使用软件载波检测功能。如果未选中该选项，则使用硬件载波检测信号。 |
| 登录提示 | 显示连接建立后向用户显示的提示。 |
| 注释 | 显示服务的注释字段。 |
| 服务标签 | 列出与此端口关联的服务标签——通常是 /dev/term 目录中的一个条目。 |

### Table 12-2 Modify Serial Port Window Items (continued)
| 项目 | 描述 |
|---|---|
| 端口监视器标签 | 指定对此端口使用的端口监视器的名称。默认监视器通常是正确的。 |
| 创建 utmp 条目 | 指定在登录时在记账文件中创建 utmp 条目。 |
| 载波连接 | 指定在收到连接指示时立即调用端口的关联服务。 |
| 服务 | 显示连接时运行的程序。 |
| 流模块 | 显示在调用服务之前推送的流模块。 |
| 超时（秒） | 指定如果端口上的打开进程成功且未接收到输入数据，则在关闭端口之前的秒数。 |

7. 单击“确定”以配置端口。

8. 使用 pmadm 命令验证调制解调器服务是否已配置为使用。
为此，输入

```
pmadm -l -s ttya
```

串行端口现已配置完成并可使用。

## Service Access Facility (SAF)
服务访问设施（SAF）

SAF 是用于管理终端、调制解调器和其他网络设备的工具。SAF 是一种开放系统解决方案，通过 tty 设备和局域网（LAN）控制对系统和网络资源的访问。SAF 不是一个程序；它是一组后台进程和管理命令的层次结构，其中包括 sacadm、pmadm、ttyadm 和 nisadmin。有关这些命令的描述，请参阅表 12-3。

### Table 12-3 SAF Commands
| 命令 | 描述 |
|---|---|
| sacadm | 用于添加、删除、启用、禁用、启动和停止端口监视器。 |
| pmadm | 配置端口监视器服务以及各个端口的关联进程。 |
| ttyadm | 为串行端口格式化输入到 pmadm。 |
| sttydefs | 在 /etc/sttydefs 文件中创建和修改条目以描述终端线路特性。 |
| nisadmin | 为远程打印格式化输入到 pmadm。 |

具体来说，SAF 使您能够

- 设置 ttymon 和侦听端口监视器（使用 sacadm 命令）
- 设置 ttymon 端口监视器服务（使用 pmadm 和 ttyadm 命令）
- 设置侦听端口监视器服务（使用 pmadm 和 nisadmin 命令）
- 排除 tty 设备故障
- 排除打印服务传入网络请求的故障
- 排除服务访问控制器故障（使用 sacadm 命令）

与 SAF 关联的配置文件在表 12-4 中描述。

### Table 12-4 Files Associated with SAF
| 文件 | 描述 |
|---|---|
| /etc/saf/_sysconfig | 每系统配置脚本 |
| /etc/saf/_sactab | SAC 的管理文件；包含 SAC 控制的端口监视器的配置数据 |
| /etc/saf/pmtag | 端口监视器 pmtag 的主目录 |
| /etc/saf/pmtag/_config | 如果存在，则为端口监视器 pmtag 的每个端口监视器配置脚本 |
| /etc/saf/pmtag/_pmtab | 端口监视器 pmtag 的管理文件；包含 pmtag 提供的服务的端口监视器特定配置数据 |
| /etc/saf/pmtag/svctag | 服务 svctag 的每个服务配置脚本 |
| /var/saf/log | SAC 的日志文件 |
| /var/saf/pmtag | 由 pmtag 创建的文件的目录，例如日志文件 |

### sacadm
使用 sacadm 命令添加、列出、删除、终止、启动、启用或禁用 ttymon 或侦听端口监视器。您必须以超级用户身份登录才能使用此命令。例如，用于添加 ttymon 端口监视器的命令语法是

```
sacadm -a -p mbmon -t ttymon -c /usr/lib/saf/ttymon -v 'ttyadm -V' -y "TTY Ports a & b"
```

注意 ttyadm 命令的使用。

要查看新添加的端口监视器，输入：

```
sacadm -l -p mbmon
```

系统响应如下：

```
PMTAG   PMTYPE   FLGS   RCNT   STATUS   COMMAND
mbmon   ttymon   -      0      STARTING /usr/lib/saf/ttymon #TTY Ports a & b
```

用于添加和查看端口监视器的 sacadm 命令选项列在表 12-5 中。

### Table 12-5 sacadm Command Options
| 命令选项 | 描述 |
|---|---|
| -a | 添加端口监视器选项 |
| -c | 定义用于启动端口监视器的命令字符串 |
| -k | 终止端口监视器状态选项 |
| -l | 列出端口监视器状态选项 |
| -p | 指定 pmtag mbmon 作为端口监视器标签 |
| -r | 移除端口监视器状态选项 |
| -s | 启动端口监视器状态选项 |
| -t | 指定端口监视器类型为 ttymon |
| -v | 指定端口监视器的版本号 |
| -y | 定义注释以描述此端口监视器实例 |

要终止 ttymon 端口监视器，输入

```
sacadm -k -p mbmon
```

要重新启动已终止的端口监视器，输入

```
sacadm -s -p mbmon
```

要删除端口监视器，输入

```
sacadm -r -p mbmon
```

### pmadm
端口监视器服务管理员（pmadm）命令使您能够管理端口监视器的服务。使用 pmadm 添加服务、列出与端口监视器关联的一个或多个端口的服务，以及启用或禁用服务。一个例子是终端服务。您还可以安装或替换每个服务的配置脚本或打印有关服务的信息。

当您使用 pmadm 命令管理服务时，您通过 pm 标签参数指定特定的端口监视器，并通过 svctag 参数指定特定的端口。对于每种端口监视器类型，SAF 需要一个专用命令来格式化端口监视器特定的配置数据。此数据由 pmadm 命令使用。

要向 mbmon 端口监视器添加标准终端服务，输入

```
pmadm -a -p mbmon -s a -i root -v 'ttyadm -V' -m '"ttyadm -i 'Terminal disabled' -l \ contty -m ldterm,ttcompat -S y -d /dev/term/a -s /usr/bin/login"'
```

pmadm 命令中使用的选项在表 12-6 中描述。请注意，上面的 pmadm 命令包含一个嵌入的 ttyadm 命令。

### Table 12-6 pmadm Command Options
| 命令选项 | 描述 |
|---|---|
| -a | 添加端口监视器状态选项 |
| -d | 禁用端口监视器服务 |
| -e | 启用端口监视器服务 |
| -l | 列出端口监视器服务信息 |
| -p | 指定 pm 标签 mbmon 作为端口监视器标签 |
| -s | 指定 svctag a 作为端口监视器服务标签 |
| -i | 指定 svctag 运行时的身份 |
| -v | 指定端口监视器的版本号 |
| -m | 指定由 ttyadm 格式化的 ttymon 特定配置数据 |

下一个示例使用 pmadm 命令列出 TTY 端口的状态，或与端口监视器关联的所有端口的状态。输入

```
pmadm -l -p mbmon
```

系统输出以下信息：

```
PMTAG PMTYPE SVCTAG FLAGS ID <PMSPECIFIC>
mbmon ttymon a . root /dev/term/a - - /usr/bin/login \
- contty ldterm,ttcompat login: Terminal disabled - y #Comment
```
