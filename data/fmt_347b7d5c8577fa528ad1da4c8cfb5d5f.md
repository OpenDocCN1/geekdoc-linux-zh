
# 内容发布指南

如果你应用了上述步骤，你的网站安全性方面已相当稳固。尽管如此，请务必监控日志活动以检测异常访问。同时记住，你网站的人员组件（如内容发布者和脚本开发者）也需要网站安全培训。为他们建立指南。

内容发布者和脚本开发者应该了解并遵循以下指南：

## 第 15 章：Web 服务器安全

例如，对于一个试图索引 HTML 页面的机器人来说，大量的位图图像存档是毫无用的。向机器人提供这些文件会浪费你的服务器资源以及机器人处的资源。

该协议是自愿的，随着机器人开发者获得 Web 机器人的经验，其礼仪仍在演变中。最流行的搜索引擎越来越遵守机器人排除协议。以下是机器人或爬虫程序的操作：

- 1. 当遵循规范的 Web 机器人访问名为 `www.domain.com` 的站点时，它首先检查 URL 是否存在：
- 2. 如果此 URL 存在，机器人将解析其内容以寻找索引网站的指令。作为 Web 服务器管理员，你可以创建符合你网站逻辑的指令。每个网站只能存在一个 `robots.txt` 文件；该文件包含可能如下的记录：

```
http://www.domain.com/robots.txt

User-agent: *

Disallow: /cgi-bin/

Disallow: /tmp/

Disallow: ~/kabir/
```

在上述代码中：
- 第一条指令告诉任何机器人都应该考虑随后的指令。
- 随后的三个指令（`Disallow`）告诉机器人不要访问指令中提到的目录。

![](img/177ab5b774eeb101e12de61f8616d71a_413_0.png)

对于每个想要排除的 URL 前缀，你都需要单独的 `Disallow` 行。例如，你的命令行不应该像这样：

```
Disallow: /cgi-bin/ /tmp/ ~/kabir/
```

记录中不应有空行。空行用于分隔多条记录。`User-agent` 和 `Disallow` 行不支持正则表达式。`User-agent` 字段中的星号是一个特殊值，意味着任何机器人。具体来说，你不能拥有下面任何一种行：

```
Disallow: /tmp/*

Disallow: *.gif
```

### 第四部分：网络服务安全

所有未显式禁止的内容都被认为机器人可以访问（下有若干示例）。
要排除整个服务器，请使用以下配置：

```
User-agent: *

Disallow: /
```

要允许所有机器人完全访问，请使用以下配置：

```
User-agent: *

Disallow: /
```

你可以通过删除 `robots.txt` 文件来实现相同的效果。要排除名为 `WebCrawler` 的单个机器人，添加这些行：

```
User-agent: WebCrawler

Disallow: /
```

要允许名为 `WebCrawler` 的单个机器人访问站点，请使用以下配置：

```
User-agent: WebCrawler

Disallow: *

User-agent: *

Disallow: /
```

要禁止机器人索引单个文件 `/daily/changes_to_often.html`，请使用以下配置：

```
User-agent: *

Disallow: /daily/changes_to_often.html
```

## 第15章：Web 服务器安全 395

- 6. 运行 `cd` 命令将当前目录切回到 `src`。
- 7. 带有你通常使用的命令行参数运行 `./configure` 命令。例如，要将 Apache 安装在 `/usr/local/apache`，你需要使用 `--prefix=/usr/local/apache` 选项运行此脚本。
- 8. 运行 `make` 和 `install` 来编译并安装 Apache。

这将编译并安装标准版 (http) 和启用 SSL (https) 的 Apache。你需要为 Apache 提供服务器证书。

### 为你的 Apache-SSL 服务器创建证书

有关为 Apache 服务器创建证书的详细信息，请参见第 11 页。为了快速上手创建一个临时证书，你可以只需执行以下操作：

- 1. 进入 Apache 源码目录的 `src` 子目录（例如，`/usr/src/redhat/SOURCES/apache_x.y.src`）。
- 2. 运行 `make certificate` 命令创建一个仅供测试的临时证书。`make certificate` 命令使用 `/usr/local/ssl/bin/openssl` 程序为你创建一个服务器证书。系统会询问你几个自言易懂的问题。以下是该会话的示例。
