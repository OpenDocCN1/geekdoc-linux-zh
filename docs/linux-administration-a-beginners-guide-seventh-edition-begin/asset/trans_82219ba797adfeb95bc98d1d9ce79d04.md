

## 第 16 章 域名系统 (DNS)

### 从源码下载、编译并安装 BIND 软件

如果你的特定发行版没有提供预包格式的 ISC BIND 软件，你可以随时从 ISC 网站 (http://isc.org) 获取源码并进行编译。你可能还想利用该软件最新的修复程序，而你的发行版可能尚未实现这些修复。截至本文编写，该软件当前的稳定版本为 9.10.3，可以从以下地址下载：

http://ftp.isc.org/bind/9.10.3/bind-9.10.3.tar.gz

在尝试编译之前，请确保在基于 RPM 的发行版上已安装了 `openssl-dev` 包。在 Debian/Ubuntu 中，对应的包是 `libssl-dev`。该包确保你拥有必要的头文件，以支持 BIND 的某些高级功能。下载包后，如所示解压软件。例如，我们将其下载到了 `/usr/local/src/` 目录下。然后解压 tar 包：

```bash
tar xvzf bind-9.10.3.tar.gz
```

进入上一个命令创建的 `bind` 子目录。花一点时间研究可能存在的所有 README 文件。接下来，使用 `configure` 命令配置你的绑定。假设你想将 BIND 安装在 `/usr/local/named/` 目录下，请运行此命令：

```bash
./configure --prefix=/usr/local/named
```

执行以下命令以在指定的 prefix 路径下编译并安装 bind：

```bash
make; make install
```

我们从源码构建的 BIND 软件版本会将服务器守护进程 (`named`) 以及其他实用工具安装在 `/sbin/` 目录下。客户端程序（`dig`、`host`、`nsupdate` 等）安装在 `/bin/` 目录下。

### 安装了什么

许多程序都带有主包 `bind` 和 `bind-utils` 包，这些包在包管理器安装期间已经安装。我们关注以下工具：

- `/usr/local/named/named` DNS 服务器程序本身。
- `/usr/local/named/sbin/rndc` bind 命名服务器控制工具。
- `/usr/local/named/bin/host` 对命名服务器执行简单查询的程序。
- `/usr/local/named/bin/dig` 对命名服务器执行复杂查询的程序。

本章的剩余部分将讨论这里列出的某些程序/工具及其配置和用法。

### 理解 BIND 配置文件

`named.conf` 文件是 BIND 的主配置文件。根据该文件的规范，BIND 决定它应该如何运行以及必须读取哪些配置文件（如果有的话）。本节涵盖了设置通用 DNS 服务器所需要的内容。你可以在 BIND 的文档中找到关于新文件格式的完整指南。`named.conf` 文件的通用格式如下：

```bind
statement {
    // comments
}
```

`statement` 关键字告诉 BIND 我们正要描述其操作的一个特定方面，以及适用于该语句的选项。大括号 `{}` 是必须的，以便 BIND 知道哪些选项与哪些语句相关；每个选项后面以及闭合大括号后面都要紧跟一个分号 `;`。例如下：

```bind
options {
    directory "/var/named"; // 将配置文件存放在 /var/named
}
```

这意味着这是一个选项语句（option statement）。这里的特定选项是指定 BIND 工作目录的指令——即本地系统中存放命名服务器配置数据的目录。

### 细节

本节记录了你在典型的 `named.conf` 文件中会看到的许多注释。处理此问题的良方法是先快速浏览一遍，然后将其作为后续章节的参考。如果你在第一次阅读时发现某些指令看起来很奇怪或不合逻辑，请不要担心。一旦你稍后看到它们被使用，其原理和原因很快就会明朗了。

### 注释

注释可以是以下格式之一：

| 格式 | 表示 |
| :--- | :--- |
| // | C++ 风格注释 |
| /*...*/ | C 语言风格注释 |
| # | Perl 和 UNIX shell 风格注释 |

在第一种和最后一种样式（C++ 和 Perl/UNIX shell）中，一旦开始写注释，它将一直持续到行尾。在普通的 C 风格注释中，需要使用 `*/` 来表示注释的结束。这使得 C 风格的注释便于编写多行注释。不过，你可以选择任何你喜欢的注释格式并坚持使用。没有哪种风格是优于另一种的。

### 语句关键字

以下是一些最频繁使用的语句关键字：

| 关键字 | 描述 |
| :--- | :--- |
| acl | 访问控制列表——决定他人对你的 DNS 服务器拥有何种访问权限 |
| include | 允许你包含另一个文件，并将该文件视为 `named.conf` 文件的一部分 |
| logging | 指定记录哪些信息以及忽略哪些信息。对于记录的信息，你还可以指定日志记录的位置。 |
| options | 解决全局服务器配置问题。 |
| controls | 允许你控制供 `rndc` 工具使用的通道。 |
| server | 设置特定服务器配置选项。 |
| zone | 定义 DNS 区域。 |

我们将在接下来的章节中详细讨论四个最常用的关键字（`include`、`logging`、`server` 和 `zone`）。

**include 语句** 如果你发现你的配置文件开始变得臃肿，你可能想要考虑将文件拆分为更小的组件。每个文件都可以包含在 `named.conf` 文件中。请注意，你不能在语句内部使用 `include` 语句。

这是一个 `include` 语句的示例：

```bind
include "/path/to/filename_to_included";
```

> NOTE 所有 C 和 C++ 程序员们：尽管你的直觉告诉你想那样，请确保不要用井号 (#) 开始包含行！该符号用于在 `named.conf` 文件中开始注释。

**logging 语句** `logging` 语句用于指定你需要的信息及其位置。当此语句与 `syslog` 结合使用时，你将获得一个强大且可配置的日志系统。记录的项目是关于 named 状态的信息。默认情况下，它们记录在 `/var/log/messages` 文件中。简单来说地，各种类型的日志根据预定义的类别或通道分组；例如有安全日志类别、通用类别、解析器类别、查询类别等。

遗憾的是，此 `logging` 语句的可配置性是以复杂性为代价的，但默认设置对于大多数用户足够。这是一个简单的日志指令示例：

```bind
logging {
    category default { default_syslog };
    category queries { default_syslog };
};
```

> NOTE 列表中增加了行号以提高可读性。

**server 语句** `server` 语句告诉 BIND 关于它可能处理的其他命名服务器的特定信息。`server` 语句的格式如下：

```bind
server ip-address {
    bogus yes/no;
    keys { string; [string; ...] };
    transfer-format one-answer/many-answers;
    <other options>...
};
```

这里，第一行的 `ip-address` 是目标远程服务器的 IPv4 或 IPv6 地址。第 2 行的 `bogus` 选项在处理可能向你发送配置错误的站点时有用。第 3 行的 `keys` 子句指定由 `key` 语句定义的 `key_id`，用于加密与远程服务器通信的事务。该密钥用于生成请求签名，并附加在与远程命名服务器交换的消息中。第 4 行的 `transfer-format` 告诉 BIND 远程命名服务器是否可以在单次查询响应中接受多个答案。

