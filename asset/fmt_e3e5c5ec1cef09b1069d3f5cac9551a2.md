
```
sudo aptitude
```

当 Aptitude 启动时，您将看到屏幕上方有一个菜单栏，有两个面板。顶部面板包含软件包类别，如新软件包和未安装软件包。底部面板包含与软件包的信息。

使用 Aptitude 进行包管理非常直观，界面使得任务变得简单。以下是 Aptitude 中执行的常见包管理功能：

字体 安装软件包：要安装软件包，使用方向键导航到未安装软件包类别。

- 软件包：要升级软件包，使用方向键导航到已安装软件包。

- 删除软件包：要删除软件包，使用方向键导航到已安装软件包类别。Aptitude 是菜单驱动的界面。

在实际查看软件包时，顶部面板软件包列表中显示的第一列信息列出了包的当前状态，并使用以下键描述包的状态：

- `i`：已安装软件包
- `c`：软件包未安装，但包配置仍留在系统中
- `p`：已清除
- `v`：虚拟包
- `u`：文件已解压，但包未配置
- `C`：半配置 - 配置失败需要修复
- `H`：半安装 - 移除失败需要修复

要退出 Aptitude，只需按 `q` 并确认您想退出。通过按 `F10` 键可以在 Aptitude 菜单中使用许多其他功能。

### 命令行 Aptitude

你也可以将 Aptitude 作为命令行工具，类似于 `apt`。在 `apt` 示例中，要安装包含所有必要依赖的 `nmap` 软件包，你需要使用以下命令：

```
sudo aptitude install nmap
```

要移除同一个软件包，可以使用以下命令：

```
sudo aptitude remove nmap
```

请查看 `man` 页面以获取有关 Aptitude 命令行选项的更多详细信息。

### dpkg

`dpkg` 是基于 Debian 的系统的软件包管理器。它可以安装、删除、构建软件包，但与其他软件包管理系统不同，`apt` 和 `Aptitude` 是较新的，并且在 `dpkg` 之上叠加了额外的功能。本节介绍了如何使用 `dpkg` 管理本地安装的软件包：

- 要列出系统软件包数据库中的所有软件包（包括所有已安装和未安装的包），请在终端提示符中输入：

```
dpkg -l
```

- 根据系统上软件包的数量，这可能会产生大量输出。通过管道传递给 `grep` 来查看是否安装了特定软件包：

```
dpkg -l | grep apache2
```

将 `apache2` 替换为任何包名、包名的一部分或正则表达式。

- 要列出软件包（在本例中为 `ufw` 软件包）安装的文件，输入：

```
dpkg -L ufw
```

`ufw`

- 如果你不确定了哪个软件包，`dpkg -S` 可能会告诉你。例如：

```
dpkg -S /etc/host.conf
```

`base-files` : `/etc/host.conf`

输出显示 `/etc/host.conf` 属于 `base-files` 软件包。

> Note
>
> 在软件包安装过程中会自动生成许多文件，尽管它们在文件系统上，但 `dpkg -S` 可能不知道它们属于哪个软件包。

- 你可以通过输入以下命令来安装 `.deb` 文件：

```
sudo dpkg -i zip_3.0-4_amd64.deb
```

将 `zip_3.0-4_amd64.deb` 替换为你想要安装的 `.deb` 文件的实际文件名。

- 可以通过以下方式完成卸载软件包：

```
sudo dpkg -r zip
```

### 注意

在大多数情况下，不建议使用 `dpkg` 卸载软件包。最好使用能够处理依赖关系的软件包管理器，以确保系统处于一致状态。例如，使用 `dpkg -r zip` 将移除 `zip` 软件包，但任何依赖它的软件包将仍保持安装状态，并且可能不再正常运行。

要查看更多 `dpkg` 选项，请参主页：`dpkg`。

### APT 配置

高级软件包工具 `APT` 源仓库的配置存储在 `/etc/apt/sources.list` 文件和 `/etc/apt/sources.list` 目录中。此处引用了该文件的示例，以及有关从列表中添加或删除仓库的信息。

你可以编辑该文件来启用或禁用它们。例如，要禁用在每次进行软件包操作时插入 Ubuntu CD-ROM 的要求，只需注释掉文件顶部的 CD-ROM 对应行即可：

```
### no more prompting for CD-ROM please
### deb cdrom:[DISTRO-APT-CODENAME- Release i386 (20111013.1)]/DISTRO-SHORT-CODENAME main restricted
```

### 额外仓库

除了 Ubuntu 官方支持的仓库外，还存在额外的社区维护仓库，它们提供了更多可供安装的软件包。最流行的两个是 `universe` 和 `multiverse` 仓库。这些仓库不受 Ubuntu 官方支持，但由社区维护；它们通常提供对于你的 Ubuntu 计算机是安全的软件包。

#### Note

`multiverse` 或 `multiverse` 仓库中的软件包包含官方支持的软件包。特别是，某些可能阻止它们与免费操作系统一起发布，并且它们在你的本地可能是非法的。

### Warning

请注意，`universe` 或 `multiverse` 仓库包含官方支持的软件包。特别是，这些软件包可能没有安全更新。

还有许多其他源，甚至只提供一个软件包，例如单个应用程序开发者提供的软件包源。然而，在使用非标准软件包源时应始终保持警惕和谨慎。在执行安装之前，请仔细研究源和软件包，因为某些源和软件包可能会导致你的系统在某些方面不稳定或无法运行。

默认情况下，`universe` 和 `multiverse` 仓库是启用的，但如果你想禁用它们，请编辑 `/etc/apt/sources.list` 并注释以下行：

```
deb http://us.archive.ubuntu.com/ubuntu/ DISTRO-SHORT-CODENAME universe multiverse
deb-sec http://us.archive.ubuntu.com/ubuntu/ DISTRO-SHORT-CODENAME multiverse

deb http://us.archive.ubuntu.com/ubuntu/ DISTRO-SHORT-CODENAME-updates
universe

deb-src http://us.archive.ubuntu.com/ubuntu/ DISTRO-SHORT-CODENAME-updates

universe

deb http://us.archive.ubuntu.com/ubuntu/ DISTRO-SHORT-CODENAME multiverse

deb-src http://us.archive.ubuntu.com/ubuntu/ DISTRO-SHORT-CODENAME-multiverse

deb http://us.archive.ubuntu.com/ubuntu/ DISTRO-SHORT-CODENAME-updates

multiverse

deb-src http://us.archive.ubuntu.com/ubuntu/ DISTRO-SHORT-CODENAME-updates

multiverse

deb http://security.ubuntu.com/ubuntu/ DISTRO-SHORT-CODENAME-universe

deb-src http://security.ubuntu.com/ubuntu/ DISTRO-SHORT-CODENAME-updates

universe

deb http://security.ubuntu.com/ubuntu/ DISTRO-SHORT-CODENAME-multiverse

deb-src http://security.ubuntu.com/ubuntu/ DISTRO-SHORT-CODENAME-multiverse

deb http://security.ubuntu.com/ubuntu/ DISTRO-SHORT-CODENAME-updates

multiverse

deb-src http://security.ubuntu.com/ubuntu/ DISTRO-SHORT-CODENAME-updates

multiverse
```

## 自动更新

上述 `unattended-upgrades` 软件包可自动安装安全更新。首先，在终端中输入以下内容安装软件包：

```
sudo apt install unattended-upgrades
```

要配置 `unattended-upgrades`，请编辑 `/etc/apt.conf.d/50unattended-grades` 并调整以下内容：

```
Unattended-Upgrade :: Allowed-Origins {

${distro_codename}-security;

${distro_codename}-updates;

${distro_codename}-proposed;

${distro_codename}-backports;

${distro_codename}-focal;

};
```
