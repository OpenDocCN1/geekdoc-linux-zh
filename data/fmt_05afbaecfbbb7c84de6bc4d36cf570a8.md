
```
$ gitpod /workspace/Linux-for-OSINT-21-day (main) $ dig google.com
; << DIG 9.10.12-Ubuntu22.04.3-Ubuntu >>> google.com
; global options: +cmd
; Got answer:
; <<HEADER>>: QUERY, status: NOERROR, id: 39629
; flags: qr rd QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1
; OPTION SECTION:
; VERSION: 9, flags=; udp: 1232
; QUESTION SECTION:
; google.com.                               IN        A
; ANSWER SECTION:
; google.com.                            122       IN        A       142
```

## Netlas

如你所见，它显示了信息、DNS 信息以及与该域名相关的各种服务器地址，这些可以用于进一步调查以及许多其他信息。

# 20 个领域调查 Python 软件包

只需在命令行中输入：`pip install + 包名`

- `python-whois`
- `dnstwist`
- `builtwith`
- `waybackpy`
- `netlas`
- `pyseoanalyzer`
- `shodan`
- `dns-crawler`
- `oxydork`
- `urlscanio`
- `virustotal-python`
- `pysnyk`
- `pydork`
- `EmailHarvester`
- `sitemap-generator`
- `censys`
- `wapiti3`
- `dirhunt`
- `cloudscraper`
- `metadata_parser`

![](img/03e4d38bded7def6bb51288422c4f89d_134_0.png)

图片来自推特。

图片中列出了一份小列表，包含了用于收集网站信息的 Python 软件包。要安装其中的每一个包，请在命令行执行 `pip install (包名)`，然后使用 `help` 命令来了解某个特定包的用途。

这是书中最大的一项作业，你可以花费几周时间来完成它。明天我们将尝试更多的命令，而接下来的课程将不再有命令示例，只需阅读和思考。

# 第 19 天 Git 和 Github

`Git` (https://git-scm.com) 是由 Linus Torvalds 创建的软件版本控制系统。根据 StackOverflow 的 2022 年调查，超过 93% 的开发者将其作为主要的版本控制工具（https://survey.stackoverflow.com/2022/#section-version-control-version-control-systems）。

Git 和 Linux 的情况极其罕见，一个人在一生中成功发明了两个改变游戏规则的软件（1991 年的 Linux，2005 年的 Git）。

即使你打算进行任何开发工作，你仍然可以从基础 Git 技能中为 OSINT（开源情报）、运行不同的工具以及分析存储了大量文本数据的 Github 仓库（例如钓鱼域名列表或智能合约文件）中受益。

Gitpod 已经安装了 Git，但在其他情况下，你可能需要手动安装：

```bash
sudo apt-get update
sudo apt-get install git
```

![](img/03e4d38bded7def6bb51288422c4f89d_135_0.png)

让我们去 https://github.com/new 并创建一个新的空白 Github 仓库。

## 创建仓库

仓库包含所有项目文件，包括修订历史。在其他地方已经有一个项目仓库了？导入它。

必填字段用星号 (`*`) 标记：

| | 仓库名称 * |
|---|---|
| cipher387 | linux_for_osint_21_day |
| | linux_for_osint_21_day 已可用。 |

描述（可选）

用于你书籍的文本仓库

| | 可见性 |
|---|---|
| 公共 (Public) | 所有人都可以查看和克隆此仓库。你以后可以更改。 |
| 私有 (Private) | 只有你可以查看并向此仓库提交代码。 |

使用以下选项初始化此仓库：

| 添加 README 文件 |
|---|---|
| [ ] 你可以在这里为你的项目编写详细描述。了解关于 README。 |

添加 `.gitignore`

| | gitignore |
|---|---|
| | 从模板中选择以忽略文件列表。了解关于 `.gitignore`。 |

选择许可证

| | 许可证 (License) |
|---|---|
| | 许可证告诉他人他们对你的代码可以做什么，不能做什么。了解许可证。 |

这将被设置为默认。在你的设置中更改默认名称。

你正在个人账户中创建一个私有仓库。

![](img/03e4d38bded7def6bb51288422c4f89d_136_0.png)

查看图片，填写仓库名称和描述字段，将仓库设为私有，创建一个 `README.MD` 文件并点击 Create（创建）。

![](img/03e4d38bded7def6bb51288422c4f89d_141_0.png)

它们在处理简单任务时非常擅长节省时间，但在处理更复杂的问题时，可能会出错并误入歧途。请小心。

141

## explainshell.com

关于 Shell 中的 `for user in！` 主题 . 显示所有，导航：解释 `crontab(1)` 解释 shell 语法

```bash
for user in $(cut -f1 -d: /etc/passwd); do crontab -l -u $user 2>/dev/null; done
```

| for name in [ in [ word ... ] ]; do list; Done | |
| :--- | :--- |
| 随后的单词列表将被展开，生成一个项目列表。变量名被设置为 |
| 依次处理此列表中的每个元素，并每次执行 list。如果单词写为 |
| for，命令为每个设置定的位置参数执行一次 list（参见 PARAMETERS）。返回状态是最后一个执行的命令的退出状态 |
| 如果后续列表的展开结果为空列表，则不执行任何命令，返回状态为 0。 | |

为单个用户维护 crontab 文件 (Vixie Cron)

在命令执行之前，其输入和输出可以使用 shell 解释的特殊符号进行重定向。重定向也可用于环境打开和关闭文件。以下重定向操作符可能出现在简单命令之前、命令内部或跟在命令之后。重定向按照它们出现的顺序从左到右进行处理。

## 重定向输出

输出重定向会导致单词展开结果的文件名在文件描述符 n 上打开写入，如果未指定 n，则使用标准输出（文件描述符 1）。如果文件不存在，则创建它；如果文件存在，则将其截断为零大小。

不要忘记，你不能要求 AI 助手从零开始编写代码或命令，但解释 Stackoverflow 上的某些命令或脚本的作用。你也可以使用 Explain Shell (https://explainshell.com/) 来实现此目的。

## phind 用于下载 google 主页的搜索聊天命令

答案 | PHIND VS 模型

使用 `curl` 命令下载 `google.com`，可以使用以下命令：

```bash
curl https://www.google.com/?hl=en_us.html
```

以下是该命令的逐步解释：

- 1. `curl` 是用于通过 URL 传输数据的工具。它支持多种协议，包括 HTTP、HTTPS、FTP、FTPS、SCP、SMTP 和 SSL/TLS。
- 2. `google.com` 是你想要下载的网站 URL。这是 Google 的主页。
- 3. `>` 是 Unix 类操作系统中的一种重定向，它用于将命令的输出重定向到文件。在这种情况下，它将 `curl` 的输出（即页面的 HTML 内容）重定向到名为 `google.html` 的本地文件。
- 4. `google.html` 是正在保存的文件名。如果文件不存在，将创建它。如果文件已存在，将会被覆盖。
- 5. 运行命令后，`google.html` 文件将位于你的当前目录。该文件包含 Google 主页的 HTML 内容。你可以在网页浏览器中打开此文件查看网页，或者可以在文本编辑器中打开它查看 HTML 源代码。

## 建议

我可以使用 `curl` 下载 Google 主页的特定部分吗？

![](img/03e4d38bded7def6bb51288422c4f89d_143_0.png)

| 来源 | Y |
| :--- | :--- |
