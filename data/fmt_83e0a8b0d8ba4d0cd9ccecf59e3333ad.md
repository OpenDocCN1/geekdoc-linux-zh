
在开始之前，最好杀死服务器上所有正在运行的 Samba 相关守护进程。杀死所有可能正在运行的 `smbd`、`nmbd` 和 `winbindd` 进程。为了使用 PAM，请确保您拥有提供 `/etc/pam.d` 目录结构的标准 PAM 包，其中包括 PAM 感知服务所使用的 PAM 模块、几个 PAM 库，以及 PAM 的 `*/usr/doc*` 和 `*/usr/man*` 条目。如果也安装了 `pam-devel` 包，Winbind 在 Samba 中的构建会更好。该包包含编译 PAM 感知应用程序所需的头文件。

### 23.5.3.1 在 Linux 和 Solaris 上配置 nsswitch.conf 和 Winbind 库

PAM 是大多数现代 UNIX/Linux 系统的标准组件。不幸的是，很少有系统安装构建 PAM 启用版 Samba 所需的 `pam-devel` 库。此外，Samba-3 可能会自动将 Winbind 文件安装到系统中的正确位置，因此在深入进行之前，请确保检查以下配置是否真的必要。您可能只需要配置 `/etc/nsswitch.conf`。

通过 `nsswitch` 运行 `winbindd` 守护进程所需的库需要复制到其正确的位置：

```bash
root# cp ../samba/source/nsswitch/libnss_winbind.so /lib
```

我还发现有必要创建以下符号链接：

```bash
root# ln -s /lib/libnss_winbind.so /lib/libnss_winbind.so.2
```

而在 Sun Solaris 的情况下：

```bash
root# ln -s /usr/lib/libnss_winbind.so /usr/lib/libnss_winbind.so.1
root# ln -s /usr/lib/libnss_winbind.so /usr/lib/nss_winbind.so
root# ln -s /usr/lib/libnss_winbind.so /usr/lib/nss_winbind.so.2
```

作为 root，编辑 `/etc/nsswitch.conf` 以允许用户和组条目对 `winbindd` 守护进程可见。编辑后，我的 `/etc/nsswitch.conf` 文件看起来像这样：

```bash
passwd:	files winbind
shadow:	files
group:	files winbind
```

`winbindd` 守护进程所需的库将在系统下次重启时自动进入 `ldconfig` 缓存，但手动操作更快（且无需重启）：

```bash
root# /sbin/ldconfig -v | grep winbind
```

这使得 `libnss_winbind` 对 `winbindd` 可用，并报告动态链接加载器当前使用的搜索路径。使用 `grep` 过滤 `ldconfig` 命令的输出，以便我们可以看到该库确实被动态链接加载器识别的证据。

Sun Solaris 的动态链接加载器管理工具称为 `crle`。使用此工具是必要的，以指示动态链接加载器搜索包含不属于原始操作系统平台的一部分的库文件的目录。以下示例展示了如何使用此工具将目录 `/usr/local/lib` 添加到动态链接加载器的搜索路径中：

```bash
root# crle -u -l /usr/lib:/usr/local/lib
```

在不带参数执行时，`crle` 报告当前的动态链接加载器配置。这里进行了演示：

```bash
root# crle

Configuration file [version 4]: /var/ld/ld.config
    Default Library Path (ELF):    /lib:/usr/lib:/usr/local/lib
    Trusted Directories (ELF):      /lib/secure:/usr/lib/secure    (system default)

Command line:
    crle -c /var/ld/ld.config -l /lib:/usr/lib:/usr/local/lib
```

显然，`/usr/local/lib` 目录被包含在动态链接库搜索中，以满足对象模块依赖关系。

### 23.5.3.2 AIX 上的 Nss Winbind

（本节仅适用于运行 AIX 的用户。）

Winbind AIX 标识模块在 Samba 源代码的 `nsswitch` 目录中构建为 `libnss_winbind.so`。可以将此文件复制到 `/usr/lib/security`，并且 AIX 命名约定表明它应该命名为 `WINBIND`。然后可以添加类似以下配置节：

```bash
WINBIND:
       program = /usr/lib/security/WINBIND
       options = authonly
```

到 `/usr/lib/security/methods.cfg`。此模块仅支持标识，但有报道称使用标准的 Winbind PAM 模块进行身份验证取得了成功。配置可加载身份验证模块时要谨慎，因为配置错误可能导致无法登录系统。有关 AIX 身份验证模块 API 的信息可以在描述 AIX 可加载身份验证模块编程接口[^2] 的“Kernel Extensions and Device Support Programming Concepts for AIX”文档中找到。有关管理模块的更多信息可以在 System Management Guide: Operating System and Devices[^3] 中找到。

### 23.5.3.3 配置 smb.conf

`smb.conf` 文件中需要几个参数来控制 `winbindd` 的行为。这些参数在 `winbindd(8)` man 页中有更详细的描述。我在 Example 23.5.1 中显示的 `smb.conf` 文件已修改，以包含 `[global]` 部分中必要的条目。

![Example 23.5.1](img/86d74c6cc862465e3a42e6dc3c90935a_505_0.png)

### 23.5.3.4 将 Samba 服务器加入 PDC 域

所有参与域安全的机器都应该是域的成员。这也适用于 PDC 和所有 BDC。

加入域的过程需要使用 `net rpc join` 命令。此过程通过 MS DCE RPC 与其将注册的域控制器（通常是 PDC）通信。当然，这意味着目标域控制器上必须正在运行 `smbd` 进程。因此，有必要临时在 PDC 上启动 Samba，以便它可以加入自己的域。

输入以下命令使 Samba 服务器加入域，其中 `PDC` 是您的 PDC 的名称，`Administrator` 是在域中具有管理员权限的域用户。

![Join Domain Command](img/86d74c6cc862465e3a42e6dc3c90935a_506_0.png)

> 在尝试将机器加入域之前，请验证目标域控制器（通常是 PDC）上正在运行 Samba，并且能够通过端口 137/udp、135/tcp、139/tcp 和 445/tcp（如果是 Samba 或 Windows Server 2Kx）访问它。

`net rpc join` 功能的使用如下所示：

```bash
root# /usr/local/samba/bin/net rpc join -S PDC -U Administrator
```

对该命令的正确响应应该是 “Joined the domain DOMAIN”，其中 `DOMAIN` 是您的域名称。

### 23.5.3.5 启动和测试 winbindd 守护进程

最终，您可能希望修改 Samba 启动脚本，以便在其他 Samba 部分启动时自动调用 `winbindd` 守护进程，但首先测试仅 Winbind 部分是可能的。要启动 Winbind 服务，作为 root 输入以下命令：

```bash
root# /usr/local/samba/sbin/winbindd
```

使用指向 `winbindd` 可执行文件位置的适当路径。

![Winbindd Output](img/86d74c6cc862465e3a42e6dc3c90935a_506_1.png)

> 启动 Winbind 服务的命令假定 Samba 已安装在 `/usr/local/samba` 目录树中。如果这不是您系统上 `winbindd` 的位置，您可能需要搜索 Samba 文件的位置。

`Winbindd` 现在也可以以“双守护进程模式”运行。这将使其作为两个进程运行。第一个将回答来自缓存的所有请求，从而加快对客户端的响应。另一个将更新第一个刚刚响应过的查询的缓存。这样做的优势在于响应保持准确且更快。您可以通过在命令行中添加 `-B` 来启用双守护进程模式：

[^1]: <http://samba.org/>

[^2]:

[^3]:
