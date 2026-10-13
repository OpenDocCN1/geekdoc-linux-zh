
`mkinitrd(8)` 命令可以为你创建一个初始内存盘镜像。该镜像在内核首次启动时被加载。初始内存盘 (`initrd`) 通常用于在启动期间将关键块设备作为 SCSI 模块加载。这样就可以将所需的 SCSI 设备作为模块加载到内核。此命令会自动加载 `/etc/conf.modules` 中找到的所有 SCSI 设备以及其中指定的所有其他模块。

表 6-2 列出了了一些 `mkinitrd(8)` 选项。在命令行中，可以根据需要不限次数地多次使用 `preload` 和 `with`。你还需要在命令行中指定 `initrd` 镜像和内核版本号。一个简单的示例如下：

```
mkinitrd /boot/initrd 2.2.5
```

根据你的系统，你可能需要也可能不需要运行此命令。

## 324 第6章：高级用户管理

内核命名为 `mykernel-2.2.5`。现在我们需要编辑 `/etc/lilo.conf` 文件。我们希望在新内核启动失败时能够启动旧内核。以下是修改前的原始 `liloconf` 文件。

```
boot=/dev/hda
map=/boot/map
installs=/boot/boot.b
prompt
timeout=50
image=/boot/vmlinuz-2.2.5-15
label=linux
root=/dev/hda
read-only
```

从这些信息中可以看出，原始内核是 `vmlinuz-2.2.5-15`，它位于第一个分区上。LILO 位于第一块磁盘的 MBR 上。当启动的内核为 `linux` 时，我们需要添加另一个 `image` 部分来指向新内核。更改部分已**加粗**显示。

```
boot=/dev/hdc5
map=/boot/map
installs=/boot/boot.b
prompt
timeout=50
image=/boot/mykernel-2.2.5
label=linux
root=/dev/hdc5
read-only
image=/boot/vmlinuz-2.2.5-15
label=old
root=/dev/hdc5
read-only
```

保存此文件并运行 `lilo(8)`。输出应该如下所示：

- 添加了 `linux`

- 添加了 `old`

当你重启系统时，LILO 会等待你输入标签（`label`）。如果你什么都不输入，或者直接按回车键，Linux 就会加载。如果新内核无法工作，你只需要重启系统并在 LILO 提示符处输入旧标签即可。

这些步骤可以通过 `linuxconf` 完成。你可以添加一个已经复制到系统的新内核镜像，或者可以让 `linuxconf` 尝试检测你最近编译的内核。你需要进入 `Boot Mode | Lilo | A new kernel that you have compiled`。

如果你复制了一个内核，可以选择 `Boot Mode | Lilo | A new kernel` 选项，然后指定你想添加到 `lilo.conf` 文件中的新内核。

## mkbootdisk

`mkbootdisk` 是一个可以为你创建启动盘的实用程序。这基本上是一个救援盘。一旦创建，该磁盘就可以仅用于启动你的系统，或者你可以在 LILO 提示符处输入 `rescue`。使用此命令时唯一需要指定的选项是内核版本。表 6-3 列出了在使用此命令创建启动盘时可能有用的其他选项。

以下是 `mkbootdisk` 命令的示例：

```
mkbootdisk -dev/fd1 -verbose -noprompt 2.2.5
```

这将告诉 `mkbootdisk` 在第二个软盘驱动器上创建一个启动盘。它不会抑制输出，也不会提示插入磁盘。它将使用内核版本 `2.2.5`。

使用此磁盘时，你也可以在 LILO 提示符处输入 `rescue` 将该磁盘作为救援盘使用。

| `-device <file>` | 镜像存放的位置 |

| :--- | :--- |

| `-mkinitrdargs <args>` | 这可以将参数传递给 `mkinitrd` |

| `-noprompt` | 不会提示插入磁盘 |

| `-verbose` | 通常 `mkbootdisk` 没有输出：此将开启输出 |

## 326 第6章：高级用户管理

## 认证目标 6.04

## PAM

PAM 代表可插认证模块（Pluggable Authentication Modules）。在单用户环境或用户受信任的环境中，PAM 并不十分，但对于用户不受信任的多用户系统，它是完美的。PAM 允许在定义安全时具有更细粒度的控制。你可以使用并非编码进程序中的方法来控制资源的访问。例如，你可以让 `pppd` 使用 Novell 或 NT 用户数据库验证用户，而不是使用 Linux 提供的 `/etc/password` 或 `/etc/shadow` 文件。

要查看一个程序是否支持 PAM 认证，可以运行 `ldd <program>` 来打印它的共享库。然后查找两个条目：`libpam` 和 `libpam_mic`。

PAM 配置文件存储在 `/etc/pam.d/`。在旧版本中，它名为 `/etc/pam.conf`。以下是 `/etc/pam.d` 目录列表示例：

```
chfn gdm linuxconf other ppp rlogin shutdown xcreensaver
chsh halt linuxconf-pair passwd reboot rsh su xserver
ftp kde login poweroff rexec samba xdm
```

这些文件中的每一个都包含脚本文件，告诉 PAM 如何与不同的应用程序交互。这些脚本的语法如下：

`module-type control-flag module-path arguments`

每个部分的描述请参见表 6-4。

| `Service-name` | 程序名称 |

| :--- | :--- |

| `Module-type` | `Auth`, `account`, `session`, or `password` |

| `Control-flag` | `Required`, `requisite`, `sufficient`, and `optional` |

| `Module-path` | PAM 模块的路径 |

| `Arguments` | 模块的参数 |

配置 PAM 模块的旧方法是 `/etc/pam.conf` 文件。该文件的语法如下：

`service-name module-type control-flag module-path arguments`

如你所见，它几乎相同，不同在于你需要指定 `service-name`。这是因为只有一个文件包含了所有不同的服务。默认配置被称为 `OTHER`。你可以使用 `/etc/pam.d/` 目录下的规则。以下是一些示例：

```
# 示例 /etc/pam.d/other
auth required pam_unix.so
account required pam_unix.so
session required pam_unix.so

# 示例 /etc/pam.conf
auth required pam_unix.so
account required pam_unix.so
session required pam_unix.so
```

| 表 6-5 | 模块类型 | 账户 (`Account`) |

| :--- | :--- | :--- |

| 控制标志 (`Control Flag`) | 会话 (`Session`) |

| | | 密码 (`Password`) |

| 引用 | | 用户的 `pts` |

| 表 6-6 | | |

| :--- | :--- |

| `Required` | 用户必须认证 |

| `Requisite` | 用户必须认证 |

| `Sufficient` | PAM 将返回成功 |

| `Optional` | 此选项不决定成功 |

## 328 第6章：高级用户管理

| 表 6-7 | | |

| :--- | :--- |

| PAM 库引用 | `pam_radius` | 通过 RADIUS 服务器认证 |

| | `pam_rhost_auth` | 通过传统登录认证 |

| | `pam_rootok` | 允许无密码访问 `root` 权限 |

| | `pam_security` | 优先检查 `/etc/security` 文件 |

| | `pam_time` | 根据时间限制访问 |

| | `pam_warn` | 记录会话信息 |

| | `pam_wheel` | 如果用户是 `wheel` 组的成员则提供 `root` 权限 |

## 329 第6章：Cron 系统

## 认证目标 6.05

## Cron 系统
