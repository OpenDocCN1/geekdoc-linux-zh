
# Ansible Playbook 中的循环

在 Ansible playbook 中，循环（loops）为通过 OLAM 自动化 Oracle Linux 环境提供了灵活性和效率。用户可以在 playbook 中定义字典（dictionaries）并使用循环语句。字典就像书，所有的基础设施或应用程序都在列表中，可以用于定义自动化中的变量。这允许为循环中的每个项执行一组任务，减少了重复代码的需求，并使 playbook 更加简洁易于管理。

例如，如果你想在一组 Oracle Linux 服务器上安装多个软件包而不使用循环，你将需要为每个包和服务器编写单独的任务，导致代码冗余。然而，通过在 OLAM 中使用循环，你可以定义一个包列表和一个服务器列表并对它们进行迭代，在单个任务中在每个服务器上安装软件包。

在本示例中，我们将首先定义 playbook（剧本）的名称和目标主机，这会使用 `hosts` 指令。我们还将把 `become` 设置为 `true`，这意味着 playbook 将以管理员权限运行。

```yaml
name: Change User Permissions
hosts: server_group
become: true
vars:
  target_users:
    - user1
    - user2
tasks:
  - name: Change user permissions
    file:
      path: /home/{{ item }}/documents
      owner: {{ item }}
      group: {{ item }}
      mode: "0755"
    with_items: "{{ target_users }}"
```

接下来，我们定义了一个变量 `target_users`，它包含一个我们想要更改权限的用户列表。在这种情况下，我们使用 `user1` 和 `user2` 作为目标用户。

`tasks` 部分包含一个名为 `Change user permissions` 的任务。该任务使用 `file` 模块来更改指定目录的所有者、组和模式。

使用 `with_items` 循环来遍历 `target_users` 列表。循环的每次迭代都会将 `item` 变量设置为从列表中使用的当前用户。然后该变量被用于 `file` 模块的 `path`、`owner` 和 `group` 参数。

通过这种方式，playbook 将为 `target_users` 列表中的每个用户执行任务，有效地更改用户和文件夹的权限。

```yaml
name: Change user permissions
hosts: all
tasks:
  - name: Change permissions for users
    file:
      path: /path/to/directory
      owner: "{{ item }}"
      state: directory
loop: "{{ users }}"
```

在前面的示例中，`file` 模块用于将指定目录的所有者更改为 `users` 列表中的每个用户。`item` 变量代表循环中的当前用户。

通过遵循这些步骤，你可以编写并执行 Ansible playbook OLAM，以更改不同服务器和描述目录的用户权限。这将允许你自动化该过程，并确保多个系统之间权限的一致性，以及在管理多个环境的许多其他方面。

## 如何操作...

1. 你需要先编写 playbook；为了简单起见，我使用了演示项目：

```bash
[opc@olam-test]$ cd /var/lib/aws/
[opc@olam-test]$ ls
awfilfo projects syslog uwsgi.stats venv
[opc@olam-test]$ cd projects/
[opc@olam-test]$ cd demo_bundle/
[opc@olam-demo-bundled]$ ls
httpd.yaml permissions.yaml yum_update.yaml
[opc@olam-test-demo-bundled]$$
[opc@olam-demo-bundled]$ sudo vi change_permissions.yaml
```

```yaml
- name: Change file permissions
hosts: olam-test-1, olam-test-2
become: true
tasks:
  - name: Change permissions for /tmp/changedir
    file:
      path: /tmp/changedir
      owner: root
      group: root
      mode: "0755"
```

```bash
[opc@olam-target-2]$ ls -ltr
total 0
drwxr-xr-x. 2 root root 6 Oct 18 11:53 1151 unified-monitoring-agent
drwxr-xr-x. 2 root root opc 6 Oct 26 15:27 changedir
[opc@olam-target-2]$
```

2. playbook 的每个组件都被拆分成一个部分，以简化循环拓扑。包含以下组件：

- `name`: 这是 playbook 的名称。
- `hosts`: `true`: 这指定了执行 playbook 的目标服务器。你可以直接在 playbook 中定义主机，也可以使用清单文件（inventory file）。
- `become`: `true`: 这允许 playbook 以提升权限运行。
- `tasks`: 该部分包含要执行的任务列表。
- `name`: 这是任务的描述。
- `file`: 该模块用于更改目录的权限。
- `path`: 这是想要更改权限的目录路径。
- `owner`: 此参数指定了要更改的所有用户名。在示例中，我们使用了 `item` 变量，它代表循环中的当前用户。
- `state`: `directory`: 确保路径是一个目录。

![](img/110fa0d6324f0893fff03cee6394144d_453_0.png)

与任何 Linux 发行版一样，每个云服务提供商（CSP）都有自己的版本或 Linux 平台选择。例如，AWS 拥有 Amazon Linux 2 (AL2)，Azure 提供与任何基于 RHEL 或 Ubuntu 的系统的兼容性，而 Oracle 显然拥有 Oracle Linux。Ubuntu 与 Oracle Linux、AL2 等之间有许多差异，但我们不是来讨论这些差异的。最终，所有的 CSP 都可以运行 Linux 发行版，但并非所有的版本都针对 Oracle Linux 进行了优化。对于 AWS 和 Azure，你可以选择从 Oracle 购买自己的支持（BYOS，支持包括补丁、升级和操作系统支持），或者在没有技术支持的情况下免费使用这些服务。在 OCI Premier 中，支持是免费提供的。下面的图显示了主要的 CSP 及其对 Oracle Linux 的不同采用情况。

![](img/110fa0d6324f0893fff03cee6394144d_454_0.png)

图 13.2 – 云选项

谁是最公平的？让我们来看看 AWS 内部提供了哪些 Linux 发行版。我们将简要介绍 AWS EC2 Image Builder，以可视化 Linux 在 AWS 任何环境及之外的多功能性。这将在本章稍后的部分，在“使用 VirtualBox 将虚拟机跳跃到 OCI”的配方中用到。

## 准备工作

我们首先需要一个 AWS 账户，无论是个人的还是通过你的组织；只要你有正确的权限来访问账户并构建基础设施，这并不重要。在这种情况下，我选择了 Root 用户，因为这是我的个人账户，我拥有这些权限。

## 登录

![](img/110fa0d6324f0893fff03cee6394144d_455_0.png)

图 13.3 – Root 登录

在输入用户类型后，你需要提供密码并通过身份验证选项继续。我启用了多因素身份验证 (MFA)，强烈建议使用这种方法来保护你的账户。如果启用了 MFA，你接下来将按照图所示获取该代码。注意，还有其他两种双重验证选项，但使用 Google Authenticator 是最佳实践。不过，人们可以使用任何应用，例如 Microsoft、RSA 等。

## Google Authenticator

Amazon Web Services: jonathansIPhone@@772550...

704 642

图 13.4 – MFA
