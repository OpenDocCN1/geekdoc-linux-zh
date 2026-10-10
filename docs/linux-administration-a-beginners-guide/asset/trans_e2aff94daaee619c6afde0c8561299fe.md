

## Samba 配置（`.configure`）选项

| Samba 配置（`.configure`）选项 | 描述 |
| :--- | :--- |
| **--with=smbmount** | 用于在 `smbmount` 命令中包含支持。（此功能目前特定于 Linux。未来的 Samba 版本将包含一个通用的挂载工具，该工具可跨多个操作系统工作。） |
| **--with=pam** | 如果您的 Linux 发行版自带 PAM（如 Red Hat 那样），请启用此功能，以便 Samba 可以利用通过密码认证模块（Password Authentication Module）提供的选项。 |

5.  使用您为 Samba 安装所选的选项运行 `./configure` 命令。例如，若要支持 `smbmount` 和 PAM 功能，请键入以下命令：

    ```bash
    [root@ford source]# ./configure --with=smbmount --with=pam
    ```

6.  像这样运行 `make`：

    ```bash
    [root@ford source]# make
    ```

7.  像这样运行 `make install`：

    ```bash
    [root@ford source]# make install
    ```

    此时 Samba 已安装到 `/usr/local/samba` 目录中。

8.  Samba 手册页的默认位置使得在使用 `man` 时无法访问它们。为了使它们可用，键入以下命令：

    ```bash
    [root@ford samba]# cd /usr/local/samba/man
    [root@ford man]# cp man1/* /usr/man/man1
    [root@ford man]# cp man5/* /usr/man/man5
    [root@ford man]# cp man7/* /usr/man/man7
    [root@ford man]# cp man8/* /usr/man/man8
    ```

9.  现在将默认配置文件复制到 `/usr/local/samba/lib` 目录中。假设您将 Samba 解压到了 `/usr/local/src` 目录，那么默认配置文件将位于 `/usr/local/src/samba-2.0.5a/examples` 目录中。要复制正确的文件，请键入以下命令：

    ```bash
    [root@ford samba]# cd /usr/local/src/samba-2.0.5a/examples
    [root@ford examples]# cp smb.conf.default/... /usr/local/samba/lib/smb.conf
    ```

    *（注：OCR 文本中的“smb.conf.default/...”可能暗示了一个路径。根据上下文，它应该是 `cp smb.conf.default /usr/local/samba/lib/smb.conf` 或类似形式。我将保留逻辑但清理换行符。）*

    基于上下文的更正命令序列：
    ```bash
    [root@ford samba]# cd /usr/local/src/samba-2.0.5a/examples
    [root@ford examples]# cp smb.conf.default /usr/local/samba/lib/smb.conf
    ```

10. Samba 目录上的默认权限仅允许 root 用户访问它们。您需要允许其他用户访问文件，除了私有目录（private directory）。为此，请发出这些命令：

    ```bash
    [root@ford man]# cd /usr/local/samba
    [root@ford samba]# chmod -R 755 bin lib lib man var
    ```

## 设置 SWAT

SWAT 是 Samba Web 管理工具，您可以通过浏览器界面管理 Samba。它是手动编辑 Samba 配置文件的绝佳替代方案，但请不要让它让您觉得配置文件很复杂！

使 SWAT 与其他基于浏览器的管理工具略有不同的是，SWAT 不依赖 Web 服务器（如 Apache）。相反，SWAT 在无需实现完整 Web 服务器的情况下执行所有必要的 Web 服务器功能。这主要通过通过 inetd 守护进程运行来实现。

设置 SWAT 非常简单。步骤如下：

1.  将 `/usr/local/samba/swat` 的权限设置为全局可读：

    ```bash
    [root@ford samba]# chmod -R 755 /usr/local/samba/swat
    ```

2.  编辑 `/etc/services` 文件，使其包含以下行：

    ```
    swat    901/tcp
    ```

3.  编辑 `/etc/inetd.conf` 文件，使其包含以下行：

    ```
    swat    stream    tcp    nowait:400    root    /usr/local/samba/bin/swat swat
    ```

4.  使用以下命令向 inetd 进程发送 HUP 信号：

    ```bash
    [root@ford ~]# kill -1 `ps -C inetd|awk '{if (/$inetd/) print $1}'`
    ```

    这样你就完成了！只需将 Netscape Navigator 指向端口 901 上的 Samba 服务器，即可进入 SWAT 登录提示界面。例如，如果您的服务器主机名是 `ford`，请使用 URL `http://ford:901`。要执行所有服务器任务，您需要以 root 身份登录。

> **警告：** 通过 SWAT 以 root 身份登录会导致 root 密码从 Web 浏览器发送到 Samba 服务器。因此，避免在不可信网络上执行管理任务。最好直接在服务器上运行 Navigator，或者在客户机主机和 Samba 服务器主机之间设置 SSH 隧道。

## Samba 管理

本节描述了 Samba 管理的一些问题。我们将了解如何启动和停止 Samba，如何使用 SWAT 执行常见的管理任务，以及如何 **smbclient** 使用。最后，我们将研究使用加密密码的过程。

### 启动和停止 Samba

大多数 Linux 发行版都有脚本可以启动和停止 Samba，您无需太费心。如果您使用的是随 Linux 发行版附带 Samba 安装，您不需要更改这些脚本。它们处理 **启动时引导** 和 **停止关机**。

> **注意：** 如果您没有用于自动启动 Samba 的脚本，花费一些时间编写它们是个好主意。请参阅第 7 章了解编写和放置脚本的详细信息。

启动 Samba 只需两个步骤。首先，启动 **smbd** 进程。虽然您可以在命令行上设置许多参数，但通常最好在配置文件（*smb.conf*）中设置它们。如果您使用 SWAT，它会将该文件为您保存。您可能拥有的唯一命令行参数是 `-D` 选项，告诉 Samba 以 **守护进程** 方式运行：

```bash
[root@ford samba]# /usr/local/samba/bin/smbd -D
```

接下来，启动 **nmbd** 进程。与 **smbd** 一样，许多参数可以通过命令行设置，但如果您将配置更改保留在 *smb.conf* 文件中，维护起来可能更容易。您可能拥有的唯一命令行参数是 `-D` 选项，告诉 **nmbd** 以 **守护进程** 方式运行。

```bash
[root@ford samba]# /usr/local/samba/bin/nmbd -D
```

> **注意：** 您应该以 root 用户身份启动 **smbd** 和 **nmbd**。

停止 Samba 比启动它稍显棘手。使用 `ps` 命令列出所有 Samba 进程。从这个列表中，找到由 root 拥有的 **smbd** 实例并终止该进程。这将终止所有其他 Samba 连接。

> **注意：** 如果您对 Samba 的配置进行了更改，您将需要停止然后重新启动 Samba，以便这些更改生效。重新建立连接是客户机的责任。这是 SMB 协议的一部分，而不是 Samba 的限制。

## 使用 SWAT

在 Samba 2.0 版本之前，配置它的官方方法是编辑 **smb.conf** 文件。虽然该文件在性质上冗长且易于理解，但相当庞大且笨拙。这也意味着在 NT 下设置共享比使用 Samba 设置共享仍然更容易。许多个人开发了编辑过程的图形前端。许多这些工具仍在使用并得到增强——您可以通过访问 Samba 的网站 http://www.samba.org 阅读更多关于它们的信息。然而，从 2.0 版本开始，Samba 附带 SWAT，即 Samba Web 管理工具。

使用 SWAT 非常容易。所有配置都通过 Web 浏览器完成。然后 SWAT 从浏览器获取信息并构建 **smb.conf** 文件。对于习惯编辑配置文件的人来说，这可能会有一点烦恼，因为 SWAT 不会在配置文件本身中保留注释。因此，服务器配置文档必须保持外部于 Samba，而不是以注释形式嵌入配置文件中。

> **注意：** 如果您更喜欢在配置文件中保留注释，或者如果您需要编写一些自己的工具来自动化某些管理任务，您不应该使用 SWAT。这里体现了基于文本的配置文件之美。您有一个选择——如果您不想要 GUI，可以使用不使用 GUI 的方式，并且由于文件格式是公开的，任何人想要编写自己的管理工具都可以。

### SWAT 菜单

当您连接到 SWAT 并以 root 登录时，您将看到图 20-1 中显示的主菜单。从这里，您可以找到几乎所有关于 Samba 配置文件、守护进程和相关程序的文档。所有链接均不指向外部网站，因此您可以随时阅读它们而无需连接网络。

窗口顶部是用于以下菜单选项的按钮：

-   **主页**：主菜单页面
-   **全局**：影响 Samba 所有操作方面的配置选项
-   **共享**：用于设置磁盘共享及其相应选项
-   **打印机**：用于设置可让 NT 客户端访问的打印机
-   **状态**：**smbd** 和 **nmbd** 进程的状态，包括连接到这些进程的所有客户端及其正在执行的操作（与 **smbstatus** 命令行程序列出的信息相同）
-   **查看**：生成的 **smb.conf** 文件
-   **密码**：密码设置

