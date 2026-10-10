
对每个软件包的描述都列出了通过使用软件仓库进行安装时默认可用的附加模块，但我们稍后在本教程的其他部分会详细讲解这一点。

```
root@debian:~# aptitude install nginx-full
The following NEW packages will be installed:
  nginx-common{a} nginx-full
0 packages upgraded, 2 newly installed, 0 to remove and 0 not upgraded.
Need to get 0 B/510 kB of archives. After unpacking 1,107 kB will be used.
Do you want to continue? [Y/n/?] Y
Selecting previously unselected package nginx-common.
(Reading database ... 66416 files and directories currently installed.)
Unpacking nginx-common (from .../nginx-common_1.2.1-2.2+wheezy1_all.deb) ...
Selecting previously unselected package nginx-full.
Unpacking nginx-full (from .../nginx-full_1.2.1-2.2+wheezy1_i386.deb) ...
Processing triggers for man-db ...
Setting up nginx-common (1.2.1-2.2+wheezy1) ...
Setting up nginx-full (1.2.1-2.2+wheezy1) ...
root@debian:~# 
```

图 1.2：在 Debian Wheezy 7.2 中使用软件仓库安装 nginx-full

此时，Nginx 已经安装完成，但尚未运行。我们将使用 `service nginx start` 启动服务，之后就可以在 Web 浏览器中看到其启动页面（见图 1.3）。

![](img/3adf2b91cc40e3d0012eab041f055ca8_8_0.png)

图 1.3：Nginx 启动页面

然后，以下命令将显示我们刚刚安装的 Nginx 版本（见图 1.4）：

```
root@debian:~# nginx -v
nginx version: nginx/1.2.1
root@debian:~#
```

![](img/3adf2b91cc40e3d0012eab041f055ca8_9_0.png)

图 1.4：从软件仓库安装的 Nginx v1.2.1

然而，截至今日，Nginx 的最新版本是 1.5.6，而版本 1.2.1 发布于 2012 年 6 月 5 日（[NGINX 下载页面](http://nginx.org/)）。这说明，如果我们想使用最新的、更新到当下的版本，就需要从源代码安装该程序。

## 1.3 在 Debian Wheezy 7.2 中从源代码安装 Nginx

请注意，以下说明代表在 Linux 中从头构建软件包的默认方式，因此请知悉，使用 `./configure`、`make` 和 `make install` 的常规安装流程会在以后使软件包卸载变得更加困难（如果您不想再使用它的话），因为系统没有方法来追踪在过程中添加/修改的所有文件。

简而言之，使用上述方法编译软件包应该有一个有效的理由（实际上是一个非常好的理由）。尽管如此，还是有一些有效的原因让您想要这样做。最常见的原因是在系统中安装某个软件包的较新版本；另一个原因是为了支持特定功能而进行编译。

如果您构建并安装 `.deb` 或 `.rpm` 文件，那么相应的软件包管理器（分别是 `aptitude` / `apt-get` 或 `yum`）将意识到该软件包的存在，并确保您不会覆盖之前安装的软件包的文件。另一方面，`make install` 命令会覆盖任何挡路的东西。我们将稍后讨论在确实有正当理由从源代码编译和安装软件包时我们拥有的其他选项。

现在，既然我们已经决定绝不接受低于最新版本的 Nginx，我们需要按照以下步骤从 http://nginx.org/download/ 下载压缩的 tarball 并在进行实际的构建之前将其解压。

- 下载 tarball：`wget http://nginx.org/download/nginx-1.5.6.tar.gz`
- 解压它：`tar xvfz nginx-1.5.6.tar.gz`
- 进入在上一步中自动创建的目录：`cd nginx-1.5.6`

然后：

- `./configure`（如果您想列出所有配置选项，请添加 `--help` 选项）。`./configure` 的输出显示了 Nginx 将安装的目录（`/usr/local/nginx`，见图 1.5）

![](img/3adf2b91cc40e3d0012eab041f055ca8_10_0.png)

图 1.5：Nginx 安装路径

- `make`
- `make install`

即使安装完成，Nginx 所在的目录也尚未被添加到 `PATH` 环境变量中（见图 1.6）

![](img/3adf2b91cc40e3d0012eab041f055ca8_10_1.png)

图 1.6：PATH 变量（安装前）

现在让我们将 `/usr/local/nginx/sbin` 目录添加到 `PATH` 变量中，并检查我们刚刚从源代码安装的 Nginx 版本（见图 1.7）。

![](img/3adf2b91cc40e3d0012eab041f055ca8_10_2.png)

图 1.7：PATH 变量（安装后）及从源代码安装的 Nginx v1.5.6

**注意：** 在配置过程中，系统可能会抱怨缺少库（见图 1.8）。在这种情况下，我们可以选择安装提供这些库的软件包（在我们的例子中，是 `libpcre3-dev` 和 `zlib1g-dev`），或者在配置期间忽略它们。

```
checking for PCRE library ... not found
checking for PCRE library in /usr/local/ ... not found
checking for PCRE library in /usr/include/pcre/ ... not found
checking for PCRE library in /usr/pkg/ ... not found
checking for PCRE library in /opt/local/ ... not found
.
./configure: error: the HTTP rewrite module requires the PCRE library.
You can either disable the module by using --without-http_rewrite_module
option, or install the PCRE library into the system, or build the PCRE library
statically from the source with nginx by using --with-pcre=<path> option.
root@debian:~/nginx-1.5.6#
```

![](img/3adf2b91cc40e3d0012eab041f055ca8_11_0.png)

## 1.4 在 Ubuntu 12.04 LTS 上安装 Nginx

虽然 Ubuntu 的最新版本是 13.10（*Saucy Salamander* 代号，发布于 2013 年 10 月 17 日），但我们选择在 Ubuntu 12.04 LTS（*Precise Pangolin* 代号）上进行安装，因为 Canonical 为其提供了直到 2017 年 4 月的延长支持。

我们将使用 `sudo aptitude update` 更新源，然后从发行版的在线软件仓库安装 `nginx-full`。在 Ubuntu 中必须添加 `sudo` 关键字，因为 root 账户默认是禁用的（见图 1.9）。除此之外，安装过程与我们刚刚在 Debian 上执行的过程不会有显著差异。从源代码安装也是如此。

```
gacanepa@ubuntuOS:~$ sudo aptitude install nginx-full
The following NEW packages will be installed:
  nginx-common{a} nginx-full
0 packages upgraded, 2 newly installed, 0 to remove and 72 not upgraded.
Need to get 400 kB of archives. After unpacking 1,101 kB will be used.
Do you want to continue? [Y/n/?]
```

![](img/3adf2b91cc40e3d0012eab041f055ca8_11_1.png)

然而，我们可以看到在这种情况下可用的版本甚至更加过时（见图 1.10）。

```
gacanepa@ubuntuOS:~$ nginx -v
nginx version: nginx/1.1.19
gacanepa@ubuntuOS:~$
```

![](img/3adf2b91cc40e3d0012eab041f055ca8_11_2.png)

和以前一样，在进行从源代码安装之前，我们将移除（卸载）所有与 nginx 相关的软件包（见图 1.11）。

![](img/3adf2b91cc40e3d0012eab041f055ca8_12_0.png)

图 1.11：截图

和以前一样，从源代码安装 Nginx 后，我们拥有了该软件包的最新且更新到当下的版本（见图 1.12）：

![](img/3adf2b91cc40e3d0012eab041f055ca8_12_1.png)

图 1.12：截图

然而，当涉及到启动 Nginx 时——正如我们在 Debian 中尝试启动时会发生的那样——我们很可能会得到一个 **nginx: unrecognized service**（Nginx：未识别的服务）错误消息（见图 1.13）。

![](img/3adf2b91cc40e3d0012eab041f055ca8_12_2.png)

图 1.13：截图

这是因为我们从源代码安装了该程序，因此启动脚本尚未就位。在这种情况下，我们可以通过使用完整路径从命令行运行主可执行文件（`/usr/local/nginx/sbin/nginx`）来启动 *nginx* 守护进程，或者编写一个脚本来处理这项工作——当然，最后一种选项代表了最佳选择，因为我们希望能够使用所有常规参数（`start, stop, restart, reload` 等）。此外，我们也可以直接使用随本教程提供的启动脚本之一（我们还可以对其进行修改以更好地满足我们的需求）。

一旦我们将脚本添加到 `/etc/init.d` 目录中（并将其命名为 `nginx`），我们需要将 `DAEMON` 变量更改为指向 `/usr/local/nginx/sbin/nginx`，并将安装目录（`/usr/local/nginx/sbin`）包含在 `PATH` 变量中（见图 1.14 和 1.15）：

![](img/3adf2b91cc40e3d0012eab041f055ca8_13_0.png)

![](img/3adf2b91cc40e3d0012eab041f055ca8_13_1.png)

然后我们可以按如下方式运行该脚本（见图 1.16）：

![](img/3adf2b91cc40e3d0012eab041f055ca8_13_2.png)

此外，我们需要确保 `nginx.conf` 文件“知道”在哪里找到 Nginx 的 PID。取消 `nginx.conf` 中以下行的注释（见图 1.18，很可能位于 `/usr/local/nginx/conf`），并将路径更改为启动脚本指示的路径（见图 1.17）：

