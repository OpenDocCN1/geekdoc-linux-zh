
```
service pop3
{
    disable         = no
socket_type     = stream
wait            = no
    user            = root
    server          = /usr/sbin/stunnel
    server_args     = stunnel pop3 -l /usr/sbin/ipop3d --pop3d
    log_on_success  += USERID
    log_on_failure  += USERID
}
```

如果你有无法使用 SSL 的 POP3 客户端软件，可以如下所示使用 POP3 重定向服务：

- 1. 在符合以下条件的系统上设置一个正常的（即不使用 Stunnel）POP3 服务器：

```
service pop3
{
    disable         = no
socket_type     = stream
wait            = no
    user            = root
    server          = /usr/sbin/stunnel
    server_args     = stunnel pop3 -l /usr/sbin/ipop3d --pop3d
    log_on_success  += USERID
    log_on_failure  += USERID
}
```

- 2. 在符合以下条件的系统上设置一个正常的（即不使用 Stunnel）POP3 服务器：

- 3. 在符合以下条件的系统上设置一个正常的（即不使用 Stunnel）POP3 服务器：

## 第 21 章：防火墙安全工具

首先，从命令行运行 `./saint`。SAINT 会启动 Web 浏览器。

### 配置审计参数

当你从安装目录使用 `./saint` 命令启动 SAINT 时，会显示一组如下的链接：

```
SAINT 首页
WWDSI
SAINT Home
数据管理
目标选择
数据分析
配置管理
SAINT 文档
故障排除
```

首先，你应该选择“配置管理”（Configuration Management）选项来配置审计参数。你会看到一个包含许多可用选项的页面。大多数默认选项都适用于你。但是，应该根据你的需求程度设置以下选项。

- 我应该使用什么种探测级别？

( ) 轻量 (Light)

( ) 普通 (Normal)

(*) 强 (Heavy)

( ) 强+ (Heavy+)

( ) Top 10 (专门针对 SANS 前10 网络安全威胁扫描)

( ) 自定义 (设置自定义扫描)

此选项用于配置探测级别；默认设置为强（Heavy）。例如，如果你了解 SANS 前 10 安全威胁（参见 http://www.sans.org/topten.htm）并想检查你的系统是否存在此类威胁，请选择 Top 10 选项。

![](img/6d176ba5e3d859ca2b04a3bba254354c_566_0.png)

当你对此页面上的任何配置选项进行更改时，使用“更改配置文件”（Change configuration file）链接保存更改。

### 审计单个系统或网络

一旦配置好 SAINT，你可以使用顶页上的“目标选择”（Target Selection）链接选择目标主机或网络进行审计。

#### 1. 你必须输入一个或多个主机名、IP 地址或子网地址进行审计。

例如，为了扫描名为 `rhat.nitec.com` 的机器，我在“目标选择”页面输入了以下信息。

主目标选择

- 主目标主机或网络，例如 `rhat.nitec.com`

- 可以是单个主机、以空格分隔的列表、IP 范围或子网：

```
(*) rhat.nitec.com
```

或者

包含包含目标主机列表的文件：

() target_file_

- 仅扫描目标主机。（禁用 smurf 检查。）

- 扫描目标主机所在子网中的所有主机。

- 如果你想扫描多个主机，可以在同一行中输入它们的主机名。用空格分隔名称。

![](img/6d176ba5e3d859ca2b04a3bba254354c_567_0.png)

如果你经常对 SAINT 多个主机，请创建一个包含主机名的文件并在此处使用它，以节省输入时间并避免错误。

![](img/6d176ba5e3d859ca2b04a3bba254354c_567_1.png)

在每个 SAINT 会话中首次扫描时，它会警告你在使用 SAINT 时会连接到外部 Web 服务器。

#### 2. 从以下选项中选择扫描级别：

扫描级别选择

SAINT 应该执行轻量级扫描、普通扫描，还是全力攻击（主）目标？

- 轻量 (Light)

- 普通 (Normal)（即使日志记录最少也可能被检测到）

(*) 强 (Heavy)（避开了已知会导致系统崩溃的 WinNT 端口）

() 强+ (Heavy+)（未避开已知会导致系统崩溃的 WinNT 端口）

() Top 10（专门针对 SANS 前10 网络安全威胁扫描）

() 自定义（设置自定义扫描）

![](img/6d176ba5e3d859ca2b04a3bba254354c_568_0.png)

扫描可能会临时占用目标机器的大量资源，因此不要在繁忙的机器上执行强扫描。请在目标系统或网络没有其他工作负载时进行扫描。

- 3. 如果你位于防火墙后，请检查下面的防火墙支持（Firewall Support）选项。

防火墙支持

扫描的主机是否在防火墙后面？如果是，你应该启用防火墙支持，否则结果可能不准确，或者你可能得不到任何结果。

(*) 无防火墙支持 (No Firewall Support)

() 防火墙支持 (Firewall Support)

![](img/6d176ba5e3d859ca2b04a3bba254354c_568_1.png)

只有当 SAINT 未运行在目标系统本身，且 SAINT 系统与目标系统或网络之间存在防火墙时，才选择防火墙支持。让 SAINT 感知防火墙的存在可以实现更准确的扫描。

- 4. 点击“开始”（Start）。

扫描完成后，你将看到结果屏幕。这是一个对名为 `rhat.nitec.com` 的单个主机运行强扫描的结果示例。

SAINT 数据收集

```
数据收集中...
03/26/01-08:41:37 bin/timeout 60 bin/fping rhat.nitec.com
03/26/01-08:41:37 bin/timeout 60 bin/tcpscan.saint
```

12754,15104,16660,20432,27665,33270,1-1525,15277-5404,5406-888,8889-999 rhat.nitec.com
