
```bash
stetson@linux_rocks# rsync /my_local_directory root@localhost:my_remote_directory
```

将远程文件传输到本地系统：

```bash
stetson@linux_rocks# rsync username@remotehost.com:/remote/directory /local/directory
```

干得好！这是对使用内置在大多数发行版中的 Linux 工具进行文件传输的方法的简要概述。事实上，文件备份和传输是保持关键文件安全的重要概念。学习它，实践它，热爱它。

## 6. 实战派武士技能与面试题

**引言**

在本章中，我们将查看我所谓的“实战级” Shell 武士技能。尽管书中的绝大部分内容都显得如此神秘……（希望这一部分有助于揭秘 DNS 的内部机制以及你的 Linux 系统如何处理 DNS。熟通 DNS 是 Shell 武士和系统管理员的关键技能！）

### Nginx

在本章中，我们将查看我所谓的“实战级” Shell 武士技能。尽管书中的绝大部分内容都显得如此神秘……（希望这一部分有助于揭秘 DNS 的内部机制以及你的 Linux 系统如何处理 DNS。熟通 DNS 是 Shell 武士和系统管理员的关键技能！）

### 安装 Nginx

在本章中，我们将查看我所谓的“实战级” Shell 武士技能。尽管书中的绝大部分内容都显得如此神秘……（希望这一部分有助于揭秘 DNS 的内部机制以及你的 Linux 系统如何处理 DNS。（等等，OCR 文本重复了））

请选择你所在的地理区域。随后的配置问题将通过列出城市列表（代表它们所在的时区）来缩小范围。

+   1. 非洲 3. 南极洲 5. 北极 7. 大西洋 9. 印度
11. SystemV 13. Etc
2. 美洲 4. 澳洲 6. 亚洲 8. 欧洲 10. 太平洋
12. 美国

地理区域：12

请选择与你时区对应的城市或地区。

+   1. 阿拉斯加 3. 亚利桑那 5. 东部 7. 印第安纳-斯特克 9.
山地 11. 萨摩亚
2. 阿留申 4. 中部 6. 夏威夷 8. 密歇根 10.
太平洋

时区：5

你的公网 IP 地址。`Ifconfig.me` 是一个简单返回你 IP 的免费服务。

如果一切顺利，你应该能看到 Nginx 的默认落地页：

![](img/368b2a05101953edc8b0734547e5066c_204_0.png)

这很棒，但如果我们只能看到默认配置页面，对我们来说帮助不大！我们想在 Nginx 上存储自己的网页！

我们可以导航到 `/var/www/html` 并使用 `ls` 查看内容，会在那里看到 `index.nginx-debian.html` 文件：

```
root@linux_rocks://var/www/html# ls
index.nginx-debian.html
```

让我们将其重命名并以 `.bak` 结尾，我们可以保留该文件。然后在 `/var/www/html` 中创建一个新的 `index.html` 文件：

```
root@linux_rocks:/var/www/html# mv index.nginx-debian.html
index.nginx-debian.bak
root@linux_rocks:/var/www/html# touch index.html
```

现在，打开你喜欢的文本编辑器，我们将在 `index.html` 中编写一些我们自己的 HTML！在这个示例中，我使用了 Tailwind 进行一些基础的 CSS 样式设置，如果你只想快速看到页面，可以省略该标签：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>My first Nginx Web Page!</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body>
  <h1 class="text-2xl text-orange">
    Hello Shell Samuraiis!
  </h1>

  <div class="container">
    Welcome to my web page
  </div>
</body>
</html>
```

保存文件并关闭它。回到浏览器并点击刷新！

![](img/368b2a05101953edc8b0734547e5066c_205_0.png)

# Hello Shell Samuraiis!

欢迎来到我的网页

太棒了！我们刚刚用 Nginx 从零开始提供了自己的网页，干得好！配置 Nginx 的方法还有很多很多，但我想保持简练，简单地向你介绍这款软件。

正如前面提到的，今天大约 30% 的网站以某种形式使用 Nginx。Nginx 还有许多其他方法让你配置它来作为代理或负载均衡器或其他用例。将 Nginx 加入你的工具箱是让自己作为一名 Shell Samurai 更有价值的一种简单直接的方法！

## 使用 Git 和版本控制

虽然 Git 不在理解 Linux 的范围内，但我认为你应该了解它，因为你以后职业生涯的某个时刻可能需要使用 Git。

在本地系统上处理代码和配置文件很棒，但当你想要与其他人合作时会发生什么？你如何协作修改网页、配置文件和源代码呢？你应该把代码压缩并通过电子邮件发送给同事让他们进行修改吗？USB 盘？Dropbox 或 Google Drive？将代码保存在共享驱动器上并直接修改？如果所做的更改完全破坏了你的应用程序会发生什么？如果两个开发者对同一个文件进行了修改会发生什么？

在版本控制出现，这些都是开发者和系统管理员必须面对的非常真实的问题。今天，我们不需要担心这些问题，因为已经为此构建了解决方案。版本控制允许团队成员协作编写代码，保留所做更改的运行日志，访问不同的版本以及更多功能。

Git 是最常用且应用广泛的版本控制系统。在本节中，我们将创建自己的 Git 仓库，提交一些代码并开始理解 Git 的基本概念。

### Git 概述

除了开发 Linux 内核外，Linus Torvalds 在 2005 年还开发了 Git 来帮助 Linux 的开发！Git 软件是开源的。你可能听过微软收购了 GitHub，并认为这意味着他们也获得了 Git。GitHub 仅仅是一个 Git 托管平台。还有其他 Git 托管平台，如 GitLab 和 Bitbucket。你不需要将代码托管在 GitHub。

Git 软件是一个分布式版本控制系统。这意味着每个开发者在本地机器上都保留代码库的完整副本。他们不需要连接到文件共享或中央服务器即可对代码进行更改或贡献。

Git 有分支（branch）和合并（merge）的概念，允许开发者对代码库进行隔离更改以添加新功能或修复错误。然后，他们将代码合并回主代码库。

对代码库所做的每一次更改都会随时间被记录和跟踪。如果发生任何错误或你想查看某段代码的历史，Git 让这变得非常简单。

### Git 核心概念

在我们继续之前，我们将定义几个理解 Git 所必要的术语。

仓库（Repository）是一个中央存储区域，代码库中的所有代码和文件都存储在那里。开发者在这里保存工作、与他人协作并跟踪他们的更改。

对代码库进行的更改被称为提交（commits）。提交就像是代码库在特定时间的快照，并带有一条描述更改的短消息。提交被赋予了可以引用的唯一 ID。

分支（Branches）是开发者处理代码库不同版本的方式。开发者会创建一个新分支，进行更改，稍后请求合并。

### 开始使用 Git

首先，在你的系统上安装 `git`。接下来，在浏览器中注册 GitHub。一旦你注册了 GitHub，你将看到一些指令：

- 公开（Public）：互联网上的任何人都可以看到。
- 私有（Private）：你选择谁可以看到它。
- 名称（Name）：选择你的仓库名称。
- 描述（Description）（可选）：为你的项目写一段长描述。
- 添加 README 文件：跳过此步骤。
- 添加 .gitignore：选择不想跟踪的文件。
- 选择许可（Choose a license）：许可告诉其他人他们对你的代码可以做什么。

### 在命令行上创建新仓库

点击“或在命令行上创建新仓库”下方的按钮，将这些命令保存到剪贴板。让我们逐行解释你复制的命令：

`echo "# my_repo" >> README.md`

这一行将文本 `my_repo` 回显名为 `README.md` 的文件中。`README.md` 文件中的任何内容都将以 markdown 格式格式。Markdown 是一种文本格式，允许我们定义列表、标题和其他链接等文本特征。在文本前加上 `#` 会使其成为一级标题（Heading 1）。

`git init`

此命令将在本地系统中创建一个新的 git 仓库。

`git add README.md`

此命令将 `README.md` 文件添加到暂存区（staging）。这告诉 `git` 我们想在下次提交中包含此文件。
