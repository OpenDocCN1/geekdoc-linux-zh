
```
    log_on_success   ++ DURATION HOST

    log_on_failure   = HOST

    nice             = -2

    disable          = no

}
```

### 示例 4
此节仅适用于你想要通过 SSL 连接运行 POP3 服务器的情况。以下是支持 SSL 的 POP3 服务（pop3s）的示例 `/etc/xinetd.d/pop3s`：

- 创建 pop3s 文件（`vi /etc/xinetd.d/pop3s`）并添加以下行：

```
# default on:

# description: The POP3 service allows remote users to access their mail

# using an POP3 client with SSL support such as fetchmail.

pop3s

{
    socket_type      = stream
    wait             = no
    user             = root
    server           = /usr/bin/ipop3d
    only_from        = 0.0.0.0
    no_access        = 207.35.78.10
    instances        = 30
    log_on_success   ++ DURATION HOST
    log_on_failure   = HOST
    nice             = -2
    disable          = no
}
```

> 注意：不要忘记重启 Xinetd 以使更改生效。

- 要重启 Xinetd，请使用以下命令：
```
[root@deep]# /etc/init.d/xinetd restart
Stopping Xinetd: [OK]
Starting Xinetd: [OK]
```

## 加固 UW IMAP

本节探讨了我们可以采取的行动，以改进和加强 UW IMAP 的安全性。这里的要点在于，我们指的是已安装的基础程序中提供的可用功能，而不是任何额外的软件。

## 你真的需要 IMAP/POP 程序及其服务吗？

请注意，IMAP/POP 程序默认使用明文密码。任何在你的网络路径上运行嗅探器的人都可以获取用户名/密码，并使用它们以用户身份登录。不仅仅是因为你在 Linux 系统上使用了如 Netscape 这样的 IMAP/POP 邮件客户端（MUA）才需要在本地运行 UW IMAP 服务器。请检查你的配置，如果你使用远程/外部 IMAP/POP 服务器，请在系统上卸载 UW IMAP。

## 明文密码

- 如果你的网络路径上运行着嗅探器，它将捕获你的用户名和密码并使用它们以用户身份登录。不仅仅是因为你在 Linux 系统上使用了如 Netscape 这样的 IMAP/POP 邮件客户端（MUA）才需要在本地运行 UW IMAP 服务器。请检查你的配置，如果你使用远程/外部 IMAP/POP 服务器，请在系统上卸载 UW IMAP。

## 明文密码

- 如果你的网络路径上运行着嗅探器，它将捕获你的用户名和密码并使用它们以用户身份登录。不仅仅是因为你在 Linux 系统上使用了如 Netscape 这样的 IMAP/POP 邮件客户端（MUA）才需要在本地运行 UW IMAP 服务器。请检查你的配置，如果你使用远程/外部 IMAP/POP 服务器，请在系统上卸载 UW IMAP。

## 明文密码

- 如果你的网络路径上运行着嗅探器，它将捕获你的用户名和密码并使用它们以用户身份登录。不仅仅是因为你在 Linux 系统上使用了如 Netscape 这样的 IMAP/POP 邮件客户端（MUA）才需要在本地运行 UW IMAP 服务器。请检查你的配置，如果你使用远程/外部 IMAP/POP 服务器，请在系统上卸载 UW IMAP。

## 明文密码

- 如果你的网络路径上运行着嗅探器，它将捕获你的用户名和密码并使用它们以用户身份登录。不仅仅是因为你在 Linux 系统上使用了如 Netscape 这样的 IMAP/POP 邮件客户端（MUA）才需要在本地运行 UW IMAP 服务器。请检查你的配置，如果你使用远程/外部 IMAP/POP 服务器，请在系统上卸载 UW IMAP。

## 明文密码

- 如果你的网络路径上运行着嗅探器，它将捕获你的用户名和密码并使用它们以用户身份登录。不仅仅是因为你在 Linux 系统上使用了如 Netscape 这样的 IMAP/POP 邮件客户端（MUA）才需要在本地运行 UW IMAP 服务器。请检查你的配置，如果你使用远程/外部 IMAP/POP 服务器，请在系统上卸载 UW IMAP。

## 明文密码

- 如果你的网络路径上运行着嗅探器，它将捕获你的用户名和密码并使用它们以用户身份登录。不仅仅是因为你在 Linux 系统上使用了如 Netscape 这样的 IMAP/POP 邮件客户端（MUA）才需要在本地运行 UW IMAP 服务器。请检查你的配置，如果你使用远程/外部 IMAP/POP 服务器，请在上上卸载 UW IMAP。

## 明文密码

- 如果你的网络路径上运行着嗅探器，它将捕获你的用户名和密码并使用它们以用户身份登录。不仅仅是因为你在 Linux 系统上使用了如 Netscape 这样的 IMAP/POP 邮件客户端（MUA）才需要在本地运行 UW IMAP 服务器。请检查你的配置，如果你使用远程/外部 IMAP/POP 服务器，请在系统上卸载 UW IMAP。

## 明文密码

- 如果你的网络路径上运行着嗅探器，它将捕获你的用户名和密码并使用它们以用户身份登录。不仅仅是因为你在 Linux 系统上使用了如 Netscape 这样的 IMAP/POP 邮件客户端（MUA）才需要在本地运行 UW IMAP 服务器。请检查你的配置，如果你使用远程/外部 IMAP/POP 服务器，请在系统上卸载 UW IMAP。

## 明文密码

- 如果你的网络路径上运行着嗅探器，它将捕获你的用户名和密码并使用它们以用户身份登录。不仅仅是因为你在 Linux 系统上使用了如 Netscape 这样的 IMAP/POP 邮件客户端（MUA）才需要在本地运行 UW IMAP 服务器。请检查你的配置，如果你使用远程/外部 IMAP/POP 服务器，请在系统上卸载 UW IMAP。

## 明文密码

- 如果你的网络路径上运行着嗅探器，它将捕获你的用户名和密码并使用它们以用户身份登录。不仅仅是因为你在 Linux 系统上使用了如 Netscape 这样的 IMAP/POP 邮件客户端（MUA）才需要在本地运行 UW IMAP 服务器。请检查你的配置，如果你使用远程/外部 IMAP/POP 服务器，请在上上卸载 UW IMAP。

## 明文密码

- 如果你的网络路径上运行着嗅探器，它将捕获你的用户名和密码并使用它们以用户身份登录。不仅仅是因为你在 Linux 系统上使用了如 Netscape 这样的 IMAP/POP 邮件客户端（MUA）才需要在本地运行 UW IMAP 服务器。请检查你的配置，如果你使用远程/外部 IMAP/POP 服务器，请在上上卸载 UW IMAP。

# 第 3 步

创建自签名证书后，我们必须确保未来的 `imap.pem` 文件同时包含 RSA PRIVATE KEY（私钥）和 RSA CERTIFICATE（证书）部分。

- 要将 CERTIFICATE 部分包含到 RSA PRIVATE KEY 中，请使用命令：
`root@deep ssl$ cat tmp.pem >> privkey.pem`

上述命令会将名为 "`tmp.pem`" 的 CERTIFICATE 文件内容添加到名为 "`privkey.pem`" 的 RSA PRIVATE KEY 中。

# 第 4 步

接下来，我们必须将证书文件放在相应的目录中，并如果你使用 IMAP 则将其重命名为 "`imapd.pem`" ，如果使用 POP3 则重命名为 "`pop3d.pem`" ，以便 UW IMAP 服务器识别它。如果你将其重命名为 "`imapd.pem`" 或 "`pop3d.pem`" 以外的名称，请注意 UW IMAP 将无法识别它。在下面的示例中，我们将证书重命名为 "`imapd.pem`" ，因为我们要为邮件用户使用 IMAP。

- 要将文件放在相应的目录下，请使用以下命令：
`root@deep ssl$ mv privkey.pem certs/imapd.pem`
`root@deep ssl$ chmod 400 certs/imapd.pem`
`root@deep ssl$ rm -f tmp.pem`

首先，我们移动包含 RSA PRIVATE KEY 和 CERTIFICATE 部分的 privkey 文件到目录，并将其重命名为 `imapd.pem` 以供 UWAP 使用 IMAP 协议。然后，我们从系统中删除 `tmp.pem` 文件，因为它不再被需要了。

# 第 5 步

现在，在连接客户端通过 SSL 读取邮件之前，验证新的 `imapd.pem` 证书是否有效非常重要。请确保在进行测试之前，带有 imap 值的 USCPI-TCP 或 Xinet 守护进程已经运行。

- 要测试你新的 IMAP 证书，请使用以下命令：
`root@deep ssl$ openssl ssl_client -connect smtp.domain.com -port 993`
`CONNECTED(smtp.domain.com:993)`
`depth=0/C=CA/ST=Quebec/L=Montreal/O=Open Network Architecture/CN=smtp.domain.com/Email=noc@domain.com`
`verify error:18:signed certificate`
`verify return:1`
`depth=0/C=CA/ST=Quebec/L=Montreal/O=Open Network Architecture/CN=smtp.domain.com/Email=noc@domain.com`
`verify return:1`

证书链
0 :/C=CA/ST=Quebec/L=Montreal/O=Open Network Architecture/CN=smtp.domain.com/Email=noc@domain.com
1 :/C=CA/ST=Quebec/L=Montreal/O=Open Network Architecture
---

服务器证书
-----BEGIN CERTIFICATE-----
MI1DDTCA6gaWIBAgDAIBQkgIG9w0BAQFQADCBM1MAk1UEBhhMC0Ex
ZAnBgNVGBTab12WJ1ZYERa8GA1UEBXMITW9udHJHJ1WxxIjAgBgNVAgTOGUw

# UW IMAP 3
## 第 3 章

ZWq4tV0d23yyBcmNoaY3r1cmNoaY3r1JaBqNVAMFTXhbllZ5dtHR2jb25
ZWlnNrbTEMCGsQQsIS3DEJKARY90Qc99W5UY55b20whcNAMW1J2
MDQ1MDQ1WcmN3E3Z1TU0UBJ1DEL1MAKAUEBMC00CXEDZBnQVBAGTQ
B1F1Z2Y1BcmN3E8GA8U1W3E1Y3r1cmNoaY3r1JaBqNVAMFTXhbllZ5dtHR2jb25
yayBcmNoaY3r1JaBqNVAMFTXhbllZ5dtHR2jb25ZlNmVBTEd3
Mc0sC6g5S3DEJKARY90Qc99W5UY55b20whcNAMW1J2
MDQ1MDQ1WcmN3E3Z1TU0UBJ1DEL1MAKAUEBMC00CXEDZBnQVBAGTQ
0ttD3hnN331Ucm5f679355HJ0FP248kddoZSOJAC+TUE
fJ/hW9G6S1R0Ub111YYY7880QQQ4444YYY4fHTEBHNAGMAJ
fQfffQY0001111XVX6666666W0FFHHWWWWbb
gaFE33333333333333333333333333333333333333333333333333333333333333333
0A1MA601BUMV1YmREVDYQWvX7v80QQQ4444YYY4fHTEBHNAGMAJ
1B003333331111222YYYYYYYYYYY11111111111111111Y22222Y2YYYYYYYY555555555555

# Qpopper 3
## 第 4 章

在此过程中，如果出现任何升级，你所做的就是参考程序生成的已添加或更改的文件列表，并在安装新软件之前手动从系统中删除这些文件。与我们上方的示例相关，我们使用系统的 `/root` 目录来存储所有生成的列表文件。

## 编译 - 优化与安装 Qpopper

在将 Qpopper 软件安装到你的 Linux 系统之前，你必须执行以下步骤对软件进行配置、编译和优化。首先，我们以用户 `/root` 的身份安装程序，以避免权限问题。

### 第 1

一旦你从主软件网站获取了程序，必须将其拷贝到 `/var/tmp` 目录，并在解压之前切换到该位置：

- 可以可以通过命令完成：

```
[root@deep]# cp qpopper-version.tar.gz /var/tmp/
[root@deep]# cd /var/tmp/
[root@deep]# tar xpf qpopper-version.tar.gz
```

### 第 2

之后，进入新创建的 Qpopper 源码目录，并执行以下步骤为你的系统配置并优化软件。

- 使用以下命令进入新创建的 Qpopper 目录：

```
[root@deep]# cd qpopper-4.0.4/
```

- 使用以下编译行配置并优化 Qpopper：

```
CFLAGS="-O2 -march=i686 -funroll-loops"; export CFLAGS
./configure
--prefix=/usr \
--sysconfdir=/etc \
--localedestir=/var \
--mandir=/usr/share/man \
--enable-cache-dir=/var/spool/mail \
--enable-log-in \
--enable-secureauth \
--enable-shy \
--enable-standalone \
--enable-timing \
--enable-uw-kludge \
--enable-servermode \
--enable-fast-update \
--enable-emp-drop-dir=/var/spool/mail \
--disable-old-spool-loc \
--disable-status \
--with-openssl \
--with-pam
```

这告诉 Qpopper 为这种特定的配置环境进行设置：

- 指定缓存文件目录的位置。
- 记录成功的用户身份验证。
- 启用安全加密或影子密码。
- 隐藏 Qpopper 版本号。
- 创建一个独立的 POP3 守护进程而不是使用 Xinetd。
- 报告登录、初始化和清理的运行时间。
- 检查隐藏的 UW文件夹数据消息。
- 启用 SERVER_MODEL。
- 减少服务器模式更新期间的 I/O。
- 指定临时丢弃目录。
- 不要检查旧位置的旧邮件队列（spools）。
- 不要写入 'Status' 或 'X-UID' 头部信息。
- 使用 OpenSSL。
- 使用 PAM 认证。

### 第 3

现在，在安装软件之前，我们必须对系统上的所有现有文件创建一个列表，然后我们使用 `diff` 工具对它们进行比较，以找到文件放置的位置，最后安装 Qpopper：

```
[root@deep qpopper-4.0.4] # make
[root@deep qpopper-4.0.4] # cd
[root@deep root] # cd /var/tmp/qpopper-4.0.4/
[root@deep qpopper-4.0.4] # make install
[root@deep qpopper-4.0.4] # cd
[root@deep root] # find / > Qpopper1
[root@deep root] # diff Qpopper1 Qpopper2 > Qpopper-Installed
```

上述命令将配置服务器以确保你的系统拥有必要的库来成功编译包，将所有源文件编译为可执行二进制文件，然后将二进制文件和任何支持文件安装到适当的位置。

### 第 4

一旦完成 Qpopper 软件的配置、优化、编译和安装，我们可以通过删除程序存档和相关的源码目录来释放一些磁盘空间，因为它们不再需要了。

- 使用以下命令删除 Qpopper 及其相关的源码目录：

```
[root@deep /]# # cd /var/tmp/
[root@deep tmp]# # rm -rf qpopper-version/
[root@deep tmp]# # rm -f qpopper-version.tar.gz
```
