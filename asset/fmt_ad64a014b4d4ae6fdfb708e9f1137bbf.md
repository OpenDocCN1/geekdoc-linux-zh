
你可以指定多行内容，如例所示：
`# dnf module install nodejs:10/development nodejs:10/s`

输出结果如下截图所示：
```
[root@localhost vagrant]# dnf module install nodejs:10/development nodejs:10/s
Last metadata check: 52:40 ago on Fri 16 Jun 2022 07:04:33 PM UTC.
Dependencies resolved.

| Package | Arch | Version | Repository | Size |
| --- | --- | --- | --- | --- |
| Installing group/packages: | | | | |
| nodejs | x86_64 | 11.24.0-1.el8.3.9671+15433c | ol8_appstream | 8.8 M |
| nodejs-dev | x86_64 | 11.24.0-module.el8.3.9671+15433c | ol8_appstream | 164 k |
| nodejs-nodemon | noarch | 1.3.0-module.el8.5141+52e2 | ol8_stream | 96 k |
| npm | x86_64 | 16.14.11-10.24.0.1.module.el8.3+9671+15433c | ol8_stream | 3.7 M |
| Installing dependencies: | | | | |
| annobin | x86_64 | 10.6.7-10.el8 | ol8_stream | 955 k |
| efi-srpm-macros | x86_64 | 3.0-1.el8 | ol8_stream | 22 k |
| gpg-srpm-macros | x86_64 | 1.4-2.el8 | ol8_stream | 9.5 k |
| perl-macros | x86_64 | 5.32-1.el8 | ol8_stream | 13 k |
| krbs5-dev | x86_64 | 18.1-14.0.1.el8 | ol8_latest | 560 k |
| libcc-devel | x86_64 | 14.5-6.4.el8 | ol8_latest | 38 k |
| libuuid | x86_64 | 2.10-20.1.el8 | ol8_latest | 179 k |
| liblinux-dev | x86_64 | 2.9-5.el8 | ol8_latest | 200 k |
| libspol-dev | x86_64 | 2.9-3.el8 | ol8_latest | 87 k |
| libverto-dev | x86_64 | 0.3-5.el8 | ol8_latest | 35 k |
| node-utils | x86_64 | 18.1-module.el8.3+5392+d60b51f | ol8_stream | 28 k |
| caml-srpm-macros | x86_64 | 5.4-2.el8 | ol8_stream | 9.3 k |
| openblas-srpm-macros | x86_64 | 2-2.el8 | ol8_stream | 7.9 k |
| open-devel | x86_64 | 1.11.14.6-5.el8 | ol8_stream | 31 k |
| prcre2-ut1 | x86_64 | 10.32-6.el8 | ol8_latest | 605 k |
| prcre2-ut2 | x86_64 | 10.32-6.el8 | ol8_latest | 229 k |
| prcre2-ut3 | x86_64 | 10.32-6.el8 | ol8_latest | 220 k |
| python-rpm-macros | x86_64 | 3.4-1.el8 | ol8_stream | 16 k |
| python-srpm-macros | x86_64 | 3.4-1.el8 | ol8_stream | 15 k |
| python3-rpm-macros | x86_64 | 3.4-1.el8 | ol8_stream | 15 k |
| qt5-devel | x86_64 | 5.15-1.el8 | ol8_stream | 11 k |
| redhat-rpm-config | x86_64 | 129.1-6.el8 | ol8_stream | 89 k |
| rust-srpm-macros | x86_64 | 5.0-2.el8 | ol8_stream | 9.2 k |
| unzip | x86_64 | 6.0-40.1.el8 | ol8_latest | 190 k |
| zip | x86_64 | 3.0-23.el8 | ol8_latest | 28 k |

Installing module profiles:
nodes/common
nodes/development
nodes/62

Enabling module streams:
nodes
10

Transaction Summary

32 Packages

Total download size: 20 M
Installed size: 60 M
Is this ok y/N]: _
```

Figure 10 – Output of `dnf module install nodejs:10/development nodejs:10/s`

或者如果你想安装所有配置，可以使用星号来选择：
`# dnf module install nodejs:10/*`

输出结果如下：
```
[root@localhost vagrant]# dnf install nodejs:*
```

## 使用 AppStreams 安装不同版本的软件

现在，我们将扩展对 AppStreams 的了解。我们不再从默认的模块流（`module stream`）安装应用程序，而是将指定一个不同的流。

## 如何操作...

有多种方法可以实现此点：只需指定安装不同的流即可完成任务，或者你可以手动启用不同的版本。我更倾向于在安装时指定版本，因为在这种情况下，AppStream 会自动启用该版本：

```bash
# dnf module install nodejs:16
```

## 注意

如果你已经安装了某个版本的 AppStream，最好在重置并安装不同版本之前删除旧版本。这将在稍后介绍。

输出如截图所示：
