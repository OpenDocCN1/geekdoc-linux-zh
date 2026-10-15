
| external | 可变 | 用于开启了地址伪装的计算机，保护本地网络 |

| dmz | 可变 | 用于可公共访问但访问受限的计算机 |

| work | 可变 | 用于可信的工作区域 |

| home | 可变 | 用于可信的家庭网络连接 |

| internal | 可变 | 用于内部网络，限制入站连接 |

网络区域允许你为不同的环境维护不同的防火墙规则集。当你使用笔记本电脑连接到新网络时，NetworkManager 会提示你选择希望在特定环境中与防火墙配合使用的网络区域。如果你选择工作（`work`）网络区域，防火火墙默认将允许文件共享流量。或者，如果你选择公共（`public`）网络区域，防火火墙默认将阻止文件共享流量。

你系统上使用的默认网络区域定义在 `/etc/firewall/zones.conf` 文件中，自定义网络区域配置存储在 `/etc/firewall/zones` 目录中。你可以通过 `firewall-cmd` 命令管理网络区域以及按服务或端口允许或拒绝流量的防火墙规则。`firewall-cmd` 命令的一些选项列表 14-3 中。

## 表 14-3 常用 firewall-cmd 选项

| 选项 | 说明 |

| --- | --- |

| --get-zones | 显示所有可用的网络区域 |

| --get-services | 显示防火墙用于识别网络服务的名称列表 |

| --get-default-zone | 指定规则的源端口号 |

| --set-default-zone=zone | 指定规则的目的端口号 |

| --get-active-zones | 显示每个网络区域下活跃的网络接口 |

| --list-all-zones | 显示每个网络区域启用（允许）的服务 |

| --list-all | 显示当前网络区域启用（允许）的服务 |

| --zone=zone --list-all | 显示当前网络区域启用（允许）的服务 |

| --add-service=service | 启用（允许）指定的服务 |

| --add-service=permanent | 确保你执行的任何防火墙配置在启动时加载 |

| --add-port=port | 启用（允许）指定的端口 |

| --add-port=port --permanent | 确保你执行的任何防火墙配置在启动时加载 |

| --remove-service=service | 禁用（禁止）指定的服务 |

| --remove-service=service --permanent | 确保你执行的任何防火墙配置在启动时加载 |

| --query-service=service | 如果指定的服务在网络区域内启用（允许），则返回 yes，否则返回 no |

| --query-port=port | 如果指定的端口在网络区域内启用（允许），则返回 yes，否则返回 no |

要在你的（当前）网络区域中为 `postgresql` 定义一个状态检测防火墙例外，并确保其在启动时加载，你可以使用以下命令：

```
[root@server1 ~]# firewall-cmd --add-service=postgresql
success
[root@server1 ~]# firewall-cmd --permanent --add-service=postgresql
success
[root@server1 ~]#_
```

你也可以通过端口号定义状态检测防火墙例外。例如，要在你的（当前）网络区域中为 SSH（TCP 端口 22）定义防火墙例外，并确保其在启动时加载，你可以使用以下命令：

```
[root@server1 ~]# firewall-cmd --add-port=22/tcp
success
[root@server1 ~]# firewall-cmd --permanent --add-port=22/tcp
success
[root@server1 ~]#_
```

> 注意

在第13章的实验项目中，你使用了 `firewall-cmd` 命令按服务名允许到 Fedora Linux 虚拟机的流量。

许多 Linux 发行版还提供图形化防火墙工具，可以通过服务名或端口配置 netfilter。在 Fedora 28 中，防火墙工具会根据你的选择自动创建 netfilter 规则。这些规则会立即激活，因为配置对话框默认设置为 Runtime（运行时）；要设置启动时加载的规则，你必须在配置对话框中选择 Permanent（永久）。

## 配置 SELinux

Security Enhanced Linux (`SELinux`) 是一系列由国家安全局（NSA）创建的内核补丁和工具，它通过策略对你的系统实施安全保护，防止应用程序被以不安全的方式访问资源和系统组件。`SELinux` 为每个文件、目录和进程添加标签。预配置的 `SELinux` 策略包含了哪些进程标签允许访问某些文件和目录标签。当 `SELinux` 启用时，Linux 内核会强制 `SELinux` 策略中的规则，以防止进程访问存在安全风险的系统区域。

## 第 14 章 安全、故障排除与性能

回想第 3 章，在 `ls -1` 命令的输出中，文件或目录模式后紧跟的一个句号（ . ））表示该文件或目录具有 `SELinux` 标签。要查看文件和目录的 `SELinux` 标签，可以为 `ls` 命令添加 `-z` 选项。这在 Fedora 系统上 `index.html` Apache 根目录（`/var/www/html/`）的输出所示：

```
[root@server1 html]# pwd
/var/www/html
[root@server1 html]# ls -1
total 4
-rw-r--r--. 1 apache 46 Nov 16 17:32 index.html
[root@server1 html]# ls -Z
unconfined_u:object_r:httpd_sys_content:t0:s0 index.html
[root@server1 html]##
```

之前的输出表示 `index.html` 具有 `unconfined_u:object_r:httpd_sys_content:s0` 的 `SELinux` 标签。`SELinux` 标签由以下四个冒号（:）分隔的部分组成：

`user:type section:level`

`user`（用户）部分标识 Linux 用户类型，`role`（角色）部分标识用户在 `SELinux` 策略中所属的类别；对于用户生成的文件，这些将分别是 `unconfined_u`（无限制对象）和 `object_r`（对象访问）。

`type`（类型）部分是 `SELinux` 标签最重要的部分；它定义了文件或目录的分类。在 `SELinux` 规则下，只有包含相同分类的进程才允许访问该文件或目录。在之前的输出中，`index.html` 的分类为 `httpd_t`（Apache 系统内容）；因此，分类为 `httpd_t`（Apache 类型）的进程将允许访问 `index.html` 文件。要查看进程的 `SELinux` 标签，可以使用 `ps` 命令的 `-z` 选项。接下来的输出显示当前运行的进程包含 `httpd_t` 分类，结果它们能够访问先前的 `index.html`：

```
[root@server1 html]# ps -eZ | grep httpd
system_u:system_r:httpd_t:s0 1625 ? 00:00:00 httpd
system_u:system_r:httpd_t:s0 1626 ? 00:00:00 httpd
system_u:system_r:httpd_t:s0 1628 ? 00:00:00 httpd
system_u:system_r:httpd_t:s0 1630 ? 00:00:00 httpd
system_u:system_r:httpd_t:s0 00:00:00 httpd
[root@server1 html]##
```

## 第 14 章 安全、故障排除与性能 777

`level`（级别）部分是一个可选属性；只有当您将 `SELinux` 功能扩展到多级安全安全（MLS）或多类别安全（MCS）时，它才会被使用。MLS 可用于根据组织提供的额外属性（例如：机密、机密、公开）来限制对文件的访问，而 MCS 可用于限制类似策略之间的相互访问。

> 注意

你可以使用 `seinfo` 命令查看系统上 `SELinux` 标签部分可用的值。例如，`seinfo -u` 显示用户值，`seinfo -r` 显示角色值，`seinfo -t` 显示类型值。

要启用 `SELinux`，你可以编辑 `/etc/selinux/config` 文件并设置以下 `SELINUX` 选项之一：

- `SELINUX = enforcing`（由 `SELinux` 强制执行策略设置）

- `SELINUX = permissive`（`SELinux` 仅在记录日志事件时生成警告）

- `SELINUX = disabled`（禁用 `SELinux`）
