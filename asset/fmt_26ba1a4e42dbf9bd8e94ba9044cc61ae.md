
应该按照顺序执行测试，因为每个后续测试都可能取决于 Samba 服务器中应该存在且已通过上一个测试证明的功能。这些测试的版本做了以下假设：

- Samba 服务器上安装了 2.0.0 或更高版本的 Samba 套件。
- Samba 服务器名为 `BIGSERVER`。
- 使用名为 `ACLIENT` 的 PC。

客户端和服务器之间存在适当的网络连接，PC 运行 Windows 95、Windows NT（工作站或服务器）或 Linux。

> 注意：其他类型客户端的操作类似。

`BIGSERVER` 服务器包含一个 Samba 发行版中公开提供的共享 `tmp`。`smb.conf` 文件中 `tmp` 共享的条目所示：

```
[tmp]
comment - temporary files
path - /tmp
read only - yes
```

记录所有返回的消息，以便你确认 Samba 服务器的配置符合你的预期。记录任何返回的错误信息尤为重要。

如果出现任何错误消息，其中包含服务器不友好的注释（使用了多么令人悦的消息啊！），你应该检查网络配置，并确定 IP 解析是否正确以及 `/etc/resolv.conf` 条目是否正确。你还应该确认服务器的主机名已注册在 DNS 中，或者服务器无法访问。

### 测试 1：检查 Samba

第一个测试是检查 Samba 服务器是否正在运行并响应请求。要做到这一点，请从客户端机器使用 `smbclient` 工具：

```
smbclient -L BIGSERVER
```

输出应显示服务器上可用共享列表。如果你看到了 `tmp` 共享，说明 Samba 服务器工作正常。

### 测试 2：测试 tmp 共享

下一个测试是查看你是否可以访问并写入 `tmp` 共享：

```
smbclient -L BIGSERVER -N tmp
```

连接到共享后，尝试创建一个文件：

```
put local.txt test.txt
```

如果文件创建成功，则说明 `tmp` 共享工作正常。

### 测试 3：测试文件权限

最后一个测试是检查文件权限是否设置正确。尝试读取你刚刚创建的文件：

```
get test.txt
```

如果你可以读取该文件，则权限设置正确。

## 立即解决方案

`oplock break wait time = 10`

`smbrun = /usr/bin/smbrun`

`config file = -`

`preload = -`

`lock dir = /var/lock/samba`

`default service = -`

`message command = -`

`dfree command = -`

`valid chars = 192.168.1.255`

`remote browse sync = 192.168.1.255`

`socket address = 0.0.0.0`

`homedir map = -`

`time offset = 0`

`unix realname = No`

`nis homedir = No`

`panic action = -`

`comment = -`

`path = -`

`alternate permissions = No`

`revalidate = No`

`username = =`

`guest account = nobody`

`invalid users = =`

`valid users = =`

`admin users = =`

`read list = -`

`write list = =`

`force user = -`

`force group = -`

`read only = Yes`

`create mask = 0744`

`force create mode = 00`

`directory mask = 0755`

`force directory mode = 00`

`guest only = No`

`guest ok = No`

`only user = No`

`hosts allow = 192.168.1.127.`

`hosts deny = -`

`status = Yes`

`max connections = 0`

`min print space = 0`

`strict sync = No`

`sync always = No`

`print ok = No`

## 12. Samba 故障排除

# 第 12 章 Samba 故障排除

`postscript = No`

`printing = bsd`

`print command = l1pr -r -P%p %%`

`l1pq command = l1pq -P%p`

`lplrm command = l1rm -P%p %J`

`lppause command = -`

`presume command = -`

`queuepause command = -`

`queuerume command = -`

`printer name = -`

`printer driver = NULL -`

`printer driver location = -`

`default case = lower`

`case sensitive = No`

`preserve case = Yes`

`short preserve case = Yes`

`mangle case = No`

`mangling char = ~`

`hide dot files = Yes`

`delete veto files = No`

`veto files = -`

`hide files = -`

`veto oplock system = No`

`map hidden = No`

`map archive = Yes`

`mangled names = Yes`

`mangled map = -`

`browseable = Yes`

`blocking locks = Yes`

`fake oplocks = No`

`locking = Yes`

`mangle locks = Yes`

`oplockocks = Yes`

`oplock contention limit = 2`

`strict locking = No`

`share modes = Yes`

`copy = -`

`include = -`

`exec = -`

`postexec = -`

`root preexec = -`

`root postexec = -`

`available = Yes`

`volume = -`

`fstype = NTFS`

```
set directory = No
wide links = Yes
follow symlinks = Yes
dont descend =
magic script =
magic output =
delete readonly = No
dos filetimes = No
dos datetime resolution = No
fake directory create times = No
```

`[homes]`

`comment = 用户主目录`

`read only = No`

`browseable = No`

`[printers]`

`comment = 所有打印机`

`path = /usr/sp/samba`

`print ok = Yes`

`[tmp]`

`comment = 测试`

`path = /tmp`

`read only = yes`

`[root@linuxserver ~]`

您应该检查此命令的输出以确认任何错误。如果您发现了任何错误，应直接使用文本编辑器或使用 `SWAT` 来修改 `smb.conf` 配置文件。

`smb.conf` 的默认位置是 `/usr/local/samba/lib`，尽管它也存在于 `/etc`。

### 测试 2：检查网络连接

第二个测试确认了从客户端到服务器的网络连接，这是通过在客户端命令行提示符运行 `ping servername` 实现的。在成功成功 后，反向重复操作运行命令 `ping clientname`。这将确认客户端和服务器之间存在网络连接性，并且客户端的 IP 名称解析按预期工作。如果出现任何其他消息，则表明存在底层网络问题，与硬件或 TCP/IP 配置有关。如果其中任何一个产生错误，您将需要咨询网络管理员来修复问题。

![](img/166cd29830b01a9e3eceb33240be1bcf_514_0.png)

# 第 12 章 Samba 故障排除

“未找到主机”（Host Not Found）或类似的消息可能表明从主机名解析 IP 地址时存在问题。这表明 DNS 软件或 `/etc/hosts` 文件设置存在问题。虽然 Samba 操作并不一定需要 DNS，但建议创建相应的 hosts 条目。

您正在使用的网络在服务器和客户端之间可能使用了路由器或防火墙，具有某些阻止正常运行的额外网络配置。这种情况，您将需要寻求网络管理员的帮助。

### 测试 3：确认 smbd 正在运行

第三个测试开始某些 Samba 客户端软件来确认 Samba 服务器程序 `smbd` 正在运行。
