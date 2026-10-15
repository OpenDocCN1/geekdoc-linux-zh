
# Linux 和虚拟服务器（VPS）上的 cPanel 和 WHM 安装教程

> 原文：<https://blog.eldernode.com/cpanel-and-whm-installation-tutorial/>

![cPanel and WHM installation tutorial on Linux and Virtual Server (VPS)](img/4a25ad99afe12a6427131541756138e5.png)

本教程介绍如何在 [Linux 服务器](https://eldernode.com/linux-vps/)和虚拟服务器（[VPS](https://eldernode.com/vps/)）上安装 cPanel 和 WHM。

cPanel 是世界上最受用户欢迎的主机控制面板之一，允许用户通过 GUI 界面而不是传统的命令行来管理服务器。这个面板是商用的，你需要定期付费才能使用。

## 硬件或系统要求

根据 cPanel 网站上提供的 CentOS 6 或 7 版本规格，最低处理器频率为 226 MHz。CentOS 6 建议配备 1 GB RAM，CentOS 7 建议配备 2 GB RAM，硬盘空间为 40 GB。

## 安装前需要考虑的事项

1. 安装前关闭操作系统防火墙，重新安装后再进行配置。
2. cPanel 在安装后不为用户提供卸载选项，您必须恢复服务器才能删除 cPanel。
3. 要安装 cPanel，您必须拥有 root 访问权限。
4. cPanel 是用 Perl 语言编程的。您需要确保您的服务器上安装了 Perl。

> 注意：要开始使用 PuTTY 软件，请通过 [SSH](https://eldernode.com/tag/install-ssh-server/) 登录到服务器。

## 安装 Perl

要安装 Perl，运行下面的命令：

```bash
yum -y install perl
```

## 设置主机名

现在，用下面的命令设置您的主机名。

您也可以使用此命令来更改您的主机名。

当然，在域名下面输入你想要的域名。

```text
主机名 web.eldernode.com
```

## 更新 CentOS

然后输入以下命令来更新 [CentOS](https://eldernode.com/tag/centos/)：

```bash
yum update
```

## 下载并安装 cPanel

使用下面的命令，我们将从主站点接收程序安装文件。

```bash
cd home
```

```bash
curl -o latest -L https://securedownloads.cpanel.net/latest
```

输入以下命令运行安装文件：

```bash
sh latest
```

根据您的服务器，这可能需要 4 个小时。当然，如果你有合适的服务器，大约需要 40 分钟。

## 进入 WHM 面板

要进入 WHM 面板，请在浏览器中输入以下地址。当然，输入你的服务器的 10 个 IP 号码。根据以下命令之一使用的协议来执行此操作：`2087` 用于 HTTPS 协议，`2086` 用于使用 HTTP。

```text
http://10.10.10.10:2086
https://10.10.10.10:2087
```

我希望你觉得 cPanel 和 WHM 安装教程有用。
