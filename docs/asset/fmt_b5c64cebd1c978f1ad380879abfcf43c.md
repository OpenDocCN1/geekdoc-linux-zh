
它不会替换你标准系统上的音乐播放器（它没有挂钩到全局音乐控制）。然而，如果你正在进行任何需要稍微了解其工作原理的开发或音乐创作，观察它播放和清理媒体的方式是非常有趣的。

![](img/f16f9d3399c2c447b8fa7812e3edd8d8_31_0.png)

*（注：由于提供的原文后半部分存在大量重复和乱码，以上翻译仅针对前半部分有效内容进行。）*

# `CampaignChain` 教程

## 规划你的社交媒体营销

`CampaignChain` 是一款开源的社交媒体营销工具，它让每一个活动都变得简单。

![](img/f16f9d3399c2c447b8fa7812e3edd8d8_33_0.png)

社交媒体是当今营销最重要的方面之一。如果没有社交媒体发挥巨大作用，机构就无法制定任何策略。但是，跨不同平台管理活动是一项巨大的挑战。要衡量影响——除非你有针对小企业和管理社交媒体活动的经理的相关数据，否则无法说一个活动运行良好。对于专业的社交媒体经理来说，这项工作已变得复杂得多。

## 01 前提条件

在我们开始使用 `CampaignChain` 之前，让我们来看看安装所需的各种前提条件。首先是 Ubuntu 12.04 上的 MySQL，默认安装了 MySQL 5.5，但如果你的系统中没有安装 MySQL，

Nitish Tiwari 职业是一名软件开发人员，内心热衷于开源。除了为业务需求编写软件外，他还帮助杂志管理他们的在线活动。

```
sudo apt-get install mysql-server-5.5
```

在本文中，我们将展示如何使用 `CampaignChain`，这是一个开源的社交媒体营销工具，可以帮助你创建、计划、执行和监控你的社交媒体平台。它适用于任何人，也适用于经营小企业并需要社交媒体工具的人员。对于本教程，我们使用了 Ubuntu 12.04 上 `CampaignChain` 的稳定版本。你还需要 Java（1.5 或更高版本）和 PHP（5.4 或更高版本）。让我们开始安装。

要检查是否安装了 MySQL，输入 `mysql --root -p`。如果出现密码提示，说明已安装。如果没有 MySQL，则说明未安装。一旦进入 MySQL 提示符，输入 `create database campaignchain_oc;`。现在我们已经有了 `CampaignChain` 准备数据库。下一步是安装 Java（如果你还没有的话）。如果你已经安装了 Java，输入 `java -version`。如果收到找不到 Java 的消息，你需要安装 Java，可以通过以下操作完成：

# 资源

- `CampaignChain`: campaignchain.com
- 文档: bit.ly/IoEnbz

```
sudo apt-get install default-jre
```

| 计划中的活动 | |
| --- | --- |
| 时间轴 | 日历 |
| 时间 | 今天 |
| `CampaignChain` | 事件 | 成员 | 任务 |
| 活动 5 | 活动 4 | 测试活动 | 活动 2 | 活动 1 |

`CampaignChain` 有一个规划窗口，可以在时间轴上显示所有活动。

## 注册系统模块安装向导

- 1. 第一步
- 2. 第二步
- 3. 第三步
- 4. 第四步
- 5. 第五步

请注意，这可能需要一或两分钟。

下一步

使用 `java --version` 交叉检查安装情况：如果你没有安装任何版本的 JAVA，请使用 `php -v` 检查你机器上的 PHP 版本。如果你没有安装 PHP 或版本低于 5.4，你需要使用 `sudo apt-get install php-f` 安装 PHP。`CampaignChain` 同样需要它。即使你已经安装了 PHP，可能需要重启它。

## 02 安装

下一步是安装 Composer。Composer 是 PHP 和 `CampaignChain` 的依赖管理工具。它用于安装其所需的包和模块。要安装 Composer，你可以切换到 root 用户，在命令提示符中输入 `sudo` 并输入密码。一旦成为 root 身份，输入 `curl -sS https://getcomposer.org/installer | php`。安装 Composer 之前必须已经安装了 PHP。运行 `sudo apt-get install php` 然后运行 `npm install`。完成这些步骤后，你现在可以下载 `CampaignChain` 基础系统了。

```bash
composer create-project --dev campaignchain/campaignchain-campaignchain dev-master
```

在命令提示符中，从 `CampaignChain` 的 GitHub 仓库下载最新版本到路径 `campaignchain/campaignchain`。它将提示你安装参数，这些参数将用于所有模块，包括 MySQL 数据库名称、需要在数据库中填充的字段、`_user` 和 `database_password` 字段。

## 03 完成

只需使用 `cd campaignchain` 进入 `CampaignChain` 目录。然后使用 `sudo composer clear-cache --prod --no-debug` 清除缓存，然后运行 `sudo php app/console/scheduler de:run --prod --no-debug`。你可以将 `CampaignChain` 调度器设置为 cron 任务，以确保它每分钟运行一次以更新状态。运行命令：

```bash
crontab -u <username>

*/ * * * * /usr/bin/php /path/to/campaignchain/app/console scheduler:run
```

你现在已经准备好运行服务器了：

```bash
sudo php app/console/server:start
```
