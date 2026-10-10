
More info and free tools at http://razor.bindview.com

Copyright (c) 2000 Bindview Development

```
```

== 你必须指定目标(s) 或类 C 进行发送

USAGE:

`./zz` `[-a 0-5]` `[-c class C]` `[-d dev]` `[-h]` `[-m host]` `[-s src]` `[-u udp]`

`[-v]` hosts

`-a` 要杀掉的 antididos 类型：

  0 类型 1-4 (默认)

  1 trinoo

  2 tfn

  3 stacheoldt

  4 Windows 版 trinoo

  5 shaft（需要使用 `-m` 选项）

`-c` x.x.x.0 格式的类 C

`-f` 发送数据包的时间（默认 1）

`-d` 从 dev 获取本地 IP（默认 eth0）

`-h` 此帮助屏幕

`-m` 被洪水的主机（用于上述 `-a 5`，仅限一个主机）

`-s` 伪造源地址（以防万一）

`-u` trinoo 的 UDP 排序端口（默认 53）

`-v` 详细模式（两次则更详细）

host(s) 是目标主机（如果使用 `-c` 则被忽略）

```

img/a7a9caa80ec85507179284d91e216f9f_131_0.png

# 系统扫描与探测 • 第3章 127

表 3.2 提供了了一些常用命令的简单概述。

## 表 3.2 常用 Zombie Zapper 命令

| 命令 | 定义 |
| - | - |
| `-a` | 允许你指定发送数据包的地址。 |
| `-c` | 在发送停止包时，你可以指定一个 C 类地址。 |
| `-s` | 允许你伪造地址。此选项和 `-u` 选项允许你在尝试尝试禁用远程网络上的僵尸网络时绕过防火墙规则。 |
| `-u` | 允许你更改发送停止包的默认 UDP 端口。 |
| 0-5 | 每个数字都能让 Zombie Zapper 模拟特定的 DDoS 客户端。例如，如果你认为发现了一个 tfn 客户端，你可以执行一个带有数字 2 的命令。 |

## 编译 Zombie Zapper 需要什么？

你需要安装 Zombie Zapper：

- 一个标准的 Linux 系统。
- Libnet：这组支持库允许你的系统生成用于网络的光数据包。你需要这些库，是因为 Zombie Zapper 的开发者在开发过程中使用了它们，如果你的系统中没有安装它们，程序将无法正常编译。这些库非常流行，经常被其他开发者使用。你可以在 www.canvasnet.com/libnet 下载 Libnet 库。

## 练习：使用 Zombie Zapper

- 1. 从随附的 CD 或通过 www.bindview.com 获取 Zombie Zapper 源码。一旦你使用 `tar -zxvf` 命令解压并解包文件，就可以准备进行编译了。获取 Zombie Zapper 请参考前述的 URL。
  在编译此代码之前，你必须先获取并安装 Libnet 库。随附的 CD 上提供了 Libnet 版本 (`libnet-0.10.8.tar.gz`)。一旦获取了 Libnet，使用 `tar -zxvf` 命令将其解压并解包。`./configure` 脚本会将 Libnet 安装到适合你系统的目录中。

- 2. 通过进入 Libnet.x.x 目录并使用 configure 脚本安装 Libnet：

```bash
./configure
```

- 3. 当 configure 脚本完成后，输入 `make`。

- 4. 输入 `make install`。

- 5. 虽然安装 Zombie Zapper 是可选的，但你现在可以通过输入 `make supp` 然后 `make util` 来安装补充和工具库。

- 6. 现在你已经安装了 Libnet，可以编译 Zombie Zapper 了。因为 Zombie Zapper 的代码依赖于此库，你必须告诉 GCC 编译器 Libnet 库的存在。执行以下命令：

```bash
gcc `libnet-config --defines` -o zz zz.c -lnetet
```

- 7. 该命令告诉 GCC 编译器使用 libnet-config 文件，该文件位于大多数 Linux 系统 `/usr/bin/` 目录下。你不需要编辑这个文件。当你输入此命令时，请确保你使用的是“反引号”字符，即键盘上 TAB 键上方的字符。不要使用单引号（'）。如果不使用反引号，GCC 将不会搜索 libnet-config，Libnet 会向你发送一条消息，告知需要在 libnet-config 脚本中定义某些值。忽略此消息，输入正确的字符。

- 8. 现在 zz 已经编译完成，你可以可以使用它了。执行以下命令：

```bash
./zz
```

- 9. 你将看到一个帮助菜单，告知你如何使用该程序。这确认你已正确编译了程序。

- 10. 现在，假设你注意到你的内部网络 192.168.5.0 上有几个主机正在发送 tfn 数据包。只要 tfn 服务器使用默认密码，以下命令将停止该服务器：

```bash
./zz -c 192.168.5.0
```

- 11. 恶意黑客在这个特定的 C 类子网上变成僵尸的服务器应该立即停止。你不能对 A 类或 B 类网络地址使用 `-c` 命令。要做到这一点，你必须指定 IP 地址以及你想要关闭的服务器的类型。例如，如果你怀疑位于 207.192.45.2 的服务器正在使用 stcheldht DDoS 服务器攻击你，你将执行以下命令：

```bash
./zz -a 3 207.192.45.2
```

- 12. 要了解更多关于你所发送的数据包的性质，可以使用 `-vv` 命令：

```bash
./zz -a 3 -vv 207.192.45.2
```

- 13. 如果你想伪造自己的地址，以便恶意用户无法知道是谁停用了他的僵尸网络，你将使用 `-s` 命令，后跟你选择的 IP 地址：

```bash
./zz -a 3 -vv 207.192.45.2
```
