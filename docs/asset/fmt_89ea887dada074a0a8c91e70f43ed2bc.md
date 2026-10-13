
[root@server ~]# `useradd -G production production4`

`autofs` 服务监控网络共享。验证 `autofofs` 服务是否创建了 `/local/production` 目录，且其权限与 `servera` 相同。

- 在 `servera` 上，调整适当的 SELinux 布尔值（Boolean），以便 `production5` 用户在通过 SSH 密钥进行身份验证后可以使用 NFS 挂载的家目录。如果需要，使用 `redhat` 作为 `production5` 用户的密码。

- 在 `servera` 上，调整防火墙设置以拒绝所有来自服务器机器的连接请求。使用服务器的 IPv4 地址 (`172.25.250.10`) 配置防火墙规则。

- 在 `servera` 上，调查并修复失败的 Apache 网页服务问题，该服务监听端口 `30880/TCP`。适当调整防火墙设置，使端口 `30880/TCP` 能够对入站连接开放。

## 评估

作为工作站机器上的学生，使用 `lab` 命令为你的工作进行评分。纠正任何报告的失败并重新运行命令，直到成功。

```
[student@workstation ~$ lab grade rhca-preview3]
```

## 完成

在工作站机器上，切换到学生家目录并使用 `lab` 命令完成本次练习。此步骤对于确保之前练习的资源不会影响后续练习非常重要。

```
[student@workstation ~$ lab finish rhca-preview3]
```

本节结束。

# 第12章 | 综合复习

## 解决方案

## 配置和管理服务器安全

> 注意
> 如果你计划参加 RHCSA 考试，请使用以下方法来最大化本次综合复习的收益：尝试每个实验时，不要查看解决方案按钮或参考课程内容。使用评分指南在完成每个实验时记录你的进度。

在复习中，你将配置 SSH 密钥身份验证、更改防火墙设置、调整 SELinux 模块以及一个 SELinux 布尔值，并排排除 SELinux 问题。

- 预期结果
  * 配置 SSH 密钥身份验证。
  * 配置防火墙设置。
  * 调整 SELinux 模块和 SELinux 布尔值。
  * 排除 SELinux 问题。

## 准备工作

如果你在上一章结束时没有重置工作站和服务器机器，请保存你想要从之前的练习中保留的任何工作，并现在重置它们。

作为工作站机器下的学生，使用 `lab` 命令为本次练习准备系统。

此命令将准备你的环境并确保所有所需的资源都已可用。

```
[student@workstation~$ lab start rhcesa-preview2]
```

1. 在 `serverb` 上，为 `student` 用户生成一对 SSH 密钥。不要使用密码语保护私钥。

1.1. 以 `student` 用户身份登录服务器。

```
[student@workstation~$ ssh student@serverb
...输出省略...
```

1.2. 使用 `ssh-keygen` 命令生成一对 SSH 密钥。不要使用密码语保护私钥。

```
[student@serverb~$ ssh-keygen
Generating public/rsa key pair.
Enter file to save the key (/home/student/.ssh/id_rsa): Enter
```

创建了目录 '/home/student/.ssh/'.
Enter passphrase (empty for passphrase): Enter
Enter same passphrase again: Enter
Your identification has been saved in /home/student/.ssh/id_rsa.
Your public key has been saved in /home/student/.ssh/id_rsa.pub.
Your key fingerprint is:
SHA256:+J1qGGSQRBR0nCIHRwRU/QsvkYHHJqYvYEI@server.lab.example.com
The key's fingerprint image:

```
---[RSA 3072]-
|+BB+0+0..+|
|+.0000 0E+0 |
|. . . . 0 0 |
|     S |
|0.. |
|     0 0 |
|----[SHA256]-----
```
```

2. 配置用户接受通过在 `server` 上生成的 SSH 密钥登录。不要使用密码语保护私钥。

2.1. 以 `student` 用户身份登录 `server`。

```
[student@workstation~$ ssh student@serverb
...输出省略...
```

1.2. 使用 `ssh-keygen` 命令生成一对 SSH 密钥（注：此处此处为为 `student` 生成 SSH 密钥，根据上下文为在 `serverb` 上生成一对 SSH 密钥）。

```
[student@serverb~$ ssh-keygen
Generating public/rsa key pair.
Enter file to save the key (/home/student/.ssh/id_rsa): Enter
```

创建了目录 '/home/student/.ssh/'.

Enter passphrase (empty for passphrase): Enter

Enter same passphrase again: Enter

Your identification has been saved in /home/student/.ssh/id_rsa.

Your public key has been saved in /home/student/.ssh/id_rsa.pub.

Your key fingerprint is:

SHA256:+J1qGGSQRBR0nCIHRwRU/QsvkYHHJqYvYEI@server.lab.example.com

The key's fingerprint image:

```
---[RSA 3072]-
|+BB+0+0..+|
|+.0000 0E+0 |
|. . . . 0 0 |
|     S |
|0.. |
|     0 0 |
|----[SHA256]-----
```
```

2. 配置用户接受通过在 `server` 上生成的 SSH 密钥登录。不要使用密码语保护私钥。

2.1. 以 `student` 用户身份登录 `server`。

```
[student@workstation~$ ssh student@serverb
...输出省略...
```

2. 配置用户接受通过在 `server` 上生成的 SSH 密钥登录。不要使用密码语保护私钥。

2.1. 以 `student` 身份. `server`. `server1`.，为 `student` 用户生成一对 SSH 密钥。

1.2. 使用 `ssh-keygen` 命令生成一对 SSH 密钥。

```....keygen
keygen public/rsa...
. file to save the key.home/student/.ssh/id_rsa): Enter
```

创建了目录 '/home/student/.ssh/'.
Enter passphrase (empty for passphrase): Enter
Enter same passphrase again: Enter
Your identification has been saved in /home/student/.ssh/id_rsa.
Your public key has been saved in /home/student/.ssh/id_rsa.pub.
Your key fingerprint is:
SHA256:+J1qGGSQRBR0nCIHRwRU/QsvkYHHJqYvYEI@server.lab.example.com
The key's fingerprint image:

```
---[RSA 3072]-
|+BB+0+0..+|
|+.0000 0E+0 |
|. . . . 0 0 |
|     S |
|0.. |
|     0 0 |
|----[SHA256]-----
```
```

2. 配置用户接受通过在 `server` 上生成的 SSH 密钥登录。不要使用密码语保护私钥。

2.1. 以 `student` 用户身份登录 `server`.

```
[student@workstation~$ ssh student@serverb
...输出省略...
```

2. 配置用户接受通过在 `server` 上生成的 SSH 密钥登录。不要使用密码语保护私钥。

2.1. 以 `student` 身份. `server`. `server1`.，为 `student` 用户生成一对 SSH 密钥。
