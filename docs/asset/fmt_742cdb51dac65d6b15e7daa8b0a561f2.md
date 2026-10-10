
```yaml
- name: use rpm_key in repository access
  hosts: all
  tasks:
    - name: get the GPG public key
      rpm_key:
        key: ftp://control.example.com/repo/RPM-GPG-KEY
        state: present
    - name: set up the repository client
      yum_repo:
      file: myrepo
      name: myrepo
      description: example repo
      baseurl: ftp://control.example.com/repo
      enabled: yes
      gpgcheck: yes
      state: present
```

## 管理 RHEL 订阅

在使用 `Red Hat Enterprise Linux` (`RHEL`) 时，仅使用之前描述的方法配置仓库访问是不够的。`Red Hat Enterprise Linux` 与订阅制工作，为了能够访问通过订阅权限提供的软件，你需要设置受管理系统来访问这些订阅。

> `RHEL` 和 `Ansible` 都有免费的开发者订阅。如果你想在 `RHEL` 上测试本节描述的主题，且你还没有有效的订阅，请访问 `https://developers.redhat.com` 注册并申请订阅。

要理解如何使用 `Ansible` 模块注册 `RHEL` 系统，你需要了解如何使用 `Linux` 命令行工具。当从 `Linux` 命令行管理订阅时，涉及到多个步骤。

1. 首先，你使用 `subscription-manager register` 命令提供你的 `RHEL` 凭据。例如，使用 `subscription-manager register --username=yourname --password=yourpassword`。

2. 接下来，你需要找到你的账户中有哪些可用池（pools）。池是你的账户可用的软件通道集合。使用 `subscription-manager list --available` 查看概述。

3. 现在你可以使用 `subscription-manager attach --pool=poolID` 连接到特定的池。请注意，如果你的账户中只有一个可用订阅，则不需要提供 `--pool` 参数。

4. 接下来，你需要使用 `subscription-manager repos --list` 查找你的账户还有哪些额外的可用仓库。

5. 要注册并使用额外的仓库，你使用 `subscription-manager repos --enable "repos name"`。然后你的系统就可以完全访问其订阅及相关仓库。

`Ansible` 提供了两个重要的模块：

- `redhat_subscription`: 该模块允许你在一个任务中完成订阅和注册。

- `rhsm_repository`: 该模块允许你添加订阅管理器仓库。

列表 **12-9** 显示了使用这些模块的 playbook 示例，用于完全注册一台 `RHEL 8` 机器并为受管理机器添加新仓库。请注意，此 playbook 无法直接运行，因为需要提供这些重要的额外信息。本节稍后“实现管理软件的 Playbook”章节中的练习 12-3 将引导你进入一个展示如何在生产中使用此代码的场景。

## 列表 12-9 使用 Subscription Manager 设置 Ansible

```yaml
---
  - name: use subscription manager to register and set up repos
    hosts: ansible5
    tasks:
      - name: register and subscribe ansible5
        redhat_subscription:
          username: bob@example.com
          password: verysecretpassword
          state: present
      - name: configure additional repo access
        rhsm_repository:
          name:
            - rh-gluster-3-client-for-rhel-8-x86_64-rpms
            - rhel-8-for-x86_64-appstream-debug-rpms
          state: present
```

在列表 12-9 的示例 playbook 中，你可以看到如何使用 `redhat_subscription` 和 `rhsm_repository` 模块。请注意 `redhat_subscription` 需要密码。在列表 12-9 中，用户名和密码以明文形式提供在 playbook 中。从安全角度来看，这是非常糟糕的做法。你应该使用 `Ansible Vault`。练习 12-3 将引导你完成此操作的设置。

在练习 12-2 中，你将通过引导完成设置自己的仓库并使用它的过程。该过程由两个不同的部分组成。在第一部分，你设置了一个基于 `FTP` 的仓库服务器。因为在 `Ansible` 中你经常需要配置并非主要关注的主题，所以你设置了 `FTP` 服务器并更改了它的配置。接下来，你编写第二个 playbook 来为客户端配置适当的仓库访问，并在安装一个包。

## 练习 12-2 设置仓库

1. 使用你的编辑器创建 `exercise122-server.yaml` 文件。

2. 定义设置基础 `FTP` 配置的计划。因为此时你对所有任务应该都熟悉了，所以你可以一次性输入所有任务：

```yaml
---
  - name: install, configure, start and enable FTP
    hosts: localhost
    tasks:
      - name: install FTP server
        yum:
          name: vsftpd
          state: latest
      - name: allow anonymous access to FTP
        linefile:
          path: /etc/vsftpd/vsftpd.conf
          regexp: '^anonymous_enable=NO'
          line: anonymous_enable=YES
      - name: start FTP
        service:
          name: vsftpd
          state: started
          enabled: yes
      - name: open firewall
        firewalld:
          service: ftp
          permanent: yes
          immediate: yes

handlers:
  - name: restart_ftp
    service:
      name: vsftpd
      state: restarted
```

3. 使用命令 `ansible-playbook exercise122-server.yaml` 设置。如果你没有拼写错误，就不会遇到任何问题。

4. 现在仓库服务器已经安装好了，是时候设置仓库客户端了。使用编辑器创建 `exercise122-client.yaml` 并编写以下头部：

```yaml
---
- name: configure repository
  hosts: all
  vars:
    my_package: nmap
  tasks:
```

5. 添加一个使用 `yum_repository` 模块配置新仓库的任务：

```yaml
- name: connect to example repo
  yum_repository:
    name: exercise22
    description: RH8 exercise 22
    baseurl: ftp://control.example.com/repo/
    gpgcheck: no
```

6. 设置仓库客户端后，你还需要确保客户端通过名称访问仓库服务器。添加下一个任务向 `/etc/hosts` 写入新行，以确保主机解析正确：

```yaml
- name: ensure control is resolvable
  linefile:
    path: /etc/hosts
    line: 192.168.4.200 control.example.com
    create: yes
- name: install package
  yum:
    name: "{{ my_package }}"
    state: present
```

7. 如果你使用 `package_facts` 模块，你需要在安装新包后更新它。添加以下任务来完成此：

```yaml
- name: update package facts
  package_facts:
    manager: auto
```

8. 作为最后一个任务，纯属趣味，使用 `debug` 模块结合包事实获取新安装包的信息：

```yaml
- name: show package facts for {{ my_package }}
  debug:
    var: ansible_facts.packages[my_package]
  when: my_package in ansible_facts.packages
```

9. 使用命令 `ansible-playbook exercise122-client.yaml -e my_package=redis`。没错，此命令覆盖了 playbook 中设置的 `my_package` 变量——这只是为了提醒你一下变量优先级的问题。

## 实现管理软件的 Playbook

在之前的章节中，你学习了如何使用不同的模块来管理软件。在本节中，你将在一个更高级的 playbook 示例中应用这些知识。你将在第 13 到 15 章中也会发现类似的高级示例，以便为 `EX294` 考试做好最好的准备。为了匹配考试风格的题目，示例是基于场景的，作业的格式为逐步演进的练习。与所有练习一样，这里讨论的完整剧本（playbook）可以在 `GitHub` 仓库获取：`https://github.com/sandervanugt/rhce8-book/exercise123.yaml`。

要在 `RHEL 8` 目标机器上运行此作业，你需要一个有效的 `RHEL 8` 订阅。如果你没有当前的订阅，可以从 `https://developers.redhat.com` 申请。

# 练习 12-3 配置新的 RHEL 管理节点

创建一个能够完全自动化设置新 `RHEL` 主机的剧本。请按照以下要求编写此剧本：

- 将新主机的信息添加到清单（inventory）和控制主机上的 `/etc/hosts` 文件中。

- 使用变量来处理要设置的主机名称。

- 以 `root` 用户身份连接到新主机。在运行剧本时，使用相应的选项运行，以便提示输入 `root` 密码。

- 在新主机上设置用户 `ansible`，并确保该用户是 `wheel` 组的成员。

- 同样，使用剧本为用户 `ansible` 设置密码。

- 修改 `sudoers` 文件，使用户 `ansible` 可以使用 `sudo` 运行 `root` 命令而无需输入密码。

- 自动用 `RHEL Subscription Manager` 注册主机。

- 使用 `Ansible Vault` 以安全的方式提供用户名和密码。

- 将新主机添加到 `rh-cluster-3-client-for-rhel-8-x86_64-rpms` 仓库和 `rhel-8-for-x86_64-appstream-debug-rpms` 仓库中。

- 使用标签（tags）以便运行剧本的各个部分。

1. 在控制主机上，使用 `sudo yum install sshpass` 安装 `sshpass` 包。该包允许你以非交互方式处理 `SSH` 密码，你需要它来在剧本环境中自动处理与 `SSH` 密码的操作。

2. 首先，你需要设置控制主机以包含新主机的信息。为了使此剧本具有灵活性，该剧本要求从命令行设置变量，因为这是确保变量在所有任务（plays）中都用的唯一方法。使用 `vars_prompt` 也是一种选择，但通过 `vars_prompt` 设置的变量仅适用于设置它的任务。要检查变量是否确实作为参数传递给 `ansible-playbook` 命令，使用如下 `fail` 模块来检查变量 `newhost` 和变量 `newhostip` 是否作为启动参数提供。创建一个名为 `exercise123.yaml` 的文件，如下：

```yaml
- name: add host to inventory
  hosts: localhost
  tasks:
    - fail:
      msg: "add the options -e newhost=hostname -e newhostip=ip.ad.dress and try again"
      when: (newhost is undefined) or (newhostip is undefined)
```

3. **为第一个任务编写任务。** 在这些任务中，你想要确保本地清单文件和 `/etc/hosts` 文件被修改。为了实现这一点，`lineinfile` 模块提供了很好的支持。注意第二次调用 `lineinfile` 模块时对 `line` 的使用。该行仅包含变量，因此整个变量字符串必须置于双引号之间。此外，在任务结束时，包含 `tags: addhost` 行，这使得在成功运行后，如果需要再次运行剧本，可以轻松地跳过此任务。请确保添加以下文本以完成第一个任务：

```yaml
- add new host to inventory linefile:
  path: inventory
  state: present
  line: "{{ newhost }}"
- add new host to /etc/hosts linefile:
  path: /etc/hosts
  state: present
  line: "{{ newhostip }} ({{ newhost }}"
tags: addhost
```

4. 此时，测试一切进展顺利是一个好主意。使用 `ansible-playbook -C exercise123.yaml` 并观察剧本输出。它应该会失败，因为命令行没有提供参数。使用 `ansible-playbook -C exercise123.yaml -e newhost=ansible5-e newhostip=192.168.4.205` 并再次尝试。

5. 此时第一个任务已就绪，是时候配置第二个任务了。此任务将在新主机上执行。目标主机名设置为变量 `newhost`，该变量是在运行 `ansible-playbook` 命令时定义的。同时注意 `remote_user` 和 `become` 语句必须设置，因为默认用户 `ansible` 尚未配置权限提升。按如下所示编写第二个任务的任务头部：

```yaml
- name: configure a new RHEL host
  hosts: "{{ newhost }}"
  remote_user: root
  become: false
  tasks:
```

6. 现在是为此任务添加任务以及标签了。在任务中，你需要确保用户 `ansible` 存在且是 `wheel` 组的成员。接下来，你使用 `sudo` 模块为用户 `ansible` 设置密码。这是一种粗略的方法，但它有效。在第 13 章“管理用户”中，你将学习如何以更优雅的方式实现。作为下一个任务，你使用 `lineinfile` 模块修改 `/etc/sudoers` 文件，并允许 `wheel` 组的成员提升权限。如下：

```yaml
- name: configure user
  user:
    name: ansible
    groups: wheel
    append: yes
    state: present
- name: set a password
  shell: 'echo password | passwd'
- name: enable sudo
  linefile:
    path: /etc/sudoers
    regexp: '^wheel'
    line: '^wheel ALL=(ALL) NOPWD: ALL'
```

7. 此时注册 `Ansible` 已经完成，但还缺少一个元素：还没有 `SSH` 密钥对。在第 13 章中你将学习更好的方法。现在你可以通过以下粗略的方法添加：

```yaml
- name: create SSH directory in ansible home
  file:
    path: /home/ansible/.ssh
    state: directory
- name: copy public key to remote
  copy:
    src: /home/ansible/.id_rsa.pub
    dest: /home/ansible/.ssh/authorized_keys
    owner: ansible
    group: ansible
    mode: '0600'
```

8. 此时可以测试第二个任务；使用 `ansible-playbook -C exercise123.yaml -e newhost=ansible5 -e newhostip=192.168.4.205`。注意 `-k` 使用。
