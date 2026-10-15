
# 第四部分

## 安全

第 16 章

加密、完整性检查和签名：GNU Privacy Guard

第 17 章

增强安全型 Linux：SELinux

第 18 章

网协议安全：IPsec

第 19 章

安全 Shell 和 Kerberos

第 20 章

网络防火墙：Netfilter

此页故意留白

# 加密、完整性检查和签名：GNU Privacy Guard

加密、完整性检查和签名：GNU Privacy Guard

注意对于备份或复制大量文件，你会使用第 34 章介绍的 `rsync`。

有时，你可能需要在远程系统上执行单个命令。`rsh` 命令在另一个系统上执行 Linux 命令并将结果显示在你的本地屏幕上。当然，你的系统名称和登录名必须在远程系统的 `/.k5login` 文件中。对于启用 SSH 的网络连接，你可以使用 `ssh` 代替 `rsh`。`ssh` 命令接受两个通用参数：系统名称和 Linux 命令。语法如下：

```
$ rsh remote-system-name Linux-command
```

在下一个示例中，`rsh` 命令在远程系统 `violet` 上执行 `ls` 命令，列出 `/home/robert` 目录下的文件：

```
$ ssh violet ls /home/robert
```

除非加引号，否则特殊字符由本地系统评估。如果你对特殊字符加引号，它将成为远程系统上评估的 Linux 命令的一部分。对重定向运算符加引号允许你在远程系统上执行重定向操作。在下一个示例中，重定向运算符被加引号。`ls` 命令生成的文件名列表随后在远程系统被重定向到一个名为 `myfiles` 的文件，该文件也位于远程系统。

```
$ ssh violet ls /home/robert '>' myfiles
```

管道也是如此。第一个命令（见下文）在本地系统的打印机上打印文件列表。在第二个命令中，文件列表打印在远程系统的打印机上。管道被加引号并由远程系统评估，将标准输出管道到远程系统的打印机上。

```
$ ssh violet ls /home/robert | lpr
$ ssh violet ls /home/robert '|' lpr
```

注意 Kerberos 版本的远程命令允许你指定 Kerberos 领域和凭据。
