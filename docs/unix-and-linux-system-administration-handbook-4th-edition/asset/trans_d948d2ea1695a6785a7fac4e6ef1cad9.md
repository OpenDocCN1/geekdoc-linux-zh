

```
redhat$ sudo rpm -U openssh-2.9p2-12.i386.rpm
error: failed dependencies:
openssh = 2.9p2-7 is needed by openssh-askpass-2.9p2-7
openssh = 2.9p2-7 is needed by openssh-askpass-gnome-2.9p2-7
openssh = 2.9p2-7 is needed by openssh-clients-2.9p2-7
openssh = 2.9p2-7 is needed by openssh-server-2.9p2-7
```

哎呀！也许并没有那么简单。这里我们看到当前安装的 OpenSSH 版本 2.9p2-7 被许多其他包所依赖。**rpm** 不会让我们升级 OpenSSH，因为这种更改可能会影响这些其他包的运行。这种类型的冲突时常发生，这也是 APT 和 **yum** 等系统开发的主要动机之一。在现实生活中，我们不会尝试手动理清依赖关系，但为了本例的目的，让我们继续仅使用 **rpm**。

我们可以用 **--force** 选项强制升级，但这通常是个坏主意。依赖信息是为了帮你节省时间和麻烦，而不是仅仅阻碍你。没有什么是比远程系统上 SSH 损坏更能毁掉系统管理员早晨的了。

相反，我们也会抓取依赖包的更新版本。如果我们足够聪明，我们本可以在尝试升级之前就确定其他包依赖于 OpenSSH：

```
redhat$ rpm -q --whatrequires openssh
openssh-askpass-2.9p2-7
openssh-askpass-gnome-2.9p2-7
openssh-clients-2.9p2-7
openssh-server-2.9p2-7
```

假设我们已经获得了所有包的更新副本。我们可以一个一个安装，但 **rpm** 足够智能，可以一次处理所有包。如果你在命令行上列出多个 RPM，**rpm** 会在安装前按依赖关系对它们进行排序。

```
redhat$ sudo rpm -U openssh-*
```

酷！看起来成功了，确实如此：

```
redhat$ rpm -q openssh
openssh-2.9p2-12
```

请注意，即使我们没有指定包的完整名称或版本，**rpm** 也能理解我们说的是哪个包。

## dpkg: 在 Ubuntu 中管理 .deb 包

![](img/14d78e3cecac4581d37024baf1e94cca_431_0.png)

正如 RPM 包拥有全能的 rpm 命令一样，Debian 包拥有 dpkg 命令。实用的选项包括 **--install**、**--remove** 和 **-l** 来列出系统上已安装的包。**dpkg --install** 在安装包时，如果该包已存在于系统上，会先移除旧版本。

运行 dpkg -l | grep package 是确定特定包是否已安装的便捷方法。例如，要搜索 HTTP 服务器，可以尝试：

```
ubuntu$ dpkg -l | grep -i http
ii  lighttpd 1.4.13-9ubuntu4 A fast webserver with minimal memory footpri
```

此搜索找到了 lighttpd 软件，这是一款优秀的开源轻量级 Web 服务器。开头的 ii 表示该软件已安装。

假设 Ubuntu 安全团队最近发布了对 nvi 的修复以修补潜在的安全问题。在获取补丁后，我们运行 dpkg 来安装它。正如你所见，它比 rpm 聊得更多，并且会告诉我们它正在做什么：

```
ubuntu$ sudo dpkg --install ./nvi_1.79-16a.1_i386.deb
(Reading database ... 24368 files and directories currently installed.)
Preparing to replace nvi 1.79-14 (using ./nvi_1.79-16a.1_i386.deb) ...
Unpacking replacement nvi ....
Setting up nvi (1.79-16a.1) ...
Checking available versions of ex, updating links in /etc/alternatives ...
(You may modify the symlinks there yourself if desired - see 'man ln'.)
Leaving ex (/usr/bin/ex) pointing to /usr/bin/nvi.
Leaving ex.1.gz (/usr/share/man/man1/ex.1.gz) pointing to
/usr/share/man/man1/nvi.1.gz
...
```

我们现在可以使用 dpkg -l 来验证安装是否成功。-l 标志接受可选的前缀模式进行匹配，因此我们可以直接搜索 nvi：

```
ubuntu$ dpkg -l nvi
Desired=Unknown/Install/Remove/Purge
| Status=Not/Installed/Config-files/Unpacked/Failed-config/Half-installed
|/ Err?(none)/Hold/Reinst-required/X=both-problems (Status,Err: uppercase=bad)
||/ Name           Version        Description
+++-==============-==============-=============================================
ii  nvi            1.79-16a.1     4.4BSD re-implementation of vi.
```

我们的安装似乎进行得很顺利。

## 12.7 使用高级 Linux 包管理系统

诸如 APT、yum 和 Red Hat Network 之类的元包管理系统共享几个目标：

- 简化定位和下载包的任务
- 自动化更新或升级系统的过程
- 促进包间依赖关系的管理

显然，这些系统不仅仅是客户端命令。它们都要求发行版维护者以商定的方式组织其产品，以便客户端可以访问和理解软件。
