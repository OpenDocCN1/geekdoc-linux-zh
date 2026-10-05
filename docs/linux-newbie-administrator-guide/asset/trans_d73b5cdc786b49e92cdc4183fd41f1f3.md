

| http://sunsite.auc.dk/linux-newbie/ | 本文档的主站 (LNAG)，请收藏。 |
| http://www.kalug.log.net/linux-admin-FAQ/ | Linux 管理员常见问题（针对非新手）。 |
| http://members.aa.net/~swear/pedia/learning-linux.html | Gary 的百科全书——学习 Linux。请收藏。 |
| http://jgo.local.net/LinuxGuide/ | Josh 的主页。学习 Linux 的良好资源。 |
| http://www.control-escape.com/ | 这个对新手来说很不错！ |
| http://qlink.quensu.ca/~3st/linux-admin/ | 让 Linux 管理变得简单 (LAME)。“全新且改进版”(4月49日)。推荐。 |
| http://metalab.unc.edu/mdw/index.html#code | 大量的 Linux 文档。请收藏。 |
| http://www.slashdot.org/ | 极客、黑客、大师等人的讨论。 |
| http://www.freshmeat.org/ | 今日 Linux 发布版本的更新。 |
| http://www.linuxtoday.com/ | Linux 新闻——优秀的每日读物。请收藏。 |
| http://www.llp.fu-berlin.de | Linux 实验室项目。数据采集等。Linuxberg。大型门户。那里无一不包。我喜欢 Linux 软件评分，并正在安装获得 5 只企鹅的包。请收藏。 |
| http://www.linuxberg.com/ | Linux 计数。注册成为一名 Linux 用户吧！ |
| http://counter.org/linuxcounter_eng.html | 查看 Dennis Havlik 关于 Linux 增长和地理分布的惊人地图。 |
| http://www.apuniv.ac.at/users/havlik/Album/iw10/linux-Counter/ | Linux 常见问题。 |
| http://www.cl.cam.ac.uk/users/iwj0/linux-faq/index.html | Sun 归档中大量的 Linux 软件。请收藏。 |
| ftp://sunsite.unc.edu/Pub/Linux/ | Linux 应用程序。 |
| http://stommel.tamu.edu/~baum/linuxlist/linuxlist/linuxlist.html | Linux 应用程序。 |
| http://www.boutelle.com/svn/ | Linux 应用程序。 |
| http://www.linuxlinks.com/Software/ | Linux 应用程序。 |
| http://directorysearch.mozilla.org/Computers/Operating_Systems/Linux | 棒的新门户（比 yahoo 好）以及为 Linux 新手提供的优秀链接。 |
| http://dir.yahoo.com/.../n/linux | Yahoo 的 Linux 条目。 |
| http://www.debian.org/ | Debian Linux 站点。 |
| http://www.redhat.com/support/docs/hardware.html | Linux 硬件兼容列表。 |
| http://metalab.unc.edu/mdw/linux.html | 许多用的 Linux 链接 |
| http://www.cse.csw.edu.au/~conrad/linux/ | 大量的优质链接。 |
| http://www.linuxstart.com/documentation/ | 更多 Linux 文档链接。 |
| http://www.linuxlinks.com/ | 更多的 Linux 链接。 |
| http://www.gnu.org/ | GNU 主站 (GNU 的含义是 不是 Unix。这是一个递归定义)。 |
| http://www.redhat.com/ | 红帽站点。它通常太忙了，没空理。 |

前往第 3 部分：基础操作常见问题

# Linux 新手管理员指南

ver. 0.59 1999-11-05

## 第 3 部分：基础操作常见问题

由 Stan 和 Peter Klimas 编写

为在家庭电脑上安装 Linux 或管理家庭网络的新 Linux 用户经常提出的问题提供解答

根据通用公共许可证发布 http://www.gnu/copyleft/gpl.html。欢迎您的反馈、意见、修正和改进。请发送至 bklima@magna.ca

### 快速站点导航：

-- 开始：Linux 新手管理员指南
- 第 0 部分：给尚未决定者（Linux 的优势）
- 第 1 部分：安装 Linux 之前
- 第 2 部分：Linux 资源、帮助及其他
- 第 3 部分：基础操作常见问题
- 第 4 部分：Linux 新手管理员常见问题
- 第 5 部分：如何升级内核
- 第 6 部分：Linux 快捷键和命令
- 第 7 部分：核心 Linux 应用（专利或非）

### 本页内容：

#### 3.1 基础

- 3.1.1 文件名 [p 28]
- 3.1.2 不同的目录是做什么的？[p 30]
- 3.1.3 我如何运行程序？[p 31]
- 3.1.4 我如何更改 PATH？[p 33]
- 3.1.5 我如何关闭电脑？[p 34]
- 3.1.6 我如何处理挂掉的程序？[p 35]

#### 3.2 用户、密码、文件权限与安全

- 3.2.1 主目录、root、添加用户 [p 38]
- 3.2.2 关于密码安全 [p 39]
- 3.2.3 关于密码安全 [p 39]
- 3.2.4 关于密码安全 [p 41]
- 3.2.5 关于密码安全 [p 45]

#### 3.3 任务调度

- 3.3.1 任务调度 [p 46]
- 3.3.2 任务调度 [p 47]

#### 3.4 使用

- 3.4.1 使用空间 [p 49]
- 3.4.2 使用空间 [p 49]

#### 3.5 Shell

- 3.5.1 Shell [p 50]
- 3.5.2 Shell [p 51]

#### 3.6 简单

- 3.6.1 简单 [p 52]
- 3.6.2 简单 [p 52]
- 3.6.3 简单 [p 53]
- 3.6.4 简单 [p 54]

#### 3.7 安装

- 3.7.1 安装 [p 54]

# 基础操作

## 3.1 基础

### 3.1.1 文件名

Linux 是区分大小写的。文件名长度可达 256 个字符，通常包含字母、数字、下划线、点等。以下是一些元字符的含义：

- * = 匹配零个或多个字符（文件名开头的点除外）。
- ? = 匹配任意单个字符。
- [abc1] = 匹配枚举集合中的单个字符。在此例中，集合是 'a'、'b'、'C' 或 '1'。
- [a-z] = 匹配任何小写字母。
- [-F] = 匹配拉丁表中 A 到 F 的任意大写字母。
- [0-9] = 匹配任何数字。
- [a-zA-Z0-9] = 匹配任何字母（大写或小写）或任何数字。

示例：此命令将显示当前目录下的每个文件名，排除以 "."（点）开头的文件：

```
ls *
```

此命令的等效操作是输入 "ls" 或 "dir"。以 "." 开头的文件不会显示，因为 "." 作为文件名的第一个字符不会被 "*" 匹配。使用 ls -a（带有 "all" 选项的列表）或 ls .* 来查看“点”文件。点文件位于用户主目录中，通常用于存储用户级配置。

为了处理包含元字符的文件名，我使用一对单引号（' '），这样 shell 就不会解释它们的含义。例如，要删除一个 file* 文件，我会使用：

```
rm 'file*'
```

请注意，使用双引号（" "）包裹的效果比使用单引号（' '）的要弱。

此命令将显示任何包含点的文件名：

```
ls *.*
```

此命令将显示任何包含两个点的文件名：

```
ls *.*.*
```

