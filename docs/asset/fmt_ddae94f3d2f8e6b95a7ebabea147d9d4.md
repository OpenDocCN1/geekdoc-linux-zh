
```yaml
tasks:
  - name: newbie exists with UID 4000
    user:
      name: newbie
      uid: 4000
      state: present
```

`tasks` 属性是剧的一部分，它实际上按顺序列出了在托管主机上运行的任务。列表中的每个任务本身都是键值对的集合。

在这个示例中，剧中的唯一任务有两个键：

- `name` 是一个可选的标签，用于记录任务的目的。为所有任务命名是一个好主意，有助于记录自动化过程中每个步骤的用途。
- `user` 是为此任务运行的模块。它的参数以键值对集合的形式呈现，这些是模块的子项（`name`、`uid` 和 `state`）。

以下是另一个带有多个任务的 `tasks` 属性示例，使用 `service` 模块确保几个网络服务在启动时启用。

```yaml
- name: web server is enabled
  service:
    name: httpd
    enabled: true
- name: NTP server is enabled
  service:
    name: chronyd
    enabled: true
- name: Postfix is enabled
  service:
    name: postfix
    enabled: true
```

## 重要

> `playbook` 中列出剧和任务的顺序是重要的，因为 Ansible 按照相同的顺序运行它们。

到目前为止你看到的 `playbook` 只是示例，随着课程继续，你将看到更多关于剧和任务可以做的更复杂的示例。

## 运行 PLAYBOOKS

`ansible-playbook` 命令用于运行 `playbook`。命令在控制节点上执行，运行的 `playbook` 名称作为参数传递：

```
$[workstation ~$ ansible-playbook site.yml
```

当你运行 `playbook` 时，会生成输出显示正在执行的剧和任务。输出还会报告每个任务的结果。

以下示例显示了一个简单 `playbook` 的内容以及运行它的结果。

```
$[workstation playdemo]$ cat webserver.yml
--
- name: setup web server
  hosts: servera.lab.example.com
  tasks:
    - name: latest httpd installed
      yum:
        state: latest
        output: emitted
$[workstation playdemo]$ ansible-playbook webserver.yml
```

PLAY [play to setup web server]

TASK [Gathering Facts]

ok: [servera.lab.example.com]

TASK [latest httpd installed]

changed: [servera.lab.example.com]

PLAY RECAP

servera.lab.example.com : ok=2 changed=1 unreachable=0 failed=0

注意在 `playbook` 运行时显示每个剧和任务的 `name` 值。`Gathering Facts` 是 `setup` 模块在剧开始时自动运行的一个特殊任务（这将在课程后面介绍）。对于具有多个剧和任务的 `playbook`，设置 `name` 有助于监控 `playbook` 执行的进度。

你应该还会看到 `latest httpd installed` 任务对于 `servera.lab.example.com` 显示为 `changed`。这意味着任务更改了该主机上的某些内容以满足其规范。在这种情况下，这意味着 `httpd` 软件包可能没有安装或者不是最新版本。

通常情况下，Ansible Playbook 中的任务是幂等的（idempotent），多次运行 `playbook` 是安全的。如果受管主机已经处于正确状态，则不应进行任何更改。例如，假设再次运行上一个示例中的 `playbook`：

```
[student@workstation playdemo]$ ansible-playbook webserver.yml
```

```
PLAY [play to setup web server] *************************************************************
```

```
TASK [Gathering Facts] *********************************************************************
ok: [server.lab.example.com]
```

```
TASK [latest httpd version installed] *******************************************************
ok: [server.lab.example.com]
```

```
PLAY RECAP ***********************************************************************************
server.lab.example.com : ok=2 changed=0 unreachable=0 failed=0
```

这次所有任务都以 status `ok` 状态通过，且没有报告任何更改。

## 增加输出详细度

`ansible-playbook` 命令的默认输出不提供详细的任务执行信息。`ansible-playbook -v` 命令可以提供额外信息，最多有四个级别。

### 配置 Playbook 执行的输出详细度

| OPTION | DESCRIPTION |
| --- | --- |
| `-v` | 显示任务结果。 |
| `-vv` | 同时显示任务结果和任务配置 |
| `-vvv` | 包含有关到受管主机连接的信息 |
| `-vvvv` | 为连接插件添加额外的详细度选项，包括用于在受管主机上执行脚本的用户，以及执行了哪些脚本 |

## 语法验证

在执行 `playbook` 之前，进行验证是一项良好的习惯，可以确保其内容的语法正确。`ansible-playbook` 命令提供了一个 `--syntax-check` 选项，可以使用它来验证 `playbook` 的语法。以下示例显示了 `playbook` 的成功验证。

```
[student@workstation ~~]$$ ansible-playbook --syntax-check webserver.yml
```

```
playbook: webserver.yml
```

当语法验证失败时，会报告语法错误。输出还包含语法问题在 `playbook` 中的的大致位置。以下示例显示了 `playbook` 验证失败的情况，其中在 play 的 `name` 属性之后缺少空格分隔符。

## 第 3 章 实现 Playbooks

```
$student@Workstation ~]$ansible-playbook --syntax-check webserver.yml
```

ERROR! Syntax Error while loading YAML.

mapping values are not allowed in this context

错误似乎出现在... 第 3 行，第 8 列，但可能在文件的其他地方，取决于具体的语法问题。

出现问题的行似乎是：

+   - name:play to setup web server

hosts: servera.lab.example.com

^ 在这里

## 执行干运行 (Dry Run)

你可以使用 `-C` 选项对 `playbook` 执行进行干运行。这会让 Ansible 显示如果执行 `playbook` 将发生哪些更改，但不会对受管主机进行任何实际更改。

以下示例显示了一个包含单个任务的 `playbook`，干运行安装最新版本的 `http` 包。注意，干运行报告了任务将影响受管主机的更改。

```
$student@Workstation ~]$ansible-playbook -C webserver.yml
```
