
## rpm 命令中常用的选项

表 11-8

| 选项 | 描述 |
|---|---|
| -a, -all | 显示系统上安装的所有软件包名称（需与 -q 选项配合使用） |
| -c, -configfiles | 显示系统上已安装软件包的配置文件位置（需与 -q 选项配合使用） |
| --dump | 显示系统上已安装软件包的配置文件的详细信息（需跟在 -q 和 -c 选项之后使用） |
| -e, -erase | 从系统中删除指定软件包 |
| -F, -freshen | 仅当系统上存在旧版本时，才升级指定软件包 |
| -f, -file | 显示指定文件所属的软件包（需与 -q 选项配合使用） |
| -h, -hash | 在屏幕上打印哈希标记以指示安装进度（需与 -i 选项配合使用） |
| -i, -install | 安装指定软件包（前提是不使用 -q 选项） |
| -i, -info | 显示指定软件包的完整信息（需与 -q 选项配合使用） |
| -K, -list | 在文件名参数之前使用时，验证 RPM 文件内列出的校验和。列出指定软件包包含的文件名（需与 -q 选项配合使用） |
| --nodeps | 强制 RPM 在安装软件包前避免检查依赖项（需跟在 -i 选项之后使用） |
| -q, -query | 查询系统中的软件包信息 |
| --test | 仅执行测试安装（需与 -i 选项配合使用） |
| -U, -upgrade | 升级指定软件包；即使系统上不存在旧版本，该软件包也会被安装 |
| -V, -verify | 验证属于指定软件包的所有文件的位置 |
| -v | 在安装或处理软件包时打印详细信息 |

在 Fedora 20 安装过程中，文件会被添加到 /etc/yum/repos.d 目录中，该目录列出了包含 RPM 软件包的互联网标准软件仓库。因此，如果在安装 Fedora 时忘记选择某个特定的 RPM 软件包，您可以轻松地使用 yum install package_name 命令在之后安装它。

![](img/c27875544958897d817484d558c208c8_533_0.png)

您使用前面章节中介绍的 yum 命令，从互联网上的软件仓库中为您的 Fedora 20 虚拟机安装了几个不同的程序。

可以使用单个 yum 命令安装多个软件包。例如，yum install packagelname package2name package3name 命令将安装三个软件包，包括任何软件包依赖项。

由于软件仓库中经常添加更新版本的 RPM 软件包，您还可以使用 yum update packagename 命令将已安装的软件包升级到最新版本。例如，要将您的 BASH Shell 升级到最新版本，您可以使用以下命令，并在提示下载和安装最新软件包时按 y：

```bash
[root@server1 ~]# yum update bash
Loaded plugins: langpacks, refresh-packagekit
Resolving Dependencies
--> Running transaction check
---> Package bash.x86_64 0:4.2.45-4.fc20 will be updated
---> Package bash.x86_64 0:4.2.53-1.fc20 will be an update
--> Finished Dependency Resolution

Dependencies Resolved

Package   Arch   Version            Repository  Size
Updating:
bash      x86_64 4.2.53-1.fc20     updates     998 k

Transaction Summary
Upgrade  1 Package

Total download size: 998 k
Is this ok [y/d/N]: y

Downloading packages:
Delta RPMs reduced 998 k of updates to 453 k (54% saved)
bash-4.2.45-4.fc20_4.2.53-1.fc20.x86_64.drpm   | 453 kB  00:00
Finishing delta rebuilds of 1 package(s) (998 k)
Running transaction check  100% [========]  0.0 B/s | 998 kB  --:-- ETA
Running transaction test
Transaction test succeeded
Running transaction
   Updating   : bash-4.2.53-1.fc20.x86_64             1/2
   Cleanup    : bash-4.2.45-4.fc20.x86_64             2/2
   Verifying  : bash-4.2.53-1.fc20.x86_64             1/2
   Verifying  : bash-4.2.45-4.fc20.x86_64             2/2

Updated:
  bash.x86_64 0:4.2.53-1.fc20

Complete!
[root@server1 ~]# 
```

![](img/c27875544958897d817484d558c208c8_535_0.png)

> 如果没有软件包名称参数，`yum update` 命令将尝试更新所有已安装的软件包。您还可以使用 `yum check-update` 命令检查已安装的软件更新。

请注意，在上面的输出中，`yum` 命令未发现其他需要更新的 BASH 软件包依赖项。您还可能会发现，`yum` 命令在找到接受连接的软件仓库之前，会尝试几个包含必要软件（称为**软件镜像**）的不同软件仓库。这种情况很常见，因为软件仓库会限制其并发下载连接数量以允许快速下载。当软件仓库达到其并发连接限制时，它会向 `yum` 命令返回否定响应，然后 `yum` 命令会在 `yum` 配置文件中列出的下一个软件镜像上搜索该 RPM 软件包。

在某些情况下，您可能不知道在 `yum` 命令旁使用哪个确切的 RPM 软件包名称。幸运的是，您可以使用 `yum search` 关键字命令按关键字搜索软件仓库，或者使用 `yum list available` 命令列出可用的 RPM 软件包。`yum grouplist` 命令将显示软件包组名称列表。**软件包组**是一组相关的 RPM 软件包，它们通常一起安装以提供关键功能。例如，要在 Fedora 20 上安装开发工具（Development Tools）软件包组（其中包含 `make` 和 `gcc` 命令），您可以使用 `yum groupinstall` “Development Tools” 命令。

未在默认软件仓库上托管的 RPM 软件包仍可使用 `yum` 命令下载和安装。许多软件作者在其私有软件仓库上托管其 RPM 软件包，并在其网站上包含指导您将该私有软件仓库添加到 `yum` 配置文件（通常通过安装特殊的 RPM 软件包）并使用 `yum` 命令安装 RPM 软件包的说明。例如，如果您想在 Fedora 20 上安装 VideoLAN VLC 媒体播放器，您可以从 VideoLAN 网站（www.videolan.org）访问 Fedora 20 的说明。由于 VideoLAN VLC 媒体播放器托管在私有的 RPM Fusion 软件仓库上，VideoLAN 网站指导您运行以下命令以将 RPM Fusion 软件仓库的位置更新到 `yum` 配置文件：

```bash
[root@server1 ~]# rpm -ivh http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm
Retrieving http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm
warning : /var/tmp/rpm-tmp.cV8NoA: Header V3 RSA/SHA256 Signature, key ID 172fF33d: NOKEY
Preparing...                    ########################################### [ 100%]
Updating / installing...
 1:rpmfusion-free-release-19-1  ########################################### [100%]
[root@server1 ~]# 
```

接下来，您可以运行 `yum install vlc` 命令来安装 VLC 媒体播放器。

`yum` 命令也可用于查看和管理已安装的 RPM 软件包。`yum list installed` 命令将列出已安装的 RPM 软件包，而 `yum info` 软件包名称命令将显示已安装 RPM 软件包的详细信息。您还可以使用 `yum remove` 软件包名称命令来删除已安装的 RPM 软件包，或使用 yum groupremove 软件包组名称 命令来删除特定软件包组内的所有 RPM 软件包。

Fedora 20 上的 GNOME 和 KDE 桌面环境包含一个实用程序，该实用程序会定期检查系统中已安装软件的更新 RPM 软件包。如果您在通知窗口中选择“安装更新”选项，此实用程序将通知您任何较新的软件包，并使用 yum 命令自动下载并安装它们。您还可以运行图形化的**软件实用程序**（如图 11-5 所示）来手动检查软件更新、搜索并安装新的 RPM 软件包，或管理已安装的 RPM 软件包。要在 GNOME 桌面环境中启动软件实用程序，请导航至“活动”、“显示应用程序”、“软件”。

# 使用 Debian 软件包管理器 (DPM)

Debian 软件包管理器 (DPM) 默认用于基于 Debian Linux 发行版的 Linux 发行版，例如 Ubuntu Linux。与 RPM 软件包类似，DPM 软件包含为特定平台预编译的软件，并且可能存在软件包依赖项。但是，DPM 软件包使用 .deb 扩展名，并由 `dpkg` 命令安装和维护。例如，要从下载的 DPM 文件 `bluefish_2.2.6-1_amd64.deb` 在 Ubuntu Linux 系统上安装 bluefish 网页编辑器，可以使用 `dpkg -i bluefish_2.2.6-1_amd64.deb` 命令。表 11-9 显示了与 `dpkg` 命令一起使用的常用选项列表。

![](img/c27875544958897d817484d558c208c8_536_0.png)

图 11-5 软件实用程序

