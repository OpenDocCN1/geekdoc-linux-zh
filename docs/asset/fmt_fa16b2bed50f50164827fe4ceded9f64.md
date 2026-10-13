
- removed: 模块已从发布中移除，但为了存根以帮助旧用户迁移到新模块。

> 注意

`stableinterface` 状态仅表示模块的接口是稳定的，并不评估模块的代码质量。

`supported_by` 字段记录了 Ansible 社区中维护该模块。可能的值有：

- `core`: 由 Ansible 上游核心维护，并始终包含在 Ansible 中。
- `curated`: 由社区中的合作伙伴或公司提交并维护。这些模块的维护者必须关注上游的任何问题或拉取请求。核心开发者在社区维护者批准更改后，对精选模块提出更改。核心提交确保由于 Ansible 引擎更改导致这些模块出现的问题得到修复。这些模块目前包含在 Ansible 中，但在未来的某个时刻可能会单独打包。

Ansible 上游社区有一个 Ansible 及其集成模块的问题跟踪器：https://github.com/ansible/ansible/issues。

有时，不存在你想要的操作模块。作为终端用户，你也可以编写自己的 playbook，或从第三方获取模块。Ansible 会在 `ANSIBLE_LIBRARY` 环境变量指定的位置搜索自定义模块，如果未设置该变量，则在当前的 Ansible 配置文件中搜索。Ansible 还会相对于当前运行的 playbook 在 `../library` 目录搜索自定义模块。

```
library = /usr/share/my_modules
```

关于编写模块的信息超出了课程的范围。关于如何编写的文档可以在此处查看：https://docs.ansible.com/ansible/latest/dev_guide/developing_modules.html。

## 重要

使用 **`ansible-doc`** 命令来查找并学习如何为你的任务使用模块。

可能的情况下，尽量避免在 playbook 中使用 `shell` 和 `raw` 模块，尽管它们看起来用起来很简单。由于这些模块会执行任意命令，使用这些模块很容易编写出非幂等（non-idempotent）的 playbook。

例如，以下使用 `shell` 模块的任务不是幂等的。每当运行 play 时，它都会重写 `/etc/resolv.conf`，即使该文件已经包含了 **`nameserver 192.0.2.1`** 这一行。

- name: 非等的 shell module

  shell: echo "nameserver 192.0.2.1" > /etc/resolv.conf

有几种方法可以使用 `shell` 模块以幂等的方式编写任务，进行一些更改并使用 shell 是最佳方法。更快的解决方案可能是使用 **`ansible-doc`** 发现 `copy` 模块，并使用它来实现所需的效果。

如果 `/etc/resolv.conf` 文件已经包含了正确的内容，则以下示例将不会重写该文件：

- name: 使用 copy module 的幂等方法

  copy:

    dest: /etc/resolv.conf

    content: "nameserver 192.0.2.1\n"

`copy` 模块会测试状态是否已经满足，如果是，它将不会进行任何更改。`shell` 模块提供了很大的灵活性，但也需要更多关注以确保它以幂的方式运行。

幂等的 playbook 可以反复运行，以确保系统处于特定状态，而如果系统已经处于该状态，则不会中断。

# PLAYBOOK 语法变体

本章的最后一部分研究你可能会遇到的某些 YAML 或 Ansible Playbook 语法变体。

## YAML 注释

注释可用于增加可读性。在 YAML 中，数字或井号符号 (`#`) 右侧的所有内容都是注释。如果注释左侧有内容，请在符号前加一个空格。

```
# 这是一个 YAML 注释
```

```
some data # 这也是一个 YAML 注释
```

## YAML 字符串

YAML 中的字符串通常不需要放在引号，即使字符串中包含空格。你可以用双引号或单引号包裹字符串。

```
this is a string
```

```
'this is another string'
```

```
"this is yet another string"
```

有两种方法编写多行字符串。你可以使用垂直线 (`|`) 字符来表示要在字符串中保留的换行符。

```
include_newlines:
Example Company
123 Main Street
Atlanta, GA 38303
```

你也可以使用大于号 (`>`) 字符编写多行字符串，表示将转换换行符并删除行首的空白字符。这种方法通常用于在空格字符处折断长字符串，使其能够跨多行显示以提高可读性。

```
fold_newlines:
This is an example
of a long string,
that will become a single sentence once folded.
```

## YAML 字典

你已经见过了以缩进块形式编写的键值对集合，如下：

```
name: svrole
svcservice: http
svcport: 80
```

字典也可以用花括号包裹的内联块格式编写，如下：

```
{name: svrole, svcservice: http, svcport: 80}
```

在大多数情况下，应该避免使用内联块格式，因为它更难阅读。然而，至少有一种情况会更常用它。角色的使用将在课程稍后的部分讨论。当一个 playbook 包含一个角色列表时，使用这种语法更为常见，以便区分包含在 play 中的角色与传递给角色的变量。

## YAML 列表

你还见过用普通的单杠语法编写的列表：

```
- hosts:
  - servera
  - serverb
  - serverc
```

列表也有用方括号包裹的内联格式，如下：

```
hosts: [servera, serverb, serverc]
```

你应该避免这种语法，因为它通常更难阅读。

# 已弃的 key=value Playbook 简写形式

某些 playbook 可能会使用较旧的简写方法来定义任务，将模块的键值对与模块名放在同一行上。例如，你可能会看到这种语法：

```
- tasks:
  - name: shorthand form
    service: name=http enabled=true state=started
```

通常情况下你会按如下方式编写相同的任务：

```
- tasks:
  - name: normal form
    service:
      name: httpd
      enabled: true
      state: started
```

你通常应该避免简写形式并使用普通格式。

普通格式行数更多，但更容易操作。任务的关键字垂直排列，更容易区分。你的眼睛会直向下运行 play，减少了从左到右的移动。此外，普通格式是原生的 YAML；简写格式不是。如果你使用普通格式，现代文本编辑器中的语法高亮工具将比你使用简写格式时更好地帮助你更高效地工作。

你可能会在文档和他人的旧 playbook 中看到这种语法，并且这种语法仍然有效。

## 参考文献

`ansible-playbook(1)` 和 `ansible-doc(1)` 手册页

Intro to Playbooks – Ansible Documentation

https://docs.ansible.com/ansible/latest/user_guide/playbooks_intro.html

Playbooks – Ansible Documentation

https://docs.ansible.com/ansible/latest/user_guide/playbooks.html

Developing Playbooks – Ansible Documentation

https://docs.ansible.com/ansible/latest/user_guide/developing_playbooks.html

Module Support – Ansible Documentation

https://docs.ansible.com/ansible/latest/user_guide/modules.html

YAML Syntax – Ansible Documentation

https://docs.ansible.com/ansible/latest/user_guide/yaml_syntax.html

# 第 3 章 | 实现 Playbook

## 引导练习

在本次练习中，你将创建一个包含多个 play 的 playbook，然后用它来管理主机。

## 成果

你应该能够构建一个 playbook 并执行它。

## 开始之前

以 student 身份登录工作站。

## 3. 在第一个剧（play）的列表中添加一个任务，确保 `/var/www/html/index.html` 中包含正确的内容。

添加以下行来定义 `/var/www/html/index.html` 的内容。确保第一行缩进四个空格。
