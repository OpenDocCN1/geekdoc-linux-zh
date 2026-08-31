

# 如何在 Ubuntu 20.04 上配置 Cowpatty——Eldernode 博客

> 原文：<https://blog.eldernode.com/cowpatty-on-ubuntu-20-04/>

![How to configure Cowpatty on Ubuntu 20.04](img/519caf3bbe57cbb7f272b8b20fe85744.png)

一步步学习如何在 Ubuntu 20.04 上配置 Cowpatty。Cowpatty 由 Joshua Wright 编写，用于攻击者、网络管理员和黑客针对 Wi-Fi 系统进行离线攻击。Cowpatty 是针对使用基于 PSK 的认证的 WPA/WPA2 网络的离线字典攻击工具。

在这篇文章中，在介绍和解释 Cowpatty 及其工具之后，我们将学习如何在 [Ubuntu](https://blog.eldernode.com/tag/ubuntu/) 20.04 上配置 Cowpatty。你可以在 [Eldernode](https://eldernode.com/) 查看可用的软件包，并购买 [Ubuntu VPS](https://eldernode.com/ubuntu-vps/) 服务器。

## Cowpatty 中有哪些可用的工具？

Cowpatty 包中包含的工具包括：

- `-f 字典文件`：指定密码攻击中要使用的字典文件和目录位置。
- `-s 网络 SSID`：用于指定无线网络名称等服务标识。
- `-c`：检查四向握手是否有效，以及是否已破解。
- `-d Hash 文件`：可以减少无线系统的破解时间，也用于显示文件的位置和文件列表。
- `-r 数据包捕获文件`：指定捕获运行后存储所有数据包的文件。
- `-V 版本`：简单显示 Cowpatty 软件的版本信息。
- `-v Verbose`：以详细模式运行命令，并在终端窗口显示所有后台进程和信息。
- `-h 帮助`：打印帮助画面。

## 了解如何在 Ubuntu 20.04 上配置 Cowpatty

在这一节，我们将教你如何在 Ubuntu 20.04 上安装和配置 Cowpatty。为此，请打开终端并按照以下步骤操作。

### 在 Ubuntu 20.04 上逐步安装 Cowpatty

**1.** 在第一步中，输入以下命令：

```bash
:~# cd Desktop/
```

**2.** 然后，在第二步中，输入以下命令：

```bash
:~# sudo apt-get install libpcap-dev libssl-dev
```

**3.** 要下载 Cowpatty，请在下一步使用以下命令：

```bash
:~# wget http://www.willhackforsushi.com/code/cowpatty/4.6/cowpatty-4.6.tgz
```

**4.** 使用以下命令解压缩下载的 Cowpatty 文件：

```bash
:~# tar zxfv cowpatty-4.6.tgz
```

**5.** 在第五步中，输入以下命令：

```bash
:~# cd cowpatty-4.6
```

**6.** 在第六步中，输入以下命令：

```bash
:~# make cowpatty
```

**7.** 最后，通过输入以下命令开始安装 Cowpatty：

```bash
:~# sudo make install -d /usr/local/bin
```

Ubuntu 20.04 上的 Cowpatty 安装现已成功完成。你可以搜索并运行它。

## 结论

使用 Cowpatty 工具，你可以针对 WPA/WPA2 网络实施离线字典攻击，这些网络基于 WPA 个人身份验证。在本教程中，我们介绍了 Cowpatty 中可用的工具，并讲解了如何在 Ubuntu 20.04 上配置 Cowpatty。

