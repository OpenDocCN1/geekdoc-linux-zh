
```
logon script = scripts\%U.bat
#或者为每个用户一个子目录，如
#logon script = %U\logon.bat
```

337

在 Windows 9x PC 上运行的脚本应该是 ASCII 格式，并格式化为在每行末尾包含 CRLF。如果可能，最好在 Windows 9x PC 上使用“记事本”创建这些文件，并将它们复制到 Samba 服务器中，同时保留行结束符。也可以使用 Unix 编辑器（如 `vi` 或 `pico`），并在脚本的每行末尾添加 Ctrl+V 和 Ctrl+M 以创建 CRLF 行结束符。这确保了脚本在 Windows 9x 客户端上运行时能够被正确识别。

**提示：** 尽管在目前阶段并非必须的，但建议在没有其他现有 WINS 服务器的情况下，将 Samba 服务器启用为 WINS 服务器。你可以通过将 `wins support` 参数设置为 `wins support=yes` 来实现这一点。这样 Windows 9x 客户端就可以利用 WINS 服务了。

列表 9.1 显示了提供简单的 Samba Windows 9x 域控制器的示例 `smb.conf` 文件。

**列表 9.1** 一个用于 Windows 9x 域控制器的简单 `smb.conf` 文件。

```
# 使用 SWAT 创建的 Samba 配置文件
# 源自 ntwdev02.domain (192.168.1.3)
# Date: 1999/07/26 20:17:33
Global parameters
[global]
workgroup = SAMBABOOK
netbios name = LINUXSERVER
encrypt passwords = Yes
log file = /usr/local/samba/var/log.%m
max log size = 50
domain logons = yes
logon script = confirm.bat
os level = 32
preferred master = Yes
local master = yes
domain master = yes
wins support = yes
```

```
[homes]
comment - Home Directories
read only = No
browseable = No
```

```
[netlogon]
comment - NetLogon Service
path = /home/samba/netlogon
guest account -
browseable = No
locking = No
available = No
```

然后需要重启 Samba 服务器以提供 Windows 9x 域功能。

# 设置 Samba Windows 9x 客户端

配置 Windows 9x 客户端以使用作为域控制器的 Samba 服务器，与设置 Windows NT 服务器执行相同任务没有区别。

关键配置是启用用于登录验证的“微软网络客户端（Client for Microsoft Networks）”属性，并输入域名称。域名将与 Samba 服务器 `smb.conf` 文件中 `workgroup` 参数设置的名称相同。如果你从其他地方使用的 `smb.conf` 文件中采用建议值 `SAMBABOOK` 并输入它，应该会显示图 9.1 所示的对话框。

系统可能会提示你插入 Windows 9x 安装光盘，完成后，它会要求重启。重启后，Windows 9x 客户端将尝试使用新的 Samba 9x 域控制器将用户登录到 Samba 域。

# 成功登录域

如果登录脚本仅包含一个在屏幕上回显提示的命令，如下处所示的命令：

```
echo "Successfully logged into the SAMBABOOK domain ..."
```

![](img/166cd29830b01a9e3eceb33240be1bcf_364_0.png)

图 9.1 Windows 9x SAMBABOOK 域配置。

# 第 9 章 域控制与管理

![](img/166cd29830b01a9e3eceb33240be1bcf_365_0.png)

图 9.2 带有脚本提示的 DOS 命令行窗口。

成功登录 `SAMBABOK` 域控制器后将出现 DOS 命令行窗口（见图 9.2）。

如果你在此处收到任何错误消息，请参考“Windows 9x 域控制器错误”章节。

# 解释配置文件

成功登录到 `SAMBABOK` 域控制器后将出现 DOS 命令行窗口（见图 9.2）。

如果你在此处收到任何错误消息，请参考“Windows 9x 域控制器错误”章节。

# 用户配置文件

用户配置文件是一系列信息的集合，用于个性化用户环境……

## 第 9 章 域控制与管理

创建期间的完整路径。如果任何组件创建失败，或者无法看到路径中的任何组件，则配置文件的创建/读取将失败。

**警告！** 在使用 Windows 客户端时，不要在配置路径中包含 `[homes]` 共享。Samba 团队确定存在一个问题：Windows 客户端可以在多次登录之间保持与 `[homes]` 共享的连接。更好的解决方案是使用独立的 `[profiles]` 共享，并将登录路径设置为 `\\profiles$\$U`。

应当设置额外的 `smb.conf` 参数来处理文件名、快捷方式以及任何配置文件夹名称的情况。列表 9.2 提供了合适的选项。

# 列表 9.2 `smb.conf` 中的大小写保留参数。

```
[global] 节

preserve case = yes

short case preserve = yes

sensitive = no
```
