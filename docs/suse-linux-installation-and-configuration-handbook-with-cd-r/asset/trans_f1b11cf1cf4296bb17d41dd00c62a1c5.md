

## 警告

如果你使用的是 IBM 8514 或兼容的适配器，最好手动配置你的调制解调器，并且使用 ttyS3 以外的串行端口。如果因为串行端口用完而必须使用 ttyS3，在使用时应格外小心，并且只能使用表 23.2 中指定的默认串行端口设置。切勿尝试在串行脚本中进行自动配置部分；它会立即使你的系统死锁。因为这是一个启动脚本，下次启动计算机时，它也会死锁。请使用下一节“手动方法”中描述的手动方法。

表 23.2 显示了串行脚本输出的说明。请注意，设备列是基于我们对系统的了解，但不会在脚本输出中生成。

**表 23.2 串行脚本输出说明**

| Serial Port | Device | IRQ | IO | Speed |
|---|---|---|---|---|
| ttyS0=com1 | Mouse | 4 | 0x03f8 | 16550A |
| ttyS1=com2 | None | 3 | 0x02f8 | 16550A |
| ttyS2=com3 | Modem | 3 | 0x02e8 | 16550A |

如果调制解调器是 ttyS3 的所有者，你可以通过检查 isapnp.conf 文件中设置的设置或调制解调器跳线/DIP 开关的设置来验证分配给它的资源是否正确。如果你的调制解调器没有用于设置 I/O 端口的跳线/DIP 开关，你应该使用串行端口的默认 I/O 端口。表 23.3 显示了对应串行端口的默认 IRQ 和 I/O 端口。

**表 23.3 默认串行端口资源**

| Serial Port | Default IRQ | Default I/O |
|---|---|---|
| ttyS0 | 4 | 0x3f8 |
| ttyS1 | 3 | 0x2f8 |
| ttyS2 | 4 | 0x3e8 |
| ttyS3 | 3 | 0x2e8 |

## 手动方法

在编辑串行脚本时，你可能会注意到该文件主要是有组织的 setserial 命令组合。考虑串行脚本手动配置部分中存在的以下行：

```
bash#run_setserial /dev/ttyS2 uart 16550A port 0x2E8 irq 3 spd_vhi
```

上一行指示串行端口 ttyS2 使用 IRQ 3 和 I/O 0x2E8。通过修改值，你可以配置串行端口使用其他 IRQ 和其他 I/O。参考前面的表格或你的 isapnp.conf 文件以获取正确的值。在行中添加 spd_vhi 将为 33.6bps 及更高速度的调制解调器提供更好的性能。

## 告诉 YaST 调制解调器在哪里

以 root 身份发出命令 yast 启动 YaST。从 YaST 菜单中，选择 System Administration，Integrate Hardware Into the System，Modem Configuration。YaST 的调制解调器配置窗口打开（见图 23.1）。

FIGURE 23.1
YaST's Modem Configuration Window.

![](img/659f91d9da7b29976c0625e2e9628511_441_0.png)

在调制解调器配置窗口中，你会找到可以分配给调制解调器的串行端口。选择你为调制解调器设置的适用端口。

现在你已经告诉 YaST 调制解调器在哪里，YaST 将记住调制解调器位于特定的串行端口上，并在 /dev 目录中创建一个符号链接。符号链接将是 /dev/modem，其中 modem 指向调制解调器的串行端口。从现在开始，你可以使用 /dev/modem 而不必担心记住串行端口。

> **CAUTION**
> 给调制解调器一个符号链接有一个缺点。两个用户可能同时尝试使用调制解调器。其中一个可以使用 /dev/modem，而另一个使用 /dev/ttyS3。这会导致一个问题，通常通过一次锁定设备给一个用户来解决。但是，这无法做到，因为用户用两个不同的名称调用同一个设备。因此，当 ttyS3 被锁定而另一个用户尝试使用调制解调器符号链接时，他会发现它未被锁定。
> 
> 如果你是机器的唯一用户，你应该尝试始终使用调制解调器符号链接或原始设备名称。如果系统有许多用户可以访问调制解调器，你可能考虑删除符号链接并告诉用户直接使用调制解调器串行端口。

## 建立你的连接

要建立到 Internet 的 PPP/SLIP 连接，你需要拨号、登录，然后将控制权交给 PPP 守护进程。我们将讨论三种不同的方法。使用 WvDial，该软件包随 SuSE Linux 提供，被认为是 SuSE 标准。然而，使用 minicom 对于测试和故障排除至关重要。第三种方法 kppp，如果你是 KDE 用户，则被认为是一个高级且易于使用的应用程序。但是，在使用这些程序之前，你必须在 YaST 中设置 nameserver 部分（DNS）。

## 设置 YaST（域名服务器）

连接到 Internet 后，你需要访问一个 nameserver。这很重要，如果你不想仅通过 IP 访问服务器。例如，如果你启动 Netscape 并输入 http://www.suse.com，Netscape 将生成错误，即使你已连接到 Internet。域名服务器（DNS）是一种特殊的服务器程序，驻留在你的 ISP

当你输入 URL 地址时，DNS 将其解析为相应的 IP。要设置 DNS，你需要执行以下步骤：

- 1. 以 root 身份发出命令 yast 启动 YaST。
- 2. 从菜单中选择 System Administration，Network Configuration，Configuration Nameserver。Nameserver 配置对话框出现（见图 23.2）。

FIGURE 23.2 YaST Domain Name Server configuration.

![](img/659f91d9da7b29976c0625e2e9628511_442_0.png)

在 IP 地址列表中，输入主 DNS 后跟次要 DNS。在域名列表中，输入 ISP 域名。

如果你没有这些信息，请致电你的 ISP 获取，因为拥有这些信息很重要。如果你在这台机器上使用其他操作系统，你可能考虑使用其他操作系统检查值。例如，在 Windows 中你可以使用 nslookup 命令。

which prints the DNS server when it starts. 以下示例说明了在 Windows NT 平台上运行时 nslookup 的启动情况：

```
C:\>nslookup
Default server: dns.wayout.net
Address: 163.121.142.2
```

此示例中使用的 ISP 的主 DNS 为 163.121.142.2。

## 修改 pppd 选项

pppd 是 PPP 守护进程，负责在 TCP/IP 网络上协商 PPP 协议。在你拨号到 ISP 并登录后，你必须将控制权交给 pppd。这是通过发出命令 pppd 完成的。当 pppd 启动时，它会查找 /etc/ppp/ options 目录，即 pppd 配置文件。为了节省时间，以下情况你不必编辑此文件：

- - 你计划使用 wvdial，因为它会输出正确的 /etc/ppp/options 文件。
- - 你计划使用 kppp。

如果你需要编辑此文件，本节将告诉你 pppd 的最重要的选项以及如何在文件中包含它们。SuSE 附带的 /etc/ppp/options 文件记录详尽且易于理解。

主要选项列在表 23.4 中。

Table 23.4 Main Options In the pppd Configuration File

| Option | Meaning |
|---|---|
| Noipdefault | Your ISP allocates IPs dynamically |
| Lock | Only the pppd should use the modem while connected |
| Modem | Usage of modem control lines |
| 115200 | The connection speed. (230400/115200/57600/38400/19200/9600) |

## 使用 WvDial

WvDial 是一个智能应用程序。它之所以智能，是因为它具有特殊的自动配置，会搜索调制解调器技术，并内置了登录字符串数据库。这使得 wvdial 的配置非常简单直接。该软件包包含以下程序：

- - wvdialconf—负责搜索调制解调器并为 WvDial 创建配置文件。默认配置文件存储在 /etc/wvdial.conf 中。
- - wvdial.tel—负责修改配置文件以插入你的账户特定信息（你的账户名、ISP 电话号码等）。
- - wvdial—负责使用前面列出的程序创建的配置文件连接到 Internet。

