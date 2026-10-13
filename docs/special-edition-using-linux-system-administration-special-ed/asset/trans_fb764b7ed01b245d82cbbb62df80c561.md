
WU-FTPD 包含一个名为 `xferstats` 的实用工具，用于分析和汇总存储在 `xferlog` 文件中的日志信息。xferstats 的输出包括以下信息：

-   传输的总字节数和日均字节数
-   每日统计
-   按每个服务器目录发送的文件和字节数的明细
-   每小时流量统计

`xferstats` 程序接受多个参数，包括 `-f filename` 用于指定 `xferlog` 文件的完整路径和文件名；`-r` 用于在统计中包含真实用户；`-a` 用于在统计中包含匿名用户；`-h` 用于生成每小时流量报告；`-d` 用于生成特定域名的流量报告；`-t` 用于按部分生成总流量报告。

以下是 `xferstats` 的示例输出：

```text
# xferstats -f /var/log/xferlog -r -a -h -t
TOTALS FOR SUMMARY PERIOD Sun Nov 7 1999 To Sat Nov 13 1999
Files Transmitted During Summary Period                  107
Bytes Transmitted During Summary Period                8217300
Systems Using Archiving                                  43

Average Files Transmitted Daily                          15
Average Bytes Transmitted Daily                      1173900
```

### 每日传输统计

| 日期 | 发送文件数 | 发送字节数 | 平均传输速率 | 发送文件百分比 | 发送字节百分比 |
|---:|---:|---:|---:|---:|---:|
| 1999年11月7日（星期日） | 29 | 2756399 | 2.2 KB/s | 27.10 | 33.54 |
| 1999年11月8日（星期一） | 11 | 161878 | 3.2 KB/s | 10.28 | 1.97 |
| 1999年11月9日（星期二） | 12 | 506230 | 2.9 KB/s | 11.21 | 6.16 |
| 1999年11月10日（星期三） | 10 | 602695 | 0.9 KB/s | 9.35 | 7.33 |
| 1999年11月11日（星期四） | 9 | 498994 | 1.2 KB/s | 8.41 | 6.07 |
| 1999年11月12日（星期五） | 19 | 1904576 | 0.6 KB/s | 17.76 | 23.18 |
| 1999年11月13日（星期六） | 17 | 1786625 | 1.7 KB/s | 15.89 | 21.74 |

### 每个存档部分的总传输量（按字节）

| 存档部分 | 发送文件数 | 发送字节数 | 发送文件百分比 | 发送字节百分比 |
|---:|---:|---:|---:|---:|
| /bahai/authors/bahaullah | 38 | 3072276 | 35.51 | 37.39 |
| /bahai/authors/other | 14 | 2269853 | 13.08 | 27.62 |
| /bahai/authors/abdulbaha | 9 | 1463654 | 8.41 | 17.81 |
| /bahai/authors/shoghi_eff | 9 | 897391 | 8.41 | 10.92 |
| /bahai/authors/bab | 2 | 211318 | 1.87 | 2.57 |
| /bahai | 32 | 159146 | 29.91 | 1.94 |
| /bahai/compilations/bahai | 1 | 55624 | 0.93 | 0.68 |
| /bahai/compilations/peace | 1 | 51099 | 0.93 | 0.62 |
| /bahai/compilations/schol | 1 | 36939 | 0.93 | 0.45 |

### 每小时传输统计

| 时间 | 发送文件数 | 发送字节数 | 平均传输速率 | 发送文件百分比 | 发送字节百分比 |
|---:|---:|---:|---:|---:|---:|
| 00 | 4 | 344770 | 3.2 KB/s | 3.74 | 4.20 |
| 01 | 30 | 2607905 | 2.1 KB/s | 28.04 | 31.74 |
| 02 | 5 | 422711 | 3.7 KB/s | 4.67 | 5.14 |
| 03 | 2 | 37908 | 0.7 KB/s | 1.87 | 0.46 |
| 04 | 1 | 3127 | 3.1 KB/s | 0.93 | 0.04 |
| 05 | 1 | 1826 | 1.8 KB/s | 0.93 | 0.02 |
| 06 | 13 | 721616 | 0.8 KB/s | 12.15 | 8.78 |
| 07 | 6 | 1121640 | 0.9 KB/s | 5.61 | 13.65 |
| 09 | 4 | 40445 | 0.5 KB/s | 3.74 | 0.49 |
| 10 | 1 | 4992 | 2.5 KB/s | 0.93 | 0.06 |
| 12 | 1 | 1826 | 1.8 KB/s | 0.93 | 0.02 |
| 13 | 3 | 89864 | 0.7 KB/s | 2.80 | 1.09 |
| 15 | 8 | 1353325 | 1.9 KB/s | 7.48 | 16.47 |
| 16 | 1 | 92 | 0.1 KB/s | 0.93 | 0.00 |
| 17 | 2 | 28298 | 4.0 KB/s | 1.87 | 0.34 |
| 18 | 5 | 116513 | 2.9 KB/s | 4.67 | 1.42 |
| 19 | 4 | 153783 | 4.0 KB/s | 3.74 | 1.87 |
| 20 | 4 | 399828 | 4.3 KB/s | 3.74 | 4.87 |
| 21 | 4 | 203706 | 0.1 KB/s | 3.74 | 2.48 |
| 22 | 2 | 226956 | 2.1 KB/s | 1.87 | 2.76 |
| 23 | 6 | 332629 | 2.3 KB/s | 5.61 | 4.09 |

除了 xferstats 之外，还有几个免费可用的第三方工具用于汇总 xferlog 文件的内容：

-   `dumpxfer` 处理 xferlog 文件并给出更易读的输出（可通过匿名 FTP 在 `ftp://tnt.microimages.com/tools/` 获取；需要 Perl）。
-   Koos van den Hout 编写了一个 Perl 脚本，用于处理 xferlog 文件、邮寄每日统计信息和上传文件，并创建下载次数最多的文件列表（可在 `ftp://ftp.cetis.nvu.nu/pub/koos/ftplogcheck` 获取）。
-   `iisstat` 可从 xferlog 文件和许多其他来源生成漂亮的传输图表（可从 `ftp://ftp.support.lotus.com/pub/utils/InternetServices/iisstat/iisstat.html` 获取）。
-   `Webalizer` 可从 `ftp.mrunix.net/pub/webalizer` 获取。它分析 WU-FTPD 格式的日志文件，并在 HTML 页面中创建报告，这些页面可以用 Web 浏览器查看。

## 故障排除

配置 WU-FTPD 服务器时经常遇到两个问题：

-   **ls 对真实用户有效，但对匿名用户不产生输出。** 要解决此问题，你需要在 FTP 用户主目录下的 `lib` 目录（本章示例中的 `/home/ftp/lib/`）中放置 `ls` 使用的动态库。你可以使用以下命令测试 `ls` 是否对 FTP 用户有效：

    ```sh
    # chroot ~ftp /bin/ls
    ```

    如果 `ls` 不工作，你可以使用 `ldd` 命令确定 `ls` 命令需要哪些库，并将这些文件复制到 `/home/ftp/lib/`：

    ```text
    # ldd /bin/ls
            libc.so.6 => /lib/libc.so.6 (0x40000000)
            /lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
    ```

    同样的原则也适用于 `/bin` 目录中的其他程序，例如 `compress` 和 `gzip`。如果 FTP 用户无法使用它们，请使用 `ldd` 检查所需的库是否存在。

-   **ls 工作正常，但不显示文件和目录的所有者和组名；显示的是 UID 和 GID 编号而不是名称。** 此问题有两个可能的原因。一个是 UID 和 GID 对应的用户和组名尚未添加到 `/home/ftp/etc/passwd` 和 `/home/ftp/etc/group` 中。另一个可能的原因是 `/home/ftp/lib/` 中缺少动态库。WU-FTPD 在 Linux 上需要 `libnsl.*` 和 `libnss_files.*` 库才能显示这些信息。

启动 ProFTPD 服务器时可能遇到两个常见问题：

-   首次安装 ProFTPD 后，当你尝试从 inetd 或作为独立守护进程启动它时，可能会看到错误“找不到组 nogroup。”这是因为默认的 `proftpd.conf` 文件要求使用用户 nobody 和组 nogroup 来运行守护进程。通常，Linux 系统在 `/etc/group` 中没有定义 nogroup 组。要修复此问题，你可以在 `/etc/group` 中定义 nogroup 组，或者修改 `proftpd.conf` 文件以改用 nobody 组。

-   以独立模式启动 ProFTPD 时，你可能会看到错误“无法绑定到端口/地址已在使用中。”当 `/etc/inetd.conf` 文件中存在 FTP 服务的行时，就会出现此问题。要解决此问题，请注释掉 `/etc/inetd.conf` 中以“ftp”开头的行，并向 inetd 发送挂断信号。或者，确保没有另一个 ProFTPD 副本或其他 FTP 守护进程已经在独立模式下运行。

## 附录

-   **A** Linux 命令参考
-   **B** Linux 硬件支持

## Linux 命令参考

以下是随 Red Hat Linux 6.2 一起发布的部分手册页的复制品。它们由各自的作者或版权所有者拥有版权，并且与 Linux 本身一样可以自由重新分发。

### AT

#### 名称

`at`、`batch`、`atq` 和 `atrm` 用于排队、检查或删除稍后执行的作业。

#### 概要

```text
at [-V] [-q queue] [-f file] [-mldbv] TIME
at -c job [job...]
atq [-V] [-q queue] [-v]
atrm [-V] job [job...]
batch [-V] [-q queue] [-f file] [-m] [-v] [TIME]
```

#### 描述

`at` 和 `batch` 在稍后执行，它们使用 `/bin/sh` 从标准输入或指定文件读取命令。

-   **at**——在指定时间执行命令。
-   **atq**——列出用户的待处理作业，除非用户是超级用户；在这种情况下，将列出所有人的作业。
-   **atrm**——删除作业。
-   **batch**——当系统负载水平允许时执行命令；换句话说，当平均负载降至 0.8 以下，或降至调用 `atrun` 时指定的值时。

`at` 允许相当复杂的时间规范，扩展了 POSIX.2 标准。它接受 HH:MM 形式的时间，以便在一天中的特定时间运行作业。（如果该时间已过，则假定为第二天。）你还可以指定午夜、正午或茶点时间（下午 4 点），并且可以让一天中的时间带有 AM 或 PM 后缀，以在早上或晚上运行。你还可以通过给出 month-name day 形式的日期（带有可选的

