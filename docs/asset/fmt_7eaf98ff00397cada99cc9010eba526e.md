
由于本章涵盖了 GUI 工具和手动编辑文本，我想提醒你注意一个潜在问题。如果在手动编辑文本文件时，你无意中做了会让 GUI 工具困惑的操作。这通常不是灾难性的，但可能会令人困惑。通常，GUI 工具远没有 SAMBA 本身那么先进，因此某些配置可能会有问题。你可以通过使用 GUI 工具创建基本配置，然后手动进行微调来避免这种情况。

## 第18章：文件共享解决方案 303

现在你可以创建你的配置文件了。如图 18-7 所示，`smb.conf` 文件被成若干部分，每个部分由方括号中的关键字表示，例如 `[global]`。一个部分持续到遇到另一个括号关键字。每个部分内包含若干参数，格式如下：

```
name = value
```

其中 `name` 是参数名称，`value` 是你希望该参数的设置。例如，如果你将共享的权限设置为可读/写，你可以这样设置参数：

```
writable = yes
```

### 全局设置

你配置文件中的第一个部分应该是 `[global]` 部分。在此部分中，你可以定义对 SAMBA 服务器提供的所有共享生效的选项。你也可以定义不适用于任何特定共享但与服务器本身运行相关的选项。这是一个示例：

```
[global]
workgroup = test
security = file
server string = Samba
```

注意，全局定义了三个参数，它们与你设置的选项完全相等。事实上，`system-samba` 做的只是将这些选项写入 `smb.conf`。

### 共享设置

现在你定义了全局参数，就可以设置一个共享了。共享的关键字是你想要给它起的名称；在此情况下是 `samba-share`。

```
[samba-share]
comment = Shared directory
path = /
writable = yes
guest ok = yes
```

就这样。`samba-share` 部分与全局部分就是设置服务器的所有内容。保存文件，确保它的路径为 `/etc/samba/smb.conf`。

## 用户认证

有时你希望将特定共享的访问限制给特定用户或组。例如，假设让每个用户访问自己的家目录。你需要设置如下的共享：

```
[homes]
comment = Home Directories
browsable = no
writable = yes
security = user
```

注意你不需要为家目录指定路径名称。服务器可以通过 `/etc/passwd` 文件中关于每个用户的家目录的信息动态创建这些。通过指定 `security=user`，你确保每个用户只能访问自己的家目录而不能访问别人的。

剩下的就是启动（重启）服务器。在上节中，你学习了如何使用 Fedora 的 `system-config-services` 启动服务器。在这里，你看到适用于 Knoppix 系统的文本命令。

### 注意

以下程序适用于许多发行版而不是 Knoppix。前提是不同的发行版会将启动脚本放在不同的位置。通常，如果你能找到名为 `init.d` 的目录，就在那里。如果你没有找到 `init.d` 目录，你的发行版可能没有使用这种启动程序。在这种情况下，你需要查阅你发行版的文档。

在 Knoppix 中，打开终端窗口，并使用 `su` 命令（以及密码）获取超级用户权限（如果你尚未这样做）。如果服务器尚未运行，给出以下命令：

```
/etc/init.d/samba
```

如果它已经在运行，输入以下内容：

```
/etc/init.d/samba restart
```

如果你不知道它是否在运行，运行以下命令查看：

```
/etc/init.d/samba status
```

## 第18 章：文件共享解决方案 305

### 提示

与其每次尝试启动服务器时都检查其状态，你始终可以直接使用 `/etc/init.d/samba restart` 来启动它。如果服务器尚未运行，程序中停止服务器的部分会直接失败，然后直接跳到重新启动的部分。这节省了你检查其是否已经运行的时间。

## 使用 SWAT

`SWAT`（SAMBA 网页管理工具）是一个在你的系统上安装小型 Web 服务器的程序。一旦安装，你就可以访问该服务器并并在 Web 浏览器中使用它来配置你的 SAMBA 服务器。这样做的好处是，你可以从任何机器配置服务器；而无必在运行 SWAT 的同一台机器上操作。

缺点是 SWAT 具有了一定的安全风险。这并不是严重的问题——每当你会在系统上运行服务器（包括 SAMBA 服务器）时，你都会创建一个可能被黑客利用的漏洞。这并不意味着你不应该运行 SWAT，但确实意味着你需要经过一些步骤才能让运行起来。以下是获取 SWAT 所需执行的步骤说明：

- 1. 确保 SWAT 已安装。就像你安装 SAMBA 软件包一样，你需要确保安装了 SWAT 软件包。SWAT 软件包有时标记为 `samba-swat`，有时标记为 `swat`。检查软件包是否已安装，如果没有，请安装它。如果你的发行版自带 SAMBA，你可能已经在安装介质中随同拥有了 SWAT。如果没有，你可以从 www.samba.org 下载。
- 2. 确保服务已注册。假设你正在使用包管理器安装 SWAT，这通常会自动为你完成，但检查一下总是有好的。给出命令：

```
more /etc/services
```

使用空格键滚动查看文件。你应该能看到像这样的一行：

```
swat 901/tcp # Samba Web Administration Tool
```

SWAT 文件的通常位置是 `/usr/bin/swat`、`/usr/share/swat`、`/opt/swat`。如果你没有这些文件或目录，那么你可能没有安装 SWAT。
- 3. 配置 inet.d 或 xinet.d。根据你的发行版，将有一个名为 `inet.d` 或 `xinet.d` 的程序。这些是超级服务器，用于处理对不经常使用的服务的网络连接。`xinet.d` 和 `inet.d` 的功能本质上相同，但 `xinet.d` 更新且更具可配置性。以下说明首先描述如何通过 `inet.d` 配置 SWAT，然后转向稍微复杂的 `xinet.d`。

- a. 鉴于 Knoppix 使用 `inet.d`，我用它作为配置 `inet.d` 的示例。首先，打开终端窗口并切换到超级用户（`su -`）。然后，用文本编辑器打开 `/etc/inet.d.conf` 文件。找到类似下面这样的一行：

```
swat tcp nowait rout /usr/sbin/swat -port 901
```

如果你没有看到这样的一行，请添加它，然后保存文件。通过以下命令重启 `inet.d`：

```
/etc/inet.d/inet.d restart
```

- b. 对于 `xinet.d`，我使用 Fedora Core 作为示例。在 Fedora 下，打开终端并变为 root 用户。移动到目录 `/etc/xinet.d`。在目录中，你应该能找到一个名为 `swat` 的文件。用文本编辑器打开该文件。你应该看到类似下面的的内容：

```
service swat
{
    port = 901
    socket_type = stream
    wait = no
    only_from = 127.0.0.1
    user = root
    server = /usr/sbin/swat
    log_on_failure += USERID
    disable = yes
}
```

当显示 `disable = yes` 时，将 `yes` 改为 `no`。此外，注释掉（即在行首加井号）`only_from 127.0.0.1` 这一行。你完成后的文件应该像这样：

```
service swat
{
    port = 901
    socket_type = stream
    wait = no
    # only_from = 127.0.0.1
    user = root
    server = /usr/sbin/swat
    # log_on_failure += USERID
    disable = no
}
```

现在，通过输入 `/etc/rc.init.d/xinetd restart` 重启 `xinet.d` 服务器。你就可以使用 SWAT 了。

### 注意

如果你想限制对 SWAT 的访问，则不应注释掉 `only_from` 行。将该值设置为 `127.0.0.1` 允许从运行它的机器上使用它。或者，如果你允许从另一台机器访问，可以将该值更改为该机器的 IP 地址。

完成配置后，你就可以开始使用 SWAT 了。打开 Web 浏览器（见第 12 章）。

## 第18 章：文件共享解决方案 307

### 注意

如果你想限制对 SWAT 的访问，则不应注释掉 `only_from` 行。将该值设置为 `127.0.0.1` 允许从运行它的机器上使用它。或者，如果你允许从另一台机器访问，可以将该值更改为该机器的 IP 地址。

完成配置后，你就可以开始使用 SWAT 了。打开 Web 浏览器（见第 12 章）。
