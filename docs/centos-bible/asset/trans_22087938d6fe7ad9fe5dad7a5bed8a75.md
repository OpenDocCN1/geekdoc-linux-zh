

## 安全性

### 图 13-1

使用**安全性级别配置**窗口设置基本防火墙。

![](img/2f265415ceec72538dd3c78ffca75c10_546_0.png)

**注意**

> 如果您需要了解特定服务的用途，请将鼠标悬停在此窗口中引起您兴趣的服务名称上，以获取更详细的描述。

-   **其他端口** — 您可以通过将其他端口号添加到“其他端口”框中允许访问它们。选择*添加*，然后选择协议类型（TCP 或 UDP）以及您想要允许使用的端口号对。可供选择的端口约有 1,000 个。若要启用不同的端口，请选中“用户定义”框，输入端口号，并选择您要启用的协议。完成后点击**确定**。有关不同服务使用端口的列表，可以在*etc/services*中找到（*etc/services* 文件和端口将在本章后续部分详细讨论）。

在点击*应用*保存设置之前，请考虑这样做会覆盖现有的防火墙规则。如果您手动编辑过配置文件（*etc/sysconfig/iptables*），这些更改将被覆盖。继续操作前请对该文件进行备份。

配置*iptables*以设置日志记录、端口转发、网络地址转换以及其他功能，都可以手动完成，方法如后续章节所述。

### 配置 iptables 防火墙

本章关于 iptables 的其余部分描述了在 Linux 中手动管理 iptables 防火墙的更多方式。我还介绍了如何实现防火墙配置窗口中不可用的特殊功能，例如端口转发和 NAT。

513

## 第三部分 管理

### 开启 iptables

iptables 防火墙功能，也称为*netfilter*，是安装 CentOS 时默认的防火墙软件。

本节描述如何开启 iptables 并为几种不同的情况设置防火墙规则。它还说明了如何开启与防火墙相关的功能，使防火墙能够执行网络地址转换 (NAT)、IP 伪装、端口转发和透明代理。

**注意**

> 如果您使用某些服务，CentOS 启动脚本会在您的防火墙中打开通道，即使这些服务未在您的 iptables 配置中明确启用，它们也会生效。例如，NTP（用于从网络时间服务器设置系统时间）和 DNS 解析（用于联系 DNS 服务器解析地址）都会在您的防火墙中打开所需的端口。

以下过程描述了如何在您的 CentOS 系统上启动 iptables。

1.  设置 iptables 脚本在启动时自动运行：

    ```
    # chkconfig iptables on
    ```

2.  在启动 iptables 之前，必须确保 /etc/sysconfig/iptables 文件中放置了一套可用的规则集。要创建这些规则，请参考后续章节中的示例。（如果没有配置文件，iptables 会静默失败。）

**提示**

> 如果您是 iptables 的新手，可以在 CentOS 安装过程中通过配置防火墙来获取一套可用的默认值。建议选择启用防火墙，并只启用您准备提供的那些服务。生成的 /etc/sysconfig/iptables 文件将让您研究 CentOS 如何创建其防火墙规则。

3.  如果您正在执行 NAT 或 IP 伪装，请开启 IP 数据包转发。允许此功能的一种方法是修改 /etc/sysctl.conf 文件中 `net.ipv4.ip_forward` 的值为 1。以 root 用户身份使用任何文本编辑器打开该文件，并将该行更改为如下所示：

    ```
    net.ipv4.ip_forward = 1
    ```

4.  重启网络接口以使 IP 数据包转发生效。

    ```
    # /etc/init.d/network restart
    ```

5.  规则文件就位后，启动 iptables：

    ```
    # /etc/init.d/iptables start
    ```

6.  此时，iptables 已安装为您的防火墙。您可以使用 `lsmod` 命令检查 iptables 使用的模块是否已加载。以下是一些示例：

    ```
    # lsmod | less
    Module             Size Used by
    nf_conntrack_ftp   10656  0
    ```

7.  如果您想允许来自局域网中计算机的被动 FTP 或 IRC 连接，可能需要通过将它们添加到 /etc/modprobe.conf 文件中来加载这些模块。基本连接跟踪模块 ip_conntrack 通常默认已加载。关于被动 FTP 和 IRC 的描述见防火墙示例章节之后。

如果 /etc/sysconfig/iptables 文件中有错误，您可以复制该文件，然后尝试通过运行 system-config-securitylevel 并设置基本防火墙来创建可用的配置。之后，您可以修改防火墙以添加您需要的功能。

![](img/2f265415ceec72538dd3c78ffca75c10_548_0.png)

随着添加 iptables 规则，必须加载更多的模块。当输入新规则时，适当的模块应自动加载。在添加几条规则后，再次运行 `lsmod | less` 查看添加了哪些模块。请注意，即使您决定停止 iptables，这些模块也不会被卸载。它们将保持加载状态，直到下次重启或您手动移除它们（`modprobe -r`）。

后续章节包含 iptables 防火墙规则的示例。

### 创建 iptables 防火墙规则

配置 iptables 的一种方法是从命令行开始添加和删除内核中的规则。然后，当您获得一组喜欢的规则后，保存当前在系统上运行的规则。用于创建防火墙规则并将其永久化的工具如下：

-   **iptables** — 使用此命令来追加（`-A`）、删除（`-D`）、替换（`-R`）或插入（`-I`）规则。使用 `-L` 选项列出所有当前规则。

-   **service iptables save** — 使用此命令保存来自内核的规则并将其安装到配置文件中。

-   **/etc/sysconfig/iptables** — 这是包含通过 `service iptables save` 命令保存的规则的文件。

-   **/etc/sysconfig/iptables-config** — 您可以将管理 iptables 规则的设置添加到 iptables-config 文件中。例如，可以在 `IPTABLES_MODULES` 行中添加 iptables 模块，如 `ip_conntrack` 及本章后续描述的其他模块，以自动加载。您还可以设置 iptables 停止时是否将运行内核中的 iptables 表保存到文件。

-   **/etc/init.d/iptables** — 这是 iptables 启动脚本，必须在每次 CentOS 重启时自动运行。启动时，它清除所有 iptables 规则和计数器，并从 `/etc/sysconfig/iptables` 文件安装新规则。您还可以在命令行中使用此脚本的不同选项来检查 `iptables` 的状态（`status`）或为您运行 `iptables-save` 以保存当前规则（`save`）。

为了帮助您入门 iptables，我提供了一组示例规则及其在不同情况下如何修改这些规则的说明。以下是如何加载和保存以下示例中描述的规则集的方法：

1.  停止 iptables 并清除所有现有规则：

    ```
    # /etc/init.d/iptables stop
    ```

2.  使用任何文本编辑器，将下例中显示的规则添加到文件中。根据您的情况修改规则并保存文件。

3.  以*root*用户身份，将文件作为 shell 脚本运行。例如，如果您将文件命名为 *firescript*，可以按如下方式运行：

    ```
    # sh firescript
    ```

4.  查看规则如何加载到内核中：

    ```
    # iptables -L
    ```

5.  如果一切正常，将内核中当前的规则保存到 `/etc/sysconfig/iptables` 文件：

    ```
    # cp /etc/sysconfig/iptables /etc/sysconfig/iptables-old
    # service iptables save
    ```

6.  启动 iptables：

    ```
    # /etc/init.d/iptables start
    ```

从此以后，每次重启或重启 iptables 时都会读取这些规则。请保存一份用于创建规则的脚本副本，以备不时之需。

### 示例 1：共享互联网连接的防火墙（加服务器）

由于防火墙配置因目标不同而可能大相径庭，我通过几个不同的示例设置说明了如何配置防火墙。这些设置结合了不同级别的安全性要求。

本示例展示了一个家庭或小型办公室局域网，其中 CentOS 系统作为 iptables 防火墙，位于局域网和互联网之间。该防火墙计算机还充当 Web 服务器、FTP 服务器和 DNS 服务器。图 13-2 显示了此配置。

如果您想使用接下来的示例防火墙脚本，必须更改以下信息以匹配您的配置：

