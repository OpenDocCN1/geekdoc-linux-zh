
### 命令操作说明

| `install` | 安装指定的软件包及其所需的所有依赖项。也可以指定位于本地系统或 Web 服务器上的 `.rpm` 文件。通过以字符 `@` 为前缀，可以安装软件包组。 |
| `list` | 显示所有已安装的软件包以及系统中已启用的软件源中可用的软件包。 |
| `makecache` | 下载并缓存系统中已启用软件源的元数据。 |
| `provides` | 查找提供指定文件或目录的软件包。 |
| `reinstall` | 重新安装指定的软件包。 |
| `remove` | 删除指定的软件包。 |
| `search` | 搜索特定的软件包。 |
| `upgrade` | 将系统或指定的软件包升级到最新可用版本。 |

*表 4.19：命令 `dnf` 和 `yum` 的操作*

*表 4.20* 展示了部分常用的全局选项：

| **选项** | **说明** |
| :--- | :--- |
| `--downloadonly` | 仅下载软件包及依赖项，而不执行安装。 |
| `--show-duplicates` | 如果软件源为同一软件包提供多个版本，则列出所有版本。默认 `dnf/yum` 仅显示最新版本。 |
| `-v`, `--verbose` | 显示调试信息。 |
| `-y`, `--assumeyes` | 不询问用户是否确认操作。 |

*表 4.20：命令 `dnf` 和 `yum` 的常用全局选项*

### 使用 `dnf` 命令执行的任务示例

在以下图中，展示了使用 `dnf` 命令执行的不同任务：

- *图 4.30* 检查是否有可用的软件包更新：

![](img/863afa537de4eed7deb11978bfbfa90e_130_0.png)

*图 4.30：检查可更新软件包的输出示例。*

- 将 Linux 发行版升级到最新可用版本。

  - *图 4.31* 显示输出的第一部分是事务摘要信息：

![](img/863afa537de4eed7deb11978bfbfa90e_130_1.png)

- 确认操作后，输入 `y` 或使用选项 `-y/--assumeyes`，接下来显示的是软件包下载进度，如 *图 4.32* 所示：

```
Downloading Packages:
(1/2): libcurl-7.76.1-14.el9_0.4.x86_64.rpm                  86 kB/s  | 288 kB   00:03
(2/2): curl-7.76.1-14.el9_0.4.x86_64.rpm                      90 kB/s  | 300 kB   00:03
---------------------------------------------------------------------------------------------
Total                                                   176 kB/s  | 588 kB   00:03
Running transaction check
Transaction check succeeded.
```

> *图 4.32：命令 `dnf distro-sync` 示例输出的第二部分。*

- 输出的最后一部分是关于事务的信息，包括每个软件包的安装、清理和验证过程。这在 *图 4.33* 中进行了说明：

```
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                             1,
  Upgrading        : libcurl-7.76.1-14.el9_0.4.x86_64            1,
  Upgrading        : curl-7.76.1-14.el9_0.4.x86_64               2,
  cleanup          : curl-7.76.1-14.el9.x86_64                   3,
  cleanup          : libcurl-7.76.1-14.el9.x86_64                4,
  Running scriptlet: libcurl-7.76.1-14.el9.x86_64                4,
  Verifying        : curl-7.76.1-14.el9_0.4.x86_64               1,
  Verifying        : curl-7.76.1-14.el9.x86_64                   2,
  Verifying        : libcurl-7.76.1-14.el9_0.4.x86_64            3,
  Verifying        : libcurl-7.76.1-14.el9.x86_64                4,
Installed products updated.

Upgraded:
  curl-7.76.1-14.el9_0.4.x86_64        libcurl-7.76.1-14.el9_0.4.x86_64

Complete!
```

> *图 4.33：命令 `dnf distro-sync` 示例输出的最后部分。*

- 从软件仓库下载名为 `dmicodec` 的软件包到当前目录但不安装它，如 *图 4.34* 所示：

```
[root@rhel ~]# dnf download dmicodec
Updating Subscription Management repositories.
Last metadata expiration check: 23:27:22 ago on Sat 23 Jul 2022 09:27:36 PM CEST.
 dmicodec-3.3-7.el9.x86_64.rpm                                28 kB/s |  93 kB    00:03
[root@rhel ~]# ls -l dmicodec-3.3-7.el9.x86_64.rpm
-rw-r--r--. 1 root root 95279 Jul 24 20:55 dmicodec-3.3-7.el9.x86_64.rpm
```

> *图 4.34：下载软件包的输出示例。*

- 从软件仓库安装名为 `traceroute` 的软件包到系统中。这在 *图 4.35* 中进行了展示：

```
[root@rhel ~]# dnf install -y traceroute
Updating Subscription Management repositories.
Last metadata expiration check: 10:49:53 ago on Sat 23 Jul 2022 09:27:36 PM CEST.
Dependencies resolved.

 Package                  Arch       Version               Repository               Size

Installing:
 traceroute               x86_64     3:2.1.0-16.el9        rhel-9-for-x86_64-baseos-rpms 61 k

Transaction Summary
Install  1 Package

(omitted)
Installed:
 traceroute-3:2.1.0-16.el9.x86_64

Complete!
```

![](img/863afa537de4eed7deb11978bfbfa90e_132_0.png)

- 在软件仓库中搜索名为 `firefox` 的软件包，如 [图 4.36](figure-4.36) 所示。

```
[root@rhel ~]# dnf search firefox
Updating Subscription Management repositories.
Last metadata expiration check: 10:57:35 ago on Sat 23 Jul 2022 09:27:36 PM CEST.
============================================================================ Name & Summary Matched: firefox =============
firefox.x86_64 : Mozilla Firefox Web browser
```

![](img/863afa537de4eed7deb11978bfbfa90e_132_1.png)
