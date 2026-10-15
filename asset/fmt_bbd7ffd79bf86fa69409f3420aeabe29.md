
```
---
- name: stat module tests
  hosts: ansible
  tasks:
    - command: touch /tmp/statfile
    - stat:
        path: /tmp/statfile
        register: st
  - name: show current values
    debug:
      msg: current value of the st variable is {{ st }}
  - fail:
    msg: "unexpected file mode, should be set to 0640"
    when: st.stat.mode != '0640'
```

如列表 8-4 中的 playbook 输出所示，playbook 因未预期的文件模式消息而失败。还要注意列表 8-4 输出中的警告：它告诉你，对于你想要实现的操作有更好的解决方案。这种情况在很多情况下都会发生，即你选择的模块可能不是你想要执行的任务的最优解决方案。请记住：使用 `command` 模块在几乎所有情况下都有效，但通常有更好的解决方案。

## 列表 8-4 运行 `ansible-playbook` `listing83.yaml` 的结果

```
$[ansible@-]$ ansible-playbook listing83.yaml

PLAY [stat module tests]
**************************************************
****
TASK [Gathering Facts]
**************************************************
****
ok: [ansible]

TASK [command]
**************************************************
****
[WARNING]: Consider使用 state=touch 的 file 模块代替 'touch'。如果你需要，这里有实现你想要操作的更好方法。这种情况会多次发生，即你可能选择了一个并不是你想要执行的任务的最优解决方案。记住：使用 command 模块在几乎所有情况下都有效，但通常有更好的解决方案。
TASK [command]
**************************************************
****
[WARNING]: Consider使用 state=touch 的 file 模块代替 'touch'。如果你需要，这里有实现你想要操作的更好方法。这种情况会多次发生，即你可能选择了一个并不是你想要执行的任务的最优解决方案。记住：使用 command 模块在几乎所有情况下都有效，但通常有更好的解决方案。

TASK [stat]
**************************************************
****
ok: [ansible]

TASK [show current values]
**************************************************
***
ok: [ansible] => {
  "msg": "current value of the st variable is {
    'changed': False, 'stat': {'exists': True, 'path':
    '/etc/hosts', 'mode': '0644', 'isdir': False, 'ischr': False,
    'isblk': False, 'isreg': True, 'isifo': False, 'uid': 0, 'gid': 0,
    'isnk': False, 'issock': False, 'uid': False, 'dev': 1,
    'size': 158, 'inode': 1680140, 'dev': 64768, 'nlink': 1,
    'atime': 158630060.147566, 'mtime': 1536580263.0,
    'ctime': 1584959818.7039, 'user': True, 'root': True,
    'xattr': False, 'wgrp': False, 'wgrp': True, 'xgrp': False,
    'roth': False, 'isgid': False, 'blocks': 8, block_size': 4096,
    'device_type': 0, 'readable': True, 'writable': True,
    'executable': False, 'pw_name': 'root', 'gr_name': 'root',
    'checksum': '73359992eb54c156756186bdfc46f64e0d5a4aa',
    'mimetype': 'text/plain', 'charset': 'us-ascii',
    'version': '408852077', 'attributes': [], 'attr_flags': []
  },
  'failed': False
}

PLAY RECAP
********************************************************************
ansible : ok=3 changed=0
unreachable=0 failed=0 skipped=0 rescued=0
ignored=0
```

文件中的多行内容。在这种情况下，你可以使用 `blockfile` 模块。列表 8-7 提供了一个示例。

## 列表 8-7 使用 `blockfile` 操作多行文本

```
---
- name: modifying file
hosts: all
tasks:
- name: ensure /tmp/hosts
  file:
    path: /tmp/hosts
    state: touch
- name: add some lines to /tmp/hosts
  blockfile:
    path: /tmp/hosts
    block: |
      192.168.4.110 host1.example.com
      192.168.4.120 host2.example.com
    state: present
```

根据你目前所学的内容，`blockfile` 的用法应该很容易理解。只需记住在 `block:` 之后使用 `|`。该字符用于指定接下来的几行被视为行，并在行末添加换行符。或者，你可以使用 `block: >`，但这会在目标文件中添加一整长文本。

注意，当使用 `blockfile` 时，`block` 中指定的文本会带有开始和结束指示器进行复制。示例参见列表 8-8：

## 列表 8-8 `blockfile` 产生的文件修改

```
127.0.0.1  localhost localhost.localdomain localhost4
localhost4.localdomain4
:1        localhost.localdomain localhost6
localhost6.localdomain6
192.168.4.200      control.example.com,    control
192.168.4.201      ansible1.example.com  ansible1
192.168.4.202      ansible2.example.com  ansible2

# BEGIN ANSIBLE MANAGED BLOCK
192.168.4.110 host1.example.com
192.168.4.120 host2.example.com
# END ANSIBLE MANAGED BLOCK
```

## 创建和删除文件

在本章之前的示例中，你已经了如何使用 `command` 模块通过 Linux `touch` 命令创建新文件。在运行此 playbook 时，你看到了一个警告，提示你不应该这样做而应该使用 `file` 模块，这是完全正确的。

你可以使用 `file` 模块执行一些非常常见的任务：

![](img/ea4c3f03927a5fe74f47acc2107727ea_334_0.png)

- 创建新文件或目录
- 创建链接
- 删除文件
- 设置权限和所有者

列表 8-9 显示了一个示例 playbook，其中使用 `file` 模块创建一个新目录，并在该目录下创建一个空文件，随后再次使用 `file` 模块递归删除该目录。这种方法并不是很有用，但至少向你展示了 `file` 模块的一些常见用法。

## 列表 8-9 使用 `file` 模块创建和删除文件

```
---
name: using the file module
  hosts: ansible
  tasks:
    - name: create directory
      file:
        path: /newdir
        owner: ansible
        group: ansible
        mode: 770
        state: directory
    - name: create file in that directory
      file:
        path: /newdir/newfile
        state: touch
    - name: show the new file
      stat:
        path: /newdir/newfile
        register: result
    - debug:
        msg: |
          This shows that newfile was created
          "{{ result }}"
    - name: removing everything again
      file:
        path: /newdir
        state: absent
```

在列表 8-9 中，你可以看到最后一个任务被配置为删除目录。只需指定目录路径并设置 `state: absent` 即可递归删除该目录。你不需要在这里指定任何其他选项，也不需要 `recurse` 键。

## 移动文件

三个模块对于移动文件特别有用。`copy` 模块将文件从 Ansible 控制主机复制到受管机器。`fetch` 模块允许你执行相反的操作，而 `synchronize` 模块执行类似 Linux `rsync` 的任务，确保控制主机上的文件同步到受管主机上的同名文件。`copy` 和 `synchronize` 之间的主要区别是 `copy` 模块总是创建一个新文件，而 `synchronize` 模块则更新现有文件。在列表 8-10 中你可以看到这些模块是如何使用的。

## 列表 8-10 使用 Ansible 移动文件

```
---
name: file copy modules
  hosts: all
  tasks:
    - name: copy file demo
      copy:
        src: /etc/hosts
        dest: /tmp/
    - name: add some lines to /tmp/hosts
      blockfile:
        path: /tmp/hosts
        block:
          192.168.4.110 host1.example.com
          192.168.4.120 host2.example.com
        state: present
    - name: verify checksum
      stat:
        path: /tmp/hosts
        checksum_algorithm: md5
```

布尔值。Ansible 提供了几个允许更改 SELinux 配置的模块，如表 8-3 所示。

> 提示
>
> 在 Ansible 中操作 SELinux，您需要具备 SELinux 知识。这是任何想要参加 `EX294` 考试的人所需的 `RHCSA` 级别知识。本节将不会解释 SELinux 本身。有关 SELinux 的更多信息，请参阅 `Red Hat RHCSA Guide`。

### 表 8-3 管理 SELinux 变化的模块

| 模块 | 用途 |
|---|---|
| `file` | 管理文件的上下文，但不从 SELinux 策略中管理 |
| `secontext` | 管理 SELinux 策略中的文件上下文 |
| `command` | 使用 `secontext` 后需要它运行 `restorecon` 命令 |
| `selinux` | 管理当前的 SELinux 状态 |
| `boolean` | 管理 SELinux 布尔值 |

## 管理 SELinux 文件上下文

在使用 SELinux 保护文件时，需要理解的关键点是：设置在文件上的上下文类型定义了哪些进程可以处理这些文件。文件上下文类型可以直接设置在文件上，也可以设置在 SELinux 策略中。

当您操作 SELinux 时，所有属性都应设置在 SELinux 策略中。要实现这一点，您可以使用 Ansible 的 `secontext` 模块。尽管如此在策略中设置上下文类型不会自动应用到文件，您仍然需要运行 Linux `restorecon` 命令来实现；Ansible 未提供运行此命令的模块，需要使用 `command` 模块进行调用。

作为替代方案，您可以使用 `file` 模块来设置 SELinux 上下文。这种方法的缺点是上下文直接设置在文件上，而不是 SELinux 策略中。因此，如果随时从策略将默认上下文应用到文件系统，通过 Ansible `file` 模块设置的所有上下文都有被覆盖的风险。因此，在 Ansible 中管理 SELinux 上下文推荐的方法是使用 `secontext` 模块。

为了使用 Ansible `secontext` 模块和 Linux `restorecon` 命令，您还需要确保 Linux 上安装了相应的软件。该软件来自 `policycoreutils-python-utils` `RPM` 包，并不是所有安装模式都会默认安装它。

列表 8-11 显示了一个使用该模块管理 SELinux 上下文类型的示例 playbook。

## 列表 8-11 使用 `secontext` 管理 SELinux 上下文

```yaml
---
- name: show selinux
  hosts: all
tasks:
  - name: install required packages
    yum:
      name: policycoreutils-python-utils
      state: present
  - name: create testfile
    file:
      name: /tmp/selinux
      state: touch
  - name: set selinux context
    secontext:
      target: /tmp/selinux
      setype: http_sys_content_t
      state: present
notify:
  - run restorecon
handlers:
  - name: restorecon
    command: restorecon -v /tmp/selinux
```

在列表 8-11 的示例 playbook 中，首先安装所需的软件包。接下来，使用 `file` 模块创建一个测试文件；在下一个任务中使用 `secontext` 命令将新上下文写入策略。如果执行成功，该任务将触发处理器，使用 `command` 模块运行 Linux `restorecon` 命令。

不要忘记：只有当触发处理器的任务产生“已更改（`changed`）”状态时，处理器才会运行。如果当前状态已符合目标状态，则不会应用任何更改，处理器也不会运行！

> 考试提示
>
> 考试任务可能不会具体到要求您使用 SELinux 更改上下文。您可能只需要配置一个带有 `ondefaultroot` 的服务，这意味着 SELinux 将拒绝访问该服务。因此在 `EX294` 考试中，对于所有任务，您都应该问自己该任务是否需要从 SELinux 级别进行更改。

## 应用通用 SELinux 管理任务

还有一些额外的模块可用。`selinux` 模块允许您将 SELinux 的当前设置为 `permissive`（宽容）、`enforcing`（强制）或 `disabled`（禁用）。`boolean` 模块允许您使用布尔值轻松地启用或禁用 SELinux 中的功能。列表 8-12 显示了一个同时使用这些模块布尔值的 playbook 示例。

## 列表 8-12 修改 SELinux 状态和布尔值
