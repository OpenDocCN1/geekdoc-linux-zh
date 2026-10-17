
```
$ sudo aptitude hold linux-image-* -y
```

## Ubuntu 服务器管理

下一次你使用 `sudo aptitude upgrade` 等命令升级软件包时，与当前 Linux 内核相关的软件包不会被升级。请小心；如果新的 Linux 内核包作为依赖被包含，则需要进一步的工作来识别那些同样不应该升级的软件包。

## 应用程序更新

了解何时更新应用程序可能会出现问题。与 Ubuntu 系统相关的多数软件包由第三方开发。虽然 Canonical 支持适当的软件包，但你仍然需要决定何时更新应用程序。某些应用程序更新可能会引入导致你所做工作失效的功能。

除了上述安全公告外，还可以找到其他信息。

## 镜像配置

同步本地镜像有两种基本方法。第一种是使用 `apt-mirror` 命令。第二种是使用 `rsync`。

`apt-mirror` 软件包很少被安装。你需要使用如下命令进行安装：

```
$ sudo apt-get install apt-mirror
```

因为 `unattended-upgrades` 软件包提供了安全处理过程的前端。它通过 `unattended-upgrades` 命令运行，并基于 `/etc/apt/apt.conf.d/50unattended-upgrades` 配置文件的设置。

```bash
$ sudo mkdir /apt-mirror/skel
$ sudo mkdir /apt-mirror/var
```

这些命令创建了上述目录，并赋予所有者写入权限。但为了让其生效，我还需要将所有这些目录（以及子目录）的所有者设置为 `apt-mirror` 用户和组。实现此点的方法是使用以下命令。`chown -R` 命令递归地更改 `/apt-mirror` 目录及其子目录的所有权：

```bash
sudo chown -R apt-mirror:apt-mirror /apt-mirror
```

现在参考 `/etc/apt-mirror/list` 配置文件。默认使用的是正在运行主机的架构。如果我在 64 位系统上创建镜像，以下设置建议默认从 64 位存储库复制内容：

```
set defaultarch <running architecture>
```

如果镜像是为与本地服务器架构不同的客户端准备的，我也必须指定该架构。例如，如果我要在 64 位服务器上为 32 位系统创建镜像，我将添加以下指令：

```
set defaultarch i386
```

这些指令包含一系列 URL，指定了需要镜像的存储库。应该更改这些 URL，仅列出需要镜像的存储库。例如，我通过仅包含以下 URL 并注释掉其他 URL 来限制镜像内容。`clean` 指令可以从关联存储库中释放过时包以释放空间。

```
deb http://us.archive.ubuntu.com/ubuntu hardy-updates main restricted
clean http://us.archive.ubuntu.com/ubuntu
```

我指定了适用于我的国家存储库，将配置文件中的 `archive.ubuntu.com` 实例替换为 `us.archive.ubuntu.com`。我还将复制范围限制在 `main` 和 `restricted` 存储库。我还可以向此指令中添加 `universe` 和 `multiverse` 存储库。你选择复制哪些存储库取决于可用的磁盘空间以及你下载数十 TB 数据的意愿。

我不考虑镜像与安全相关的存储库，因为安全更新基于最新的可用发布版本更为重要。

虽然 `http://us.archive.ubuntu.com/ubuntu` 存储库是最新的，但我可以使用镜像，例如 `http://mirrors.kernel.org/ubuntu`。决定取决于是复制镜像还是更更新但距离较远的存储库。这两者都有充分的理由，决定在很大程度上取决于所选镜像站点更新的频率。我选择从镜像复制，因此在 `/etc/apt/mirror.list` 中相应地进行了替换：

```
deb http://mirrors.kernel.org/ubuntu hardy-updates main restricted
clean http://mirrors.kernel.org/ubuntu
```

此文件中显示的任何其他 URL 都可以通过在前面添加注释字符（`#`）来禁用。如前所述，如果你更改了之前为 `/etc/apt/mirror.list` 配置文件定义的默认 `base_path`，则 `/usr/bin/apt-mirror` 脚本也需要更改。由于我将其更改为了 `/apt-mirror`，因此在 `/usr/bin/apt-mirror` 脚本中也进行了更改：

```bash
"base_path" => '/apt-mirror/',
```

# 镜像 Ubuntu 存储库

现在我已经设置了一个具有可用卷，至少对于那些要在本地镜像的存储库是如此。我已经修改了 `/etc/apt/mirror.list` 配置文件和 `/usr/bin/apt-mirror` 脚本，通过 `/apt-mirror` 目录为 i386 CPU 架构镜像 `main` 和 `restricted` 存储库。

我可以运行 `sudo apt-mirror` 命令，它会执行 `/usr/bin/apt-mirror` 脚本。与之前可能下载 40GB 文件相比，我配置中的 `apt-mirror` 命令仅下载了略多 1GB 的文件。如果 `/apt-mirror` 目录中有足够的可用空间，这就可以工作。

可用空间会有所不同。下载到系统的信息量取决于 `/etc/apt/mirror.list` 中选择的存储库以及这些存储库中的包。包和安全更新随时间推移而增加，请确保你为此目的保留的任何卷足够大。

进程完成后，检查 `/apt-mirror` 目录（或你选择的任何目录）的结构。由于我是从 `http://mirrors.kernel.org/ubuntu` 站点复制更新，配置好的 `apt-mirror` 命令会将选定的存储库部分复制到 `/apt-mirror/mirrors.kernel.org/ubuntu` 。

# 使用本地镜像

当然，除非你将本地系统指向上述镜像，否则这一切都无法运行。虽然可以设置其他协议，但对于本地存储库来说，最方便的协议是 HTTP。它是相同的默认 Web，并利用了基于 LAMP 的 Ubuntu Server 安装中预配置的 Apache Web 服务器。有关 Apache 和 LAMP (Linux, Apache, MySQL, PHP) 的更多信息，请参见第 15 章。

请注意，与 Apache Web 服务器关联的标准目录位于 `/var/www`，这与之前创建的 `/apt-mirror` 目录不同。我使用软链接通过 Apache 设置了访问，命令如下：

```bash
$ sudo ln -s /apt-mirror/mirror/mirrors.kernel.org/ /var/www/mirror
```

## Ubuntu 服务器管理

然后，我可以修改目标客户端上相应的 `/etc/apt/sources.list` 配置文件。根据已镜像的更新存储库，我将与远程存储库的连接替换为以下指令：

```
deb http://us.archive.ubuntu.com/ubuntu hardy-updates main restricted
```
