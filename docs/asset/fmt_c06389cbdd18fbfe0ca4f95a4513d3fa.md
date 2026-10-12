
# Espanso 使用说明

## 用法

`espanso [FLAGS] [SUBCOMMAND]`

```
- 标志 (FLAGS):
  -h, --help
  -v
  -V, --version
    打印帮助信息
    设置详细程度
    打印版本信息

- 选项 (OPTIONS):

命令 (COMMANDS):
  code
  edit
  nc-path
  install
  log
  migrate
  package
  restart
  service
    向 espanso 编辑器发送命令以编辑配置文件
    从 PATH 中打开默认文本编辑器命令的快捷方式
    打印此消息或给定子命令的帮助信息
    打印守护进程日志
    从 CLI 列出并验证条目
    自动将配置迁移到新版本
    打印所有 espanso 目录以轻松定位配置和匹配项
    一组管理 espanso 服务的命令（例如，启用系统启动时自动启动）
    将 espanso 作为服务启动
    检查守护进程是否运行
    删除软件包
  ununinstall
  workaround
    一组解决常见问题的变通方案。
```

## 故障排除

图 1：你可以使用 `-h` 或 `--help` 来识别可用选项。

`match/` 是你指定 espanso 扩展什么以及扩展成什么的方式。工具在 `/match/base.yml` 文件中提供了一些简单的替换示例（图 3）。匹配项由触发器（trigger）和替换（replace）值对定义。触发器是触发替换的字符串，而替换是它被替换的文本。一个简单的示例如下：

为了创建一个新行，YAML 使用两个运算符 `|`，并且当两行进入视野时生效。如果你在行中使用 `|` 作为第一个运算符，另一方面，如果将缩进的三行作为 `replace |` 使用，应用程序将在单行中应用替换。你可以在 Stack Overflow [4] 上学习更多关于这些标量的知识。

```yaml
trigger: ":"
replace: "Kind, regards,"
```

另一个示例出现在信件和邮件的结尾，它给你两行输出：

```yaml
trigger: ":"
replace: "Love,

s/Peter"
```

### 静态还是动态？

Espanso 区分了静态和动态替换。上述描述的示例属于静态类别；它们的输出始终保持不变。动态替换的一个典型例子是放置当前行的文本。

## 全局变量

创建全局变量的一个原因是你可以在多个地方使用它们。在 YAML 文件的顶部定义全局变量。它们适用于此文件及其子集中定义的所有替换。如果你经常写错单词（例如，输入了额外的字符而不是别的），Espanso 证明非常有用。此处使用的真实触发器如详细配置 [5] 所示。

**列表 4：示例**

| 触发器 (trigger) | 替换 (replace) |
| :--- | :--- |
| `01` | `:"div"` |
| `02` | `:"<<div></</div>>"` |
| `03` | `:"quote"` |
| `04` | `"三个人可以保守一个秘密，如果有两个的话。"` |
| `05` | `:"quote"` |
| `06` | `"存在或不存在，这是一个问题。"` |
| `08` | `:"replace"` |
| `09` | `"如果你想让事情正确，就自己做。"` |
| `10` | `image_path:"PATH/TO/IMAGE.png"` |

## LINUX 用户西班牙语指南

语言。如果需要，Espanso 还可以触发图像（ 9 和 10）并创建各种形式 [6]。

## 软件包 (Packages)

得益于 Espanso 的软件包策略，你可以还原其他用户创建的副本。为了方便你操作，该软件自带了一个专用的包管理器，它主要与网页上的 Espanso Hub (5) 配合，但也接受其他来源。Espanso Hub [7] 显示了可以按发布者或用途发布的软件包。关于这有单独的文档 [8]。在最简单的情况下，只需替换 `espanso install` 命令来安装软件包即可。

除了 Espanso Hub 之外，还有其他仓库 [9]。我开始从 Hub 安装 `html-utils` 软件包。使用 DIY 副本，将此处的触发器替换，例如 `div:espanso-match`。软件包配置可以在此处找到。我还添加了第三方的 `espansoconfig` [9] 仓库。这稍微复杂一点。首先，你需要使用第 1 到 5 行的命令从 GitHub 将仓库克隆到你的主目录。你会找到 `espanso-config/` 目录，其中包含了使用符号链接的 Espanso（第 2 行）。这是

![](img/4dce49e5b3f3b719f67be60db9a2a5ec_77_0.png)

图 4：Espanso，多个替换项可以使用相同的触发器。`quote:` 触发器显示了如何通过按下键盘快捷键选择你想要的内容。

你将找到带有实用配置的 YAML 文件。

**列表 5：包含仓库**

```bash
$ git clone https://github.com/Lissy92/espanso-config.git
$ ln -s ~/espanso-config/ ~/.espanso/match/packages
```
