
`passwd` (driver = `passwd-file`) `addr = /etc/passwd-dovecot` `userdb` (driver = `static`) `mail_location = /home/$user/home=$` `mail_location = maildir:/Maildir/`

## 16 为测试启用身份验证

打开 Dovecot 配置文件：`/etc/dovecot/conf.d/10-master.conf`

滚动到以下部分：

```
service mail-login (# ...
inet_listener_maps = (
```

并将 `SSL` 身份验证切换以缩小可能连接的设置范围：

```
ssl =
```

保存并关闭文件。打开新文件作为：`/etc/dovecot/conf.d/10-auth.conf`

设置这些身份验证参数以允许：

```
disable_auth = no
auth_mechanisms = plain
```

事实是不安全的。由于你的配置是功能性的，请记住反转此操作并使用受信任权威机构的 `SSL` 加密！

## 17 使用密码文件设置身份验证

`GNU` `nano` `3.2.1` 文件: `.../dovecot/conf.d/a` 设置

```
### -d 如果没有域名，则连接到 user@domain
## 目录
## 家目录
```

```
doc <wiki/Variables.txt 获取完整列表，请参示例：
mail_location =home/user/Maildir/
mail_location =home/user/Maildir/var/index/mail/
## <doc/wiki/UserDatabase.txt>
```

```
## 用于系统用户的身份验证。包含自 auth.conf
## <doc/wiki/PasswordDatabase.txt>
## 如今对于大多数系统，PAM 是典型的。
## 你需要 /etc/passwd-dovecot 来使用 userdbd
## 身份验证才能生效。<doc/wiki/PasswordDatabase.txt>
```

```
## 如果你需要特殊权限来更改目录属性，
# 请按照此方法操作：
chown -R user:group /home/user/Maildir
chmod 700 /home/user/Maildir
```

## 18 创建密码数据库

为了简单起见，此文件将作为你的邮件用户数据库。在大多数简易实现中，“密码数据库”使用以下格式：

```
/etc/passwd
```

注意，密码应仅在初始配置期间使用，以缩小潜在问题。`SSL` 并不是永久解决方案：今天的 `Dovecot` 有多种身份验证方法。

## 19 调整用户权限

在对用户进行身份验证时，`Dovecot` 需要适当的访问权限。你可以这样调整它们（例如针对 `ec2-user`）：

```
chgrp -Rf /home/user/Maildir/
chown -Rf /home/user/Maildir/
chmod /home-user/Maildir/
```

## 20 重启 Postfix 和 Dovecot

```
service postfix restart
service dovecot restart
```

测试发送邮件：

```
echo "test email" | mail -s "test subject" user@example.com
```

# WebKit 教程

## 使用 WebKit 构建浏览器

`WebKit` 是一个开源 `Web` 引擎。`WebKit` 是 `Safari`、`Mail` 以及其他 `OS X` 项目使用的引擎的操作系统框架版本。`WebKit` 是 `HTML` 和 `JavaScript` 代码，是 `Chromium` 的分支，以及 `KDE` 的库。

### 01 获取源码

我们需要获取 `WebKit` 的源码。在终端中进入你想要存放源码的地方。

```
git clone https://github.com/webkit/webkit
```

该源码将占用 `4 GB` 空间，请确保你在等待时有足够的空间。

### 资源

`webkit.org`

`Ubuntu` `12.04` 或更高

![](img/dc2302183c6b3ebee0d18a3807d4d058_35_1.png)

### WebKit 网站

| 首页 |

| `Safari` 功能 |

| 行星 `WebKit` |

| 项目 |

| 联系我们 |

| 跟踪 |

| 贡献者会议 |

| 与代码工作 |

| 安装开发工具 |

| 代码 |

| 构建 `WebKit` |

| 运行 `WebKit` |

| 调试 `WebKit` |

| 提交与策略审查 |

| 添加功能 |

| 安全策略 |

| 文档 |

| `Wiki` |

| 项目 |

| 代码规范 |

| 开发者资源 |

| `Demo` |

| 测试 |

| 回归测试 |

### 参与

有很多方法可以参与。你可以：

- 下载最新的测试版本
- 安装开发工具并查看源码

一旦完成这些，你还可以：

- 报告软件 `Bug`
- 贡献代码
- 提交补丁进行审查

### 项目

有很多令人兴奋的（新）项目你可以参与：

- 帮助我们提高网站兼容性
- 编写文档
- `Swift`
- 数学
- `CSS`

## 安装 Qt 5

```
rob@ubuntu:~$ sudo wget http://download.qt.io/official_releases/qt/5/5.4.1/qt-opensource-linux-x86-5.4.1.run
-- 2015-05-11 10:00:56-- - http://download.qt.io/official_releases/qt/5/5.4.1/qt-opensource-linux-x86-5.4.1.run
-- [Connecting to download.qt.io...] 1
-- [Connecting to download.qt.io] 2
-- Resolving www.mirrorservice.org... 1
-- Resolving www.mirrorservice.org... done
-- Connecting to www.mirrorservice.org [IP ADDRESS]... 1
-- HTTP request GET, awaiting response... 200 OK
-- Received 209715200 bytes (200 MiB)
-- Saving to 'qt-opensource-linux-x86-5.4.1.run'
-- 2015-05-11 10:08:12 (2.79 MB/s) -- qt-opensource-linux-x86-5.4.1.run
```

`Qt` `5.4.1` 安装

欢迎使用 `Qt` `5.4.1` 安装向导。

![](img/dc2302183c6b3ebee0d18a3807d4d058_36_0.png)

一次创建，随处部署。

### 02 获取阶段分支 (staging branch)

此步是可选的，但你也可以专门查看 `Qt` 移植的阶段分支。要进行此操作，你需要检出创建的 `Qt` 仓库。运行以下命令之一：

> 如果你使用的是较新版本的 `Ubuntu`，可能会在 `Qt` 代码上遇到一些问题

```bash
$ git clone qtgithub https://github.com/qt/qt
cd qtgithub
$ git fetch qtgithub
```

然而，`Qt` 移植的当前发布版本在我们推荐的主分支 `Qt` 分支中。

请记住将此行的版本号更改为你下载的版本。一旦完成后，你可以使用以下命令进行安装：

- 构建基础包 (Build essentials)

如果你是从源码开始编译，你可能已经安装了编译器。如果没有，可以使用以下命令轻松安装：

```bash
/qt-opensource-linux-x86-5.4.1.run
```

### 03 获取 Qt 5 源码

我们需要正确构建 `Qt` `5`，以便我们按照自己的方式运行和开发 `Qt`。我们首先需要下载 `Qt` `5` 的文件，可以在 `www://qt.io/download-open-source` 找到它们。你也可以在终端中使用以下命令下载安装程序：

```bash
$ wget http://download.qt.io/official_releases/qt/5.4.1/qt-opensource-linux-x86-5.4.1.run
```

在下载之前，请考虑 `Qt` `5` 的最新版本。

### 04 安装 Qts

这将构建一个图形化安装程序 - 请按照说明安装 `Qt`。

## 设置 Open Qt

如果你正在使用已安装的库，你应该这样做。可以使用以下方法进行安装：

下载完成后，提升文件权限以执行它：
