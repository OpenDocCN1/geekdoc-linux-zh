
## 第 29 章：将 Linux 部署到云端

11. 终止实例。当你完成实例的操作后，可以通过在“实例”页面勾选实例复选框，然后选择“实例状态 -> 终止（删除）”来终止它。系统会警告你，删除实例时该实例的存储将被删除。选择“终止”以移除实例及其关联存储。

务必记住在完成后要销毁实例，否则你将继续被收取费用。

## 总结

了解云计算如何与直接在计算机硬件上安装操作系统有何不同，将帮助你适应越来越多的数据中心向云计算的转型。在本章的开始，我鼓励你尝试获取一些云镜像，将它们结合并在本地 Linux 虚拟机管理程序上启动它们，以理解云镜像是如何工作的。

之后，我介绍了 Amazon 弹性计算云（Elastic Compute Cloud）服务，如果你没有足够的计算资源，可以付费使用云存储和处理时间。

下一章将描述如何使用 Ansible 自动化向你的数据中心部署主机系统和应用程序。

## 练习

本节的练习假设你已经将主机系统设置为虚拟机管理程序（KVM 主机计算机）。你需要使用该虚拟机管理程序运行练习中创建的虚拟机。如果你遇到困难，附录 B 中提供了任务的解决方案。请记住，附录 B 中的解决方案只是完成任务的许多方法之一。

1. 创建自定义虚拟机镜像，请安装 `genisoimage`、`cloud-init`、`qemu-img` 以及 `virt-manager`、`virt-viewer` 包。
2. 从 Fedora 项目获取云镜像。
3. 使用 `qemu-img` 创建一个名为 `myvm.qcow2` 的 qcow2 格式镜像快照，稍后你可以将其和你自己的数据结合。
4. 创建名为 `meta-data` 的 cloud-init 元数据文件，将 `instance-id` 设置为 `myvm`，`local-hostname` 设置为 `myvm.example.com`。
5. 创建名为 `user-data` 的 cloud-init 用户数据文件，将默认用户密码设置为 `test`，并设置 `chpasswd` 永不过期为 `{expire: False}`。
6. 运行 `genisoimage` 命令结合 `meta-data` 和 `user-data` 文件，创建一个 `mydata.iso` 文件，稍后你可以将其与虚拟机镜像结合。
7. 使用 `virt-install` 命令将 `myvm.qcow2` 虚拟机镜像与 `mydata.iso` 镜像结合，创建一个名为 `newvm` 的新虚拟机镜像，它将在你的虚拟机管理程序上启动运行。
8. 使用 `virt-viewer` 为 `newvm` 虚拟机打开控制台。
9. 使用之前设置的 `fedora` 用户和 `test` 密码登录 `newvm` 虚拟机。

## 第 30 章：使用 Ansible 自动化应用程序和基础设施

## 本章内容

- 理解 Ansible
- 安装 Ansible
- 梳理部署步骤
- 运行即时命令（ad hoc commands）

到本书的此处，我们主要关注如何手动配置单个 Linux 系统。你已经学习了如何在运行它们的机器上直接安装软件、编辑配置文件并启动服务。虽然了解如何操作 Linux 主机是管理 Linux 系统的基础，但仅靠自己无法良好扩展。这正是 Ansible 可以派上用场的地方。

Ansible 是今天许多自动化功能之一，它将 Linux 管理工作从单系统转变为系统组。如果你将系统配置从每台机器移动到控制节点，它将用**剧本**（playbooks）取代每台机器上的 shell 用户界面，这些剧本通过网络在其他机器上运行任务。

尽管我们的重点是管理 Linux 系统，但 Ansible 也可以管理这些 Linux 系统周边的许多事务。有许多 Ansible 模块可以确保机器开机、网络设备配置正确以及远程存储可访问。

在所有小型数据中心中，了解如何自动部署和管理 Linux 系统及周边基础设施正成为一种趋势（见第 31 章“使用 Kubernetes 容器部署应用程序”）。对于基础设施和更传统的应用程序部署，Ansible 为具有 Linux 思维的管理员提供了丰富的功能集。

本章将带你了解入门 Ansible 所需的知识。随后，它将详细说明跨系统组部署应用程序，并向你展示如何通过运行即时命令来使用 Ansible。

### 理解 Ansible

Ansible 扩展而非取代了你所学的 Linux 知识。在最基础层面，Ansible 包含以下内容：

- 一种描述实现特定状态所需任务的自动化语言。这些任务被汇成剧本。
- 用于运行剧本的自动化引擎。
- 用于管理和保护剧本与其他组件的接口，通过命令和 RESTful API 实现。

通过清单（定义主机组）和剧本（定义对主机执行的操作），Ansible 以以下方式配置主机：

**简单功能配置**：你以纯文本文件创建清单和剧本，并在其中识别所需的组件。

**设置预期结果**：你在此描述的是你希望节点所处的状态资源。这种状态可以是运行中的系统、特定地址的网络接口或特定大小的磁盘分区。如果由于某种原因功能的状态发生了变化，你可以再次运行剧本以返回预期状态。

每个主机必须运行 SSH 服务，并配置允许 Ansible 从控制节点与其通信。基于密钥的身份验证允许这种操作发生，并在需要 root 权限时可以使用 sudo。由于你使用的是可能已经在主机上运行的 SSH 服务，因此无需运行额外的代理程序或配置防火墙规则即可工作。

### Ansible 的应用场景

**容器化应用**：Ansible 不仅可以部署容器化应用，但它们还可以实时响应变化并使升级变得更容易。详情请参阅 Ansible Operator 的描述（https://www.ansible.com/blog/ansible-operator）。

**网络管理**：通常需要手动执行的配置、测试、验证和增强您的网络基础设施的任务可以通过 Ansible 实现自动化。详情请参阅 Ansible 网络入门指南（https://docs.ansible.com/ansible/latest/network/getting-started/index.html#network-getting-started）。

**云环境管理**：正如同你可以将基础设施部署到裸机上一样，Ansible 也提供了为云环境配置基础设施和应用程序的工具。仅对于亚马逊 Web Services (AWS)，就有数百个 Ansible 模块可用于管理基础设施和应用程序。对于阿里云、Azure、Google 以及几十个云环境同样可用。

### 探索 Ansible 组件

当运行一个 `playbook`（剧本）时，它会作用于一个或多个目标主机（由清单/inventories 表示），并执行这些操作，称为 `play`（操作）。每个 `play` 包含一个或多个要实现的任务（tasks）。为了执行某个任务，任务会调用模块（modules），模块按照它们出现的顺序被执行。在开始使用 Ansible 之前，进一步了解这些组件将会有帮助。

#### 清单 (Inventories)

通过将你想要管理的主机系统（节点）收集到所谓的“清单”中，你可以管理具有相似特征的机器。相似性可以包括以下内容：

- 位于相似的位置
- 提供相同类型的服务
- 被分配到流程中的特定阶段，例如开发、测试、预发布和生产环境的机器组

将多个组组合在一起允许它们基于不同的属性进行分类。例如，`host1` 可能既属于一个名为 `network` 的组（基于其位置），也属于一个名为 `ftp` 的组（基于其提供的应用）。在这些清单组上运行的任务允许每个主机根据其位置分别获取网络设置，并根据其用途获取相应的应用程序。

创建清单有多种方法。你可以设置一组静态服务器，也可以创建一个系统范围。你还可以使用来自云提供商（如 Azure、AWS 和 GCP）的动态服务器列表。

使用变量（variables），你可以为清单中的一组主机分配属性。这些变量可以配置诸如主机上可用服务的端口、服务的超时值，或主机使用的服务位置（例如用于网络时间协议服务器的数据库）。

与 playbook 一样，清单可以是简单的文本文件。它们也可以通过清单脚本实现。

#### Playbooks (剧本)

Playbooks 以 YAML 格式的文件创建，它们描述了某物的最终状态。这种状态可以导致软件安装、应用配置或服务启动。它可以只关注应用本身，也可以包含该应用所在的整个环境（网络、存储、身份验证或其他功能）。

Playbooks 的设计目的是为了复用——以便稍后部署相同的组件、适配其他组件，或重新播放以恢复特定 playbook 实例的原始意图。因为 playbook 旨在复用，许多人将其保存在源码版本控制中。这样，你就可以跟踪随时间的变化，并让 playbook 易可用。

#### Plays (操作)

playbook 内部包含一个或多个 `play`。每个 `play` 都有一个目标，例如主机标识符，告诉 playbook 在哪些主机上执行操作。之后可以跟随一个远程用户，告诉 playbook 以哪个用户身份对主机进行身份验证。`play` 还可以指示在开始执行任务之前需要通过 sudo 提升权限。之后，可以有一个或多个任务来定义在主机上执行的实际活动。

#### 任务 (Tasks)

在最基础的层，每个任务运行一个或多个模块。任务提供了一种将模块与模块相关的参数和返回值关联起来的方法。

#### 模块 (Modules)

今天有数百个 Ansible 模块可用，并且不断有新的模块被创建。运行时，模块通过检查预期状态（由所提供的参数指示）来确保请求的状态实现；如果目标不在该状态，则执行需要做什么才能达到该状态。模块索引（Module Index）按类别组织模块（https://docs.ansible.com/ansible/latest/modules_by_category.html）。

模块示例包括 `yum`、`mysql_db` 和 `ipmi_power`。`yum` 模块可以从 YUM 设施安装、删除或其他管理软件包和存储库。`mysql_db` 模块允许你从主机上添加或删除 MySQL 数据库。`ipmi_power` 模块允许检查带有 IPMI 接口的计算机状态，并确保它们达到请求的状态（开启或关闭）。

条件判断可以应用于每个任务。例如，使用 `yum` 模块，你可以根据包的状态条件决定是否安装某个包。你可以说，如果包的状态已安装，则不安装该包（即使有新版本）。然而，如果你使用 `latest`，如果当前包不是最新版本，则将安装较新版本的包。

参数允许你添加信息来修改任务。例如，使用 `user` 模块时，向系统添加用户时，你可以识别用户的名称、密码、UID 和 shell。

除了设置从 playbook 执行的模块外，你还可以直接从命令行运行模块。如果你希望立即对主机执行操作，而无需运行整个 playbook，这将非常有用。例如，你可以 ping 一组主机确保它们正在运行。

大多数模块都会返回指示操作结果的值。常见的返回值包括布尔值，指示任务是否成功（https://docs.ansible.com/ansible/latest/dev_guide.html）。

#### Roles, imports 和 includes

随着你 playbook 集的增长，你可能会发现通过将 playbook 拆分为更小的部分包含 `includes` 和 `roles`。`roles` 与任务类似，但它们可以包含不仅仅是任务，例如变量和处理器（handlers）。有关使用 includes 信息，请访问 https://docs.ansible.com/ansible/latest/.html 并搜索“Creating Reusable Playbooks”。

### 逐步 Ansible 部署

为了开始使用 Ansible，我们将通过一个程序向一组主机部署服务。在安装 Ansible 后，该程序将展示如何创建部署所需的所需的清单和 playbook。

#### 先决条件

开始时，我使用了四台计算机（你可以使用虚拟机），名称如下：

- `ansible` 用作控制节点
- `host01` 第一个目标节点
- `host02` 第二个目标节点
- `host03` 第三个目标节点

然后我运行了以下步骤来准备使用这些主机：

- 在每台计算机上安装了 Fedora
- 对于三个目标节点（`host01`、`host02` 和 `host03`），我确保执行了以下操作：
    - 确保 SSH 服务正在运行并可用（必要时开启 TCP 22 端口）供 Ansible 控制节点访问。
    - 创建非 root 用户账户。稍后使用 playbook 时，使用 `--ask-become-pass` 选项提示提升权限所需的密码。
    - 为该用户设置密码。

运行 Ansible 时，我使用具有 sudo 权限的普通账户连接到每个系统，并使用 sudo 提升到 root 权限。

#### 为每个节点设置 SSH 密钥

登录控制节点 (`ansible`)，确保它可以访问你正在配置的其他三个节点。要么通过 DNS 服务器访问这些主机，要么将其添加到控制节点的 `/etc/hosts` 文件中。然后设置访问这些节点的密钥。例如：

1. 作为 root 用户，将要部署 Ansible playbook 的每个节点的 IP 地址添加到 `/etc/hosts` 文件中：

```
192.168.122.154   host01
192.168.122.94    host02
192.168.122.189   host03
```

2. 在 `ansible` 系统上生成 ssh 密钥，以便与每个主机进行密码通信。你可以作为普通用户在 `ansible` 主系统上运行此命令以及随后的 Ansible 命令：

```
$ ssh-keygen
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/joe/.ssh/id_ed25519):
<ENTER>
Created directory '/home/joe/.ssh'.
```

```
Enter passphrase (empty for no passphrase): <ENTER>
Enter same passphrase again: <ENTER>
Your identification has been saved in /home/joe/.ssh/id_ed25519
Your public key has been saved in /home/joe/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:UexjkyUSQGIxPyKu9fmNB2wJER7ka8IPyDVv5 chris@ansible
The key's randomart image is:
+----[ED25519]----+
| .O..               |
| .O+  .  O..          |
| +   + == E           |
|O+0+..* S  O         |
| =oo+=.               |
| .oo..               |
+----[SHA256]----+
```

3. 使用 `ssh-copy-id` 将您的公钥复制到每台主机上具有复制 `sudo` 权限的用户账户。以下 `for` 循环步骤将用户 joe 的密码复制到所有三个主机：

```
for i in 1 2 3; do ssh-copy-id joe@host$i; done
```

```
/usr/bin/ssh-copy-id INFO: Source of key(s) to be installed: "/home/joe/.ssh/id_ed25519.pub"
/usr/bin/ssh-copy-id INFO: attempting to log in with the new key(s), to filter out any already installed
/usr/bin/ssh-copy-id INFO: 1 key(s) remain to be installed
If you are prompted now it is to install the new keys
joe@host01's password: <password>
Number of key(s) added: 1
Now try logging into the machine, with: "ssh joe@host01"
and check to make sure only the key(s) you wanted were added.
/usr/bin/ssh-copy-id INFO: Source of key(s) to be installed: "/home/joe/.ssh/id_ed25519.pub"
/usr/bin/ssh-copy-id INFO: attempting to log in with the new key(s), to filter out any already installed
/usr/bin/ssh-copy-id INFO: 1 key(s) remain to be installed
If you are prompted now it is to install the new keys
joe@host02's password: <password> ...
```

下一步是在控制节点 (`ansible`) 上安装 ansible 软件包。从现在开始起，所有工作都将从控制节点发出。

## 安装 Ansible

Ansible 软件包适用于 RHEL、Fedora、Ubuntu 以及其他 Linux 发行版。由于 Ansible 剧本（playbooks）是从控制节点运行的，因此无需在任何目标节点上安装 Ansible 软件。

因此，首先在您想要作为控制节点的 RHEL、Fedora、Ubuntu 或其他系统上安装 `ansible` 软件包。该控制节点只需能够连接到运行在您要部署的主机上的 SSH 服务即可。

通过以下方式之一安装 `ansible` 软件包（或轻量级安装 `ansible-core`）：

- **RHEL**
  ```
  # dnf install ansible -y
  ```

- **Fedora**
  ```
  # dnf install ansible -y
  ```

- **Ubuntu**
  ```
  # sudo apt install ansible
  ```

安装 Ansible 后，您就可以开始构建清单（inventory），它为您将运行的剧本提供目标。

## 创建清单

简单的清单可以由代表剧本目标的名称以及与该名称关联的主机系统组成。要开始操作，这里有一个包含三组静态主机的清单示例：

```
[ws]
host01
host02
host03
```

```
[newyork]
host01
```

```
[houston]
host02
host03
```
