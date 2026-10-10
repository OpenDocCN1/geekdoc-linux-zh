
你在此脚本中执行的所有操作都可以在 `playbook` 中完成。只需查看列表 5-2 中的 `playbook` 示例，即可看到 `playbook` 的样子。如果你观察得足够仔细，你会发现临时命令中指定的所有元素也都出现在 `playbook` 中。

### 列表 5-2 从 Playbook 配置主机

```yaml
---
- name: install start and enable httpd
  hosts: all
  tasks:
  - name: install package
    yum:
      name: httpd
      state: installed
  - name: start and enable service
    service:
      name: httpd
      state: started
      enabled: yes
```

## Playbook

`Playbook` 是 `play`（场）的集合。每个 `play` 针对特定的主机，并在每个 `play` 中指定一个任务列表。在列表 5-2 的示例 `playbook` 中，定义了一个名为“install start and enable httpd”的 `play`。

`Playbook` 使用 `YAML` 格式编写，通常以 `.yml` 或 `.yaml` 扩展名保存。`YAML` 格式本质上将对象指定为键值对。可以使用破折号来指定嵌入对象的列表。

在每个 `playbook` 的开头，你会看到三个破折号。使用这些字符可以方便地将 `playbook` 代码嵌入到其他内容中，并在包含它时轻松地隔离出 `playbook` 代码。

当你编写 `playbook` 时，目标主机是在 `play` 中指定的，而不是在运行 `playbook` 的命令中指定的（后者发生在临时命令中）。在你指定目标主机后，要指定一个任务列表。列表中的每一项都用连字符标识。对于每个任务，你需要指定该任务运行的 `Ansible` 模块和一个名称。注意，为任务使用名称不是强制的，但强烈建议这样做，因为使用名称的任务会稍微更容易识别哪些任务已成功运行。接下来，你应该识别任务应该运行的参数。

要识别 `playbook` 中的层级关系，你需要使用缩进。缩进的基本规则非常简单：

- 层级结构中相同层的数据元素必须具有相同的缩进。
- 作为另一个元素子节点（属性）的项目，其缩进比父元素深。

你使用空格来创建缩进。对于使用多少个空格没有要求，但使用两个空格是常见的。不允许使用制表符进行缩进。

在 `playbook` 内部，定义了一个或多个 `play`。`play` 是 `playbook` 中的最高层，每个 `play` 都以连字符开头。这是因为 `playbook` 定义了一个 `play` 列表，即使列表只包含一个 `play`，它也是有效的。`play` 的所有属性（`name`、`hosts` 和 `tasks` 单词）都在同一层级缩进，接下来是任务列表。任务列表是 `play` 的一个属性，这些任务比父项深缩进一层，以显示 `play` 和任务之间的层级关系。下一层缩进发生在任务参数级别，传递给任务的每个参数都会再深缩进一层。

> **提示**
>
> 为了让缩进工作更轻松，你可以配置 `vi` 编辑器。如果文件 `~/.vimrc` 中包含以下行内容，那么当 `vi` 检测到创建了 `YAML` 文件时，缩进会自动发生。注意，这需要你对文件使用 `.yaml` 或 `.yml` 扩展名。

```
autocmd FileType yaml setlocal ai ts=2 sw=2 et
```

在 `playbook` 中，你可能会发现一个或多个 `play`。每个 `play` 都有一些必需元素，列在表 5-2 中。

## 核心主题

**表 5-2 Playbook Play 必需键**

| 键 | 用途 |
| :--- | :--- |
| `hosts` | 执行此 `play` 的主机 |
| `name` | `play` 的名称 |
| `tasks` | 在此 `play` 中执行的一个或多个任务 |

## 运行 Playbook

要运行 `playbook`，你使用命令 `ansible-playbook listing52.yaml`。结果所示列表 5-3。请注意，取决于受管机器的状态，你可能会看到略有不同的结果，显示“changed”而不是“ok”。

### 列表 5-3 运行 Playbook 输出

```
[ansible@control ~]$ ansible-playbook listing52.yaml

PLAY [install start and enable httpd]
********************************************************************

TASK [Gathering Facts]
********************************************************************
ok: [ansible2]
ok: [ansible1]

TASK [install package]
********************************************************************
ok: [ansible1]
ok: [ansible2]

TASK [start and enable service]
********************************************************************
ok: [ansible2]
ok: [ansible1]

PLAY RECAP
************************************************
ansible1 : ok=3 changed=0 unreachable=0 skipped=0
ansible2 : ok=3 changed=0 unreachable=0 skipped=0
```

在 `playbook` 中，你可能会发现一个或多个 `play`。每个 `play` 都有某些必需元素，如表 5-2 所示。

1. 在此阶段，你可以开始定义任务了。第一个任务确保使用 `yum` 模块来定义 `vsftpd` 软件包。注意缩进，它表明该任务是 `play`（剧）的子元素：

```yaml
---
- name: install and start the vsftpd service
  hosts: all
  tasks:
    - name: install vsftpd
      yum:
```

2. 在此阶段，你可以指定 `yum` 模块的参数。因为这些参数是 `yum` 模块的子元素，你需要另一层缩进：

```yaml
---
- name: install and start the vsftpd service
  hosts: all
  tasks:
    - name: install vsftpd
      yum:
        name: vsftpd
        state: latest
```

3. 现在第一个任务已经定义完成，你可以指定下一个任务，该任务调用 `service` 模块来启动并启用 `vsftpd` 服务。注意该任务的缩进与 `yum` 任务处于同一级别：

```yaml
---
- name: install and start the vsftpd service
  hosts: all
  tasks:
    - name: install vsftpd
      yum:
        name: vsftpd
        state: latest
    - name: start and enable vsftpd service
      service:
        name: vsftpd
        state: started
        enabled: yes
```

4. 现在剧本（`playbook`）已完成，将你的更改写入文件并退出编辑器。接下来，使用 `ansible-playbook exercise51.yaml` 运行该剧本。

5. 观察剧本的输出，并验证所有内容执行正确。

## 使用 YAML

`YAML`（根据某些人的说法是 `YAML Ain’t Markup Language`，另一些人则认为是 `Yet Another Markup Language`）是一种易于阅读的数据序列化语言。`YAML` 是一种常用于配置文件的通用语言，不仅用于 `Ansible` 中，也用于 `Kubernetes` 以及某些 `Linux` 服务的配置中。`YAML` 并不难使用，但在处理 `YAML` 时，你应该了解以下几点。

## 缩进

首先，`YAML` 使用缩进。如之前讨论的，缩进标识了配置部分之间的关系，以便你轻松地看出哪些是父对象，哪些是子对象。缩进最重要的规则是必须使用空格而不是制表符（`tabs`）。

## 使用键值对

`YAML` 的核心是定义键值对，也称为字典。这种键值对的示例是 `name: vsftpd`。键值对可以通过两种方式定义：`key: value` 或 `key=value`。在这两种方法中，首选第一种，但第二种方法同样有效。

如果 `YAML` 中的某一个对象需要多个键值对来定义其属性，通常的做法是每行定义一个键值对。如果使用 `key=value` 格式，则可以在一行内定义所有多个键值对。列表 5-4 中的示例剧本展示了这样一个例子。

# 列表 5-4 定义键值对的多种方式

```yaml
---
- name: deploy vsftpd
  hosts: ansible2
  tasks:
    - name: install vsftpd
      yum: name=vsftpd
    - name: enable vsftpd
      service: name=vsftpd enabled=true
    - name: create readme file
      copy:
        content: "welcome to the FTP server\n"
        dest: /var/ftp/README
        force: no
        mode: 0044
...
```

在列表 5-4 的示例剧本中，定义了三个任务。在前两个任务中，所有的键值对都以 `key=value` 格式定义在所用模块名称的同一行。第三个任务以 `key: value` 格式单独定义了所有键值对。为了保持剧本的可读性，你应该只使用后一种方法。

> **注意**
>
> 在 `Ansible` 中，很多情况下可以使用不同的语法。本节仅作为使用 `YAML` 的介绍，而不是对该语言所有工作方式的完整概述。如果你需要更完整的 `YAML` 语法变体概览，请查阅 `Ansible` 文档中的“`YAML Syntax`”。

注意，在第三个任务中，使用了 `copy` 模块将一行文本复制到目标文件中。这是创建一个包含标准文本的配置文件的简单方法。还有其他模块可以管理需要复制到文件的文本；你将在第 8 章“部署文件”中学习它们。

## 理解 YAML 列表

当你在 `Ansible` 剧本中使用 `YAML` 时，键可以有一个值，而某些键可以有多个值。没有标准规则规定在什么情况下属于哪一种。键是否可以包含多个值取决于 `Ansible` 模块。例如，当你使用 `yum` 模块时，你可以为 `name` 键指定一个软件包列表。例如，当你使用 `service` 模块时，无法将列表作为 `name` 键的参数。模块文档通常会指示是否可以为特定键指定列表值。列表 5-5 展示了一个使用列表定义键值的剧本示例。

# 列表 5-5 使用列表安装多个软件包

```yaml
---
name: using lists
  hosts: all
  tasks:
    - name: install packages
      yum:
        name:
          - nmap
          - httpd
          - vsftpd
        state: latest
```

> **提示**
>
> `yum` 模块可以与不同的软件包状态配合。例如，你可以使用 `state: latest` 来确保软件包是最新版本。

## 使用字符串

在 `Ansible` 剧本中使用 `YAML` 时，经常会包含字符串。在 `YAML` 文件中使用字符串并不困难，因为字符串不需要使用引号来转义。然而，你仍然可以使用引号。这意味着以下写法都是有效的：

- `Line of text`
- `"Line of text"`
- `'Line of text'`

这里有两种处理多行字符串的方法。你可以使用 `|` 符号处理多行字符串以保留换行符。如果你希望多行字符串仅被视为文本，而不包含任何格式，可以使用 `>` 符号。使用 `|` 符号是因为你想保留格式；使用 `>` 符号是因为你想为了易读将文本拆分成多行。

## 验证语法

由于你很容易写错拼写或缩进错误的行，验证语法可能是明智的。`ansible-playbook` 命令提供了 `--syntax-check` 选项为此。列表 5-6 显示了该命令可能的输出。

```bash
[ansible@control ~]$ ansible-playbook --syntax-check listing54.yaml
ERROR! Syntax Error loading YAML.
mapping values are not allowed in this context
The error appears to be in '/home/ansible/listing54.yaml':
line 8, column 12, but may
else in the file depending on the exact syntax
The offending line appears to be:
name: httpd
state: latest
^ here
```

你可以看到，`ansible-playbook` 命令会对语法问题发生进行合理的猜测。根据具体的错误，这个猜测可能是准确的，也可能是完全不准确的。在这种情况下，它是准确的，如列表 5-7 所示（错误发生在早一行）。

> **提示**
>
> 书列表中相关的剧本代码可以在 `GitHub` 仓库中获取。

# 列表 5-7 错误的示例 YAML 文件

```yaml
---
- name: install start and enable httpd
  hosts: all
  tasks:
    - name: install package
      yum:
        name: httpd
        state: latest
    - service:
        name: httpd
        state: started
      enabled: yes
```

错误。你必须修复此错误并重新运行命令才能看到第二个错误。

关于 `--syntax-check` 的最后一点说明。它可能是一个很有用的选项，但你应该意识到 `ansible-playbook` 命令默认就会检查语法。因此，如果你刚刚运行了 `ansible-playbook listing56.yaml`，你将看到完全相同的消息。

## 执行 Playbook 的演练运行（Dry Run）

在实际运行 `playbook` 并对托管主机进行所有修改之前，执行演练运行是有意义的。你可以通过使用 `ansible-playbook -C myplaybook.yaml` 命令来实现。在执行演练运行期间，`ansible-playbook` 命令会向你显示哪些主机将在运行 `playbook` 时被更改，而不会实际应用更改。示例请参见列表 5-8。之后，你可以完成练习 5-2 来练习 `YAML` 技能。

## 列表 5-8 执行 Playbook 的演练运行

```
[ansible@control ~]$ ansible-playbook -C listing56.yaml

PLAY [using lists]
****************************************************

TASK [Gathering Facts]
****************************************************
ok: [ansible2]
ok: [ansible1]
```

```
TASK [install packages]
**************************************************
changed: [ansible2]
changed: [ansible1]

PLAY RECAP
**************************************************
ansible           : ok=2 changed=1
unreachable=0 failed=0 skipped=0 rescued=0
ignored=0
ansible           : ok=2 changed=1
unreachable=0 failed=0 skipped=0 rescued=0
ignored=0
```

## 练习 5-2 练习 YAML 技能

1. 打开编辑器创建文件 `exercise52.yaml`。通过包含以下行来定义 `playbook` 头部：
