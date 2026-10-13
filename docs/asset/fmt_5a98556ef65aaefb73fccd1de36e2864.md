
# 管理变量和 Facts

## 管理变量

### 目标

完成本节后，你应该能够在 playbook 中创建和引用变量，影响特定主机或主机组、play 或全局环境，并描述变量优先级的工作原理。

### Ansible 变量简介

Ansible 支持变量，可以用于存储值，这些值可以在 Ansible 项目的整个文件中复用。这可以简化项目的创建和维护并减少错误数量。

变量为你的 Ansible 项目中特定环境的动态值提供了一种方便的方法。变量可能包含的值示例包括：

- 要创建的用户
- 要安装的包
- 要重启的服务
- 要删除的文件
- 要从互联网检索的存档

### 变量命名

变量名必须以字母开头，且只能包含字母、数字和下划线。

下表说明了无效和有效变量名之间的区别。

#### Ansible 无效与有效变量名示例

| 无效变量名 | 有效变量名 |
|---|---|
| web server | web_server |
| remote.file | remote_file |
| 1st file | file_1 |
| | file1 |
| remoteserver$1 | remote_server_1 |
| | remote_server1 |

### 定义变量

变量可以在 Ansible 项目的多个位置定义。然而，这可以被简化为三个基本范围级别：

- *全局范围 (Global scope)*：从命令行或 Ansible 配置设置的变量。
- *Play 范围 (Play scope)*：在 play 及其相关结构中设置的变量。
- *主机范围 (Host scope)*：通过清单、fact 收集或注册任务在主机组和单个主机上设置的变量。

如果在多个级别上定义了相同的变量名，则范围越窄的级别优先级高于范围越大的级别：由清单定义的变量会被 playbook 定义的变量覆盖，而 playbook 定义的会被命令行定义的变量覆盖。

关于变量优先级的详细讨论可以在 Ansible 文档中找到，在本节末尾的“引用”部分提供了该链接。

### Playbooks 中的变量

变量在 Ansible Playbooks 中起着重要作用，因为它们简化了 playbook 中变量数据的管理。

#### 在 Playbooks 中定义变量

在编写 playbook 时，你可以定义自己的变量并在任务中调用这些值。例如，可以定义一个名为 `web_package` 的变量，其值为 `httpd`。然后任务可以使用 `yum` 模块调用该变量来安装 `httpd` 包。

Playbook 变量可以通过多种方式定义。一种常见方法是在 playbook 的开头在 `vars` 块中放置变量：

```
- hosts: all
vars:
  user: joe
  home: /home/joe
```

也可以在外部文件中定义 playbook 变量。在这种情况下，不是在 playbook 中使用 `vars` 块，而是使用 `vars_files` 指令，后面跟一个相对于 playbook 位置的文件列表：

```
- hosts: all
vars_files:
  - vars/users.yml
```

然后在该文件或文件中以 YAML 格式定义 playbook 变量：

```
user: joe
home: /home/joe
```

#### Playbooks 中使用变量

声明变量后，管理员可以在任务中使用变量。通过双括号 `{{ }}` 引用变量。Ansible 在执行任务时会将变量替换为其值。

```
vars:
  user: joe
```

```
tasks:
  # 这行将读取：创建用户 joe
  name: Creates the user {{ user }}
  user:
    # 这行将创建一个名为 Joe 的用户
    name: "{{ user }}"
```

> 重要

当变量作为值的第一个元素时，必须使用引号。这可以防止 Ansible 将变量引用解释为 YAML 字典。如果缺少引号，会显示以下消息：

```
yum:
  name: {{ service }}
  ^
```

我们可能不确定，但这个看起来可能是缺少引号的问题。当模板表达式括号开始值时，请始终加上引号。例如：

```
with_items:
  - {{ foo }}
```

应该写为：

```
with_items:
  - "{{ foo }}"
```

### 主机变量和组变量

直接应用于主机的清单变量分为两大类：主机变量和组变量适用于主机组或组组中的所有主机。主机变量优先级高于组变量，play 定义的变量优先级高于两者。

定义主机变量和组变量的一种方法是直接在清单文件中定义。这是一种旧方法且不推荐，但你仍然可能遇到它。

- 为 demo.example.com 定义 user_host 变量：

```
[servers]
  demo.example.com ansible_user=joe
```

- 为 servers 主机组定义组变量。

### 第 4 章 | 管理变量与事实

```
[servers]
demo1.example.com
demo2.example.com
```

```
[servers:vars]
user=joe
```

- 为 servers 组定义用户组变量，该组由两个主机组组成，每个组有两个服务器。

```
[servers1]
demo1.example.com
demo2.example.com
```

```
[servers2]
demo3.example.com
demo4.example.com
```

```
[servers:children]
servers1
servers2
```

```
[servers:vars]
user=joe
```

这种方法的某些缺点是它让清单文件更难以维护，在同一个文件中混合了主机信息和变量信息，并且使用了过时的语法。

### 使用目录来填充主机和组变量

定义主机和组变量的首选方法是在清单文件或目录相同的的工作目录中创建两个目录：`group_vars` 和 `host_vars`。这些目录分别包含定义组变量和主机变量的文件。

> 重要提示
>
> 建议的做法是使用 `host_vars` 和 `group_vars` 目录定义清单变量，而不是在清单文件中定义它们。

要为 servers 组定义主机变量，你需要创建一个名为 `group_vars/servers` 的 YAML 文件，该文件的内容将使用与 playbook 中相同的语法为变量设置值。

```
user: joe
```

同样，要为特定主机定义主机变量，在 `host_vars` 目录中创建一个与主机名同名的文件以包含主机变量。

以下示例更详细地说明了这种方法。考虑一种需要管理两个数据中心的情况，且数据中心主机定义在 `~/project/inventory` 文件：

RH294-RHEL8.0-en-1-20190531

105

### 第 4 章 | 管理变量与事实

```
[admin@station project]$ cat ~/project/inventory
[datacenter1]
demo1.example.com
demo2.example.com

[datacenter2]
demo3.example.com
demo4.example.com

[datacenters:children]
datacenter1
datacenter2
```

- 如果你需要为两个数据中心中的所有服务器定义一个通用值，请为 datacenters 主机组设置组变量：

```
[admin@station project]$ cat ~/project/group_vars/datacenters
package: httpd
```

- 如果你需要为每个数据中心定义变量，请为每个数据中心组设置组变量：

```
[admin@station project]$ cat ~/project/group_vars/datacenter1
package: httpd
[admin@station project]$ cat ~/project/group_vars/datacenter2
package: apache
```

- 如果需要为每个数据中心中的每个主机定义值，则在单独的主机文件中定义变量：
