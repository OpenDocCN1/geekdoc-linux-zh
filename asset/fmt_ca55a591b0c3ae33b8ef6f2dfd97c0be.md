
```
root@server1 ~# date +s

1535823499

root@server1 ~#
```

默认情况下，系统从系统的 BIOS 获取当前时间。你可以使用 `hwclock` 命令在 BIOS 中查看或修改时间。`hwclock` 参数仅打印来自 BIOS 时间，但你也可以指定选项来修改 BIOS 时间。例如，`hwclock --set --date='2021-08-20 08:16:00'` 将将 BIOS 设置为 2021 年 8 月 20 日上午 8:16。

或者，你可以使用 Linux 时间来设置 BIOS。例如，命令 `date -s "20 AUG 2021 08:16:00" -w` 将将 Linux 时间设置为为 2021 年 8 月 20 日上午 8:16。然后你可以使用 `hwclock -w` 命令确保在启动时根据 Linux 时间校正 BIOS 时间。

> 你也可以使用网络时间协议（NTP）从网络（如互联网）获取时间。NTP 的配置将在第 13 章讨论。

时间信息取决于区域时区。例如，加拿大多伦多的上午 8:16 是法国巴黎的下午 2:16。时区信息存储在二进制文件 `/etc/localtime` 中，该文件包含了相对于纪元计算你时区的规则。该文件是 `/usr/share/zoneinfo/` 下正确文件的副本或符号链接，其中存储了所有时区文件，如下：

```
root@server1 ~# ls -l /etc/localtime

lrwxrwxr-x 1 root root 37 Jul 8 20:13 /etc/localtime -> ../usr/share/zoneinfo/America/Toronto

root@server1 ~#
```

要更改系统时区，你可以从 `/usr/share/zoneinfo/` 目录复制适当的时区信息到 `/etc/localtime`，或者修改 `/etc/localtime` 符号链接指向 `/usr/share/zoneinfo/` 目录下正确的时区信息文件。

除了 `/etc/localtime`，某些发行版还有 `/etc/timezone` 文本文件，其中包含指向 `/usr/timezone/` 下正确时区路径的引用，供某些应用程序使用，如下：

```
[root@server1 ~]# cat /etc/timezone

America/Toronto

root@server1 ~]#
```

你还可以通过修改 `TZ` 变量在当前 shell 中覆盖默认系统时间。例如，运行 `export TZ='America/Toronto'` 命令将确保你的 shell 中运行的任何命令都使用多伦多的时区显示时间。如果你不确定 `TZ` 变量中使用的是哪个时区（例如 `America/Toronto`），可以运行 `tzselect` 命令，它将提示你回答一系列问题以确定正确的时区。

### 格式本地化

除了时间本地化，不同地区可能有不同的数据表示格式。这主要包括语言，也包括该地区使用的习惯。例如，虽然北美通常以 `$4.50` 的格式表示货币（四美元五十十美分），但欧洲会表示为 `4,50`。亚洲通常以 `YYYYMMDD`（年、月、日）形式表示日期，而美国通常以 `MMDDYYYY`（月、日、年）形式表示日期。

不同的语言可能有不同的字符集，这些字符需要在软件中表示，并映射到键盘键上。20世纪60 年代早期计算机使用的美国信息交换标准（ASCII）字符集专门针对英语字符，没有国际本地化选项。随着 ISO-8859 标准的引入，它扩展到了包含一些其他语言，但仍然缺少这些语言使用的许多扩展字符。一种名为 Unicode 的新标准扩展了 ASCII，允许表示全球所有语言的字符，而 UTF-8 字符集允许软件使用一个到 4 个 8 位字节来表示 Unicode 定义的字符。

## 448 第 8 章 系统初始化、X 窗口与本地化

> 注意
> 你可以使用 `locale` 命令在不同的字符集之间转换数据。

此外，同一种语言在不同地区可能有略有不同的字符集、键盘布局和格式；例如，加拿大法语键盘与欧洲法语键盘不同，加拿大法语的日期和货币格式也与法语的日期和货币格式不同。因此，大多数系统上的格式本地化包含语言、区域和字符集，被称为 `locale`（区域设置）。例如，`en_US-UTF-8` 代表带有 UTF-8 字符集的美国区域英语。如果 `locale` 省了字符集，则假设使用 ASCII 字符集；例如，`en_US` 代表带有 ASCII 字符集的美国区域英语。许多 Linux 发行版不会将正确的 `locale` 传递给 Linux 内核，因为它是通过 GRUB2 引导程序使用内核命令行上的 `LANG` 选项加载的，该选项指示 Linux 在启动期间设置 `LANG` 变量以设定正确的区域设置。你也可以查看 `/proc/cmdline` 的内容，看看你的 Linux 是否带有 `LANG` 参数加载的：

```
[root@server1 ~]## cat /proc/cmdline

BOOT_IMAGE=vmlinuz-4.16.0-301..c28.x86_64 root=UUID=9ff25add-035b-4d26-9129-9a9d6a6fa3 ro resume=UUID=4837b-d96e-4edc-8d3d-556df0a17ca62 rhgb quiet LANG=en_US.UTF-8

[root@server1 ~]#
```

如果 `LANG` 不是由 Linux 内核在启动期间创建的，它是从文件中加载的；在 Ubuntu 系统上，`LANG` 变量从 `/etc/default/locale` 加载，在 Fedora 系统上，它从 `/etc/locale.conf` 加载，如下：

```
[root@server1 ~]# cat /etc/locale.conf

LANG=en_US.UTF-8

[root@server1 ~]#
```

你可以使用 `locale` 命令显示 `locale` 变量的值，如下所示：

```
[root@server1 ~]# locale

LANG=en_US.UTF-8

LC_CTYPE="en_US.UTF-8"

LC_NUMERIC="en_US.UTF-8"

LC_TIME="en_US.UTF-8"

LC_COLLATE="en_US.UTF-8"

LC_MONETARY="en_US.UTF-8"

LC_MESSAGES="en_US.UTF-8"

LC_PAPER="en_US.UTF-8"
```

## 第 8 章 系统初始化、X 窗口与本地化

```
LC_NAME="en_US.UTF-8"

LC_ADDRESS="en_US.UTF-8"

LC_TELEPHONE="en_US.UTF-8"

LC_MEASUREMENT="en_US.UTF-8"

LC_IDENTIFICATION="en_US.UTF-8"

LC_ALL=

[root@server1 ~]#
```
