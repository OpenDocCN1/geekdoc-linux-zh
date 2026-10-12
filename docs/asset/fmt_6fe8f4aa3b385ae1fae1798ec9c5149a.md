
`Ksample.com+.005+05451.key` 包含公钥。此文件应该提供给其他 DNS 服务器，因为 DNS 内部没有方法允许你将此文件传输到其他系统，因此你应该使用其他技术，例如安全外壳（SSH）。

`Ksample.com+.005+05451.private` 文件包含私钥。它用于生成带数字签名的区域文件。

## dnssec-signzone 命令

实施 DNSSEC 时使用的区域文件不是标准区域文件。相反，使用的是使用 `dnssec-keygen` 命令生成的私钥生成的带数字签名的区域文件，且数字签名只能通过 `dnssec-keygen` 命令生成的公钥进行验证。

要创建此加密区域文件，首先创建一个纯文本区域文件，然后使用 `dnssec-signzone` 命令生成加密文件（注意：在你的发行版中，你可能需要使用 `-S` 选项进行智能签名）：

```
[root@localhost named]# dnssec-signzone -o sample.com.sample.com

K.com+.005+15117
```

结果是一个名为 `named.sample.com.signed` 的新文件，你应该将其作为该域名的区域文件。

## 第 22 章：保护 DNS 服务器

**注意：** 这一过程比比书中描述的更多。例如，你应该在 `/etc/named.conf` 文件中进行一些额外的设置（例如 `dnssec-enable` 设置）。本节的重点是 `dnssec-keygen` 和 `dnssec-signzone` 命令背后的概念。这些是你预计在考试中看到的内容。

对于考试，你已经知道 `dnssec-keygen` 生成公钥和私钥，`dnssec-signzone` 使用私钥对文件进行数字签名。

## 考试准备任务

### 复习所有关键主题

复习本章最重要的主题，并注出每个主题所在的页码。

**表 22-2 关键主题**
| 主题 | 页码 |
|---|---|
| Chroot 监狱 | 441 |
| 分布式 DNS 配置 | 443 |
| 事务签名 | 446 |
| `dnssec-keygen` 命令 | 447 |
| `dnssec-signzone` 命令 | 448 |

### 定义术语

定义本章中的以下术语并在词汇表中检查答案：

- 劫持攻击
- chroot 监狱
- 分布式 DNS
- 缓存投毒
- DNS 欺骗

### 复习题

这些问题的答案在附录 A。

1. 为了创建分布式 DNS，每个都 配置为 a。

2. 在位于 `/chroot/named` 目录的 chroot 监狱中，以下位置通常是设备文件？
- a. `/chroot/named/dev`
- b. `/chroot/named/etc`
- c. `/chroot/named/var`
- d. `/chroot/named/run`

3. 在位于 `/chroot/named` 目录的 chroot 监狱中，以下位置通常是 `named` 进程存储 PID？
- a. `/chroot/named/dev`
- b. `/chroot/named/etc`
- c. `/chroot/named/var`
- d. `/chroot/named/run`

4. 在分布式 DNS 配置中，外部 DNS 服务器充当。

5. 关于分布式 DNS 配置，哪些是正确的？（选择两个）
- a. 创建分布式 DNS 只有一种方法：使用两个 DNS 服务器。
- b. 分布式 DNS 配置根据查询的来源产生不同的 DNS 响应。
- c. 创建分布式 DNS 需要特殊的软件，因为 BIND 不允许分布式 DNS。
- d. 分布式 DNS 配置被认为比普通 DNS 配置更。

6. 以下在区域文件中被认为是注释字符？
- a. `;`
- b. `@`
- c. `~`
- d. `&`

7. 在 chroot 监狱中创建所有目录和文件后，你应该执行命令命令以确保所有文件和目录都属于用户和组。

8. 创建 chroot 监狱时，你需要通过执行命令命令在 `/chroot/named/dev` 目录下创建设备文件。

9. 以下哪个命令可以为 DNS 区域文件分配数字签名？
- a. `dnssec-keygen`
- b. `dnssec-signzone`
- c. `dnssec`
- d. `dnssec-zone`

10. 根据以下输出，`Ksample.com+.005+05451.key` 文件是由 `dnssec-keygen` 命令创建的密钥。

```
[root@localhost named]# ls K*

sample.com+.005+05451.key Ksample.com+.005+05451.private
```

本章涵盖了以下主题：

- Apache Web 服务器基础配置
- 为 Apache Web 服务器配置安全功能
- 实现虚拟主机

本章涵盖了以下目标：

- 208.1 实现 Web 服务器

## 第 23 章

### 实现 Web 服务器

`![](img/a76ac3bb017d749781a228f025853f37_487_0.png)` 是专注于 Web 服务器配置的三个章节中的第一个。在本章中，你将接触 Apache Web 服务器。你将学习如何对它的主配置文件和包含目录配置文件进行基本的配置更改。

你还将学习如何进行某些更改以使 Web 服务器更安全，包括如何限制对特定目录的访问。此外介绍了虚拟主机的概念，允许你配置 Apache Web 服务器从单台机器上“提供”多个网站。

### 我已经熟悉这些了吗？测试

“我已经熟悉这些了吗？”测试练习可以让你评估自己是应该阅读整个章节，还是直接跳到“考试准备任务”部分进行复习。如果你有疑问：

| 基础知识点章节 | 本节涵盖内容 |
|---|---|
| Apache Web 服务器配置 | 1, 2 |
| Apache Web 服务器安全 | 3, 4 |
| 虚拟主机 | 5 |

- 1. Apache Web 服务器的 `___` 指令用于指定存储服务器配置、错误和日志文件的目录树的顶端。
  - a. `root`
  - b. `ServerRoot`
  - c. `DocumentRoot`
  - d. `ApacheRoot`

- 2. 下列哪些是 Apache Web 服务器的默认日志文件？（选择两项）
  - a. `access_log`
  - b. `system_log`
  - c. `error_log`
  - d. `config_log`

- 3. 使用 `___` 指令告诉 Apache Web 服务器要响应的最大客户端数量。

- 4. 为 Apache Web 服务器创建密码文件，请使用 `___` 命令。

- 5. 使用单个 IP 地址提供多个虚拟主机的系统被称为
  - a. 虚拟主机 (`virtual host`)。

### 基础知识点

通常，当人们说他们在系统中安装了 Apache 时，他们指的是由 Apache 软件基金提供的 Web 服务器。该组织实际上提供了许多开源项目，但因为它最著名的是 Apache 超文本传输协议服务器，在软件术语中，“Apache”已成为这种 Web 服务器的同义词（我通常将其称为 Apache Web 服务器）。它也被称为 `httpd`，因为这通常是 Web 服务器进程的名称。

超文本传输协议（HTTP 或简单称为 hypertext）是一种自 20 世纪 90 年代以来网页标准的协议。该协议允许客户端程序（网络浏览器）从服务器程序（例如 `http` 进程）请求数据。这些数据由一种称为超文本标记语言（HTML）的标记语言进行格式化，然后被转换为人类可读的网页。

> **注意：** 对于考试，你应该理解 HTML 是什么，但不需要理解使用该语言的编码。

在开始配置 Apache Web 服务器之前，你首先需要查找主配置文件的位置。根据你的发行版，该文件应该位于以下目录之一：

- `/etc/apache`
- `/etc/apache2`
- `/etc/httpd`
- `/etc/httpd/conf`

例如，在我一直使用的 Ubuntu 14.X 系统中，配置文件位于 `/etc/apache2` 目录下，而 CentOS 7.x 系统位于 `/etc/httpd/conf` 目录下。尽管这可能令人沮丧，但好消息是，无论配置文件位于何处，文件内的语法应该是相同的。

> **注意：** 即使主配置文件的文件名也可以随发行版而变化。例如，在 CentOS 7.x 上文件名为 `httpd.conf`，在 Ubuntu 14.X 上文件名为 `apache2.conf`。

### Apache Web 服务器基础配置

默认的 Apache Web 服务器配置文件由注释和指令组成，指令是你可以赋予数值的参数。以下是 Apache 配置文件的部分示例：

```
# ServerRoot: The top of the directory tree under which the server's
# configuration, error, and log files are kept.
#
# 不要在目录路径末尾添加斜杠。如果你将
```
