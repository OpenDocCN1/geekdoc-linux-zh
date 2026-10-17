
```
buildah commit --rm oracleinux-working-container ol-repo-sync
```

现在我们已经使用 `buildah` 创建了镜像，可以使用 `buildah` 命令检查 `ol-repo-sync`：

```
$ buildah images
```

输出看起来如下：

| REPOSITORY | TAG | IMAGE ID | CREATED | SIZE |
| :--- | :--- | :--- | :--- | :--- |
| localhost/ol-repo-sync | latest | a14 | seconds ago | 279 MB |
| localhost/ol-repo-sync | latest | b25 | 2 minutes ago | 285 MB |
| localhost/ol-repo-sync | latest | c37 | 3 minutes ago | 285 MB |

最后，`Skopeo` 还可以用于从远程仓库或本地容器存储中删除镜像。要执行此操作，只需运行以下命令：

```
skopeo delete containers-storage:pandoc:core:latest
```

# 航行 Ansible 的水域

在本章中，我们将通过几个实例教程来扩展你关于安装 Oracle Linux Automation Manager (`OLAM`)、管理其基础架构、创建剧本（playbooks）、优化这些剧本以及帮助你理解 `OLAM` 功能的知识。每个教程都将让你大开眼界，看到自动化可以实现的全部范围；从补丁到部署完全的混合云环境，`OLAM` 能够改变你对计算的思考方式，让你的思维开启一个“循环往复”的新世界。以下是自动化可以简化的极小部分的触点。

![](img/110fa0d6324f0893fff03cee6394144d_380_0.png)

在本章中，接下来的教程将涵盖 `OLAM` 平台的安装、配置和可用性：

- 安装 `OLAM`
- 快速从基础开始配置和管理 `OLAM`
- `OLAM` 不是幻想足球，但它们都使用剧本
- 控制补丁混乱
- 展望自动化之外的世界
- 设置好后一劳永逸

# 安装 OLAM

自古以来，我们人类人类一直试图让事情变得更简单、更快、更高效。然而，我确定我们大多数人人都听过父母说：“永远不要走捷径”，或者“我小时候小的时候，我必须在雪天里单着一条腿走上坡去学校，来回都是如此。”这些轶事从未改变；随着我们演进到父母的年龄，并试图将我们的智慧传给下一代。那么，如果我告诉你你既可以拥有蛋糕又可以吃掉它呢？自动化是计算的演进和重复任务的自动化。现在，我们不能自动化一切，某些任务并不值得投入自动化的精力，因为它们不可重复的，或者因素的变化到了自动化会破坏流程的程度。

自动化的字典定义是“应用技术、程序、机器人技术或过程，以最少的人为输入来实现结果”。注意“过程”——我们改变、执行或更改结果输出的过程。自动化就是这种过程的变化。我们可以自动化应用程序的安装，例如安装 Microsoft Office 或反病毒软件；自从计算世界的开始起，我们就在自动化这些过程了。现在，我们将自动化推下一个水平。例如 `Ansible Tower`，Red Hat 版本的自动化。`Ansible` 和 `OLAM` 都是基于 `AWX` 构建的，`AWX` 是一个强大且现代的 Web UI 和 API，允许你管理组织的 `Ansible` 剧本、清单、密钥库（vault）和凭据。通过 `AWX`，你可以简化自动化流程并简化基础设施管理任务，所有这一切通过单一、易于使用的界面完成。例如，假设一位大学科学教授每周都必须做准备；实验室有 50 名学生，每个人都需要一个虚拟实验室来参与。教授不想坐在那里每周重建一次实验室环境。使用 `Ansible`，可以汇编一个剧本（不是足球剧本，而是大纲和功能需求）来自动化该实验室环境的创建。通过创建该剧本，工程师可以更改几个变量来改变虚拟机的数量、内存、vCPU 或任何正在使用的资源或应用程序。本质上，`Ansible` 和剧本呈指数级地缩短了创建过程，使其变得可重复，并让教授免于每周重复创建。

`OLAM` 是一个自动化套件，以开源 Linux 发行版（Oracle Linux）的形式捆带，基于 `AWX` 和 `Ansible Tower`。`OLAM` 是一个可配置平台，类似于 `Ansible`，具有创建、管理和更改剧本的能力。`OLAM` 安装时带有 UI（如你在稍后的教程中看到的），还带有 CLI。UI 和 CLI 都是功能完备的，并且与 `Ansible Tower` 相同的所有细粒度，在拥有高级支持订阅的情况下可以免费使用。如图所示，`OLAM` 可用于创建剧本，以自动化多个领域内的流程，从本地虚拟化农场和 HCI 环境到应用程序部署，一直触及到多个云平台和混合云发行版。

![](img/110fa0d6324f0893fff03cee6394144d_382_0.png)

图 12.2 – 剧本层次结构

在本教程中，我们将安装 `OLAM`。与任何安装过程一样，我们需要准备一个基础环境来在上面安装应用程序——在这种情况下是 Oracle Linux 8。不过，建议你安装带有 GUI 的操作系统。我们不会详细介绍上一个教程中涵盖的内容。

## 准备工作

我们将在 Oracle Cloud Infrastructure (`OCI`) 中以虚拟机的形式安装 `OLAM`。请参阅第 3 章和第 4 章关于导航和配置 `OCI` 虚拟机的内容。我们将在以下步骤简要介绍 VM 的创建：

1. 导航到 `OCI` Instances（实例）为 `OLAM` 创建一个主机：
   - 概述
   - 实例
   - 专用主机
   - 实例池
   - 自动伸缩
   - 容量限制
2. 点击**创建实例**以创建虚拟机：
   ![](img/110fa0d6324f0893fff03cee6394144d_382_0.png)
   图 12.3 – 实例
3. 选择镜像：
   ![](img/110fa0d6324f0893fff03cee6394144d_382_0.png)
   图 12.4 – 镜像
4. 选择可用域（Availability Domain）来托管：
   图 12.5 – 可用域
5. 我们将选择 8 GB 内存和 2 个 vCPU。`OLAM` 的最低要求是 2 个 vCPU 和 4 GB 内存：
   ![](img/110fa0d6324f0893fff03cee6394144d_382_0.png)
   图 12.6 – 内存
6. 点击**形状**（Shape）来更改形状：
   图 12.7 – 形状
7. `VM.Standard.E3.FLEX` 形状允许你指定你的资源：
   图 12.8 – 形状选择
8. 我们将选择 8 GB 内存和 2 个 vCPU。
   图 12.9 – VM 资源配置
9. 在配置虚拟机资源后，你必须配置你的访问密钥（公密钥）：
   图 12.10 – SSH 密钥选择
10. 你可以创建、上传、粘贴或继续不使用密钥：

### 添加 SSH 密钥

生成 SSH 密钥对以通过安全外壳 (`SSH`) 连接到实例，或者上传您已有的公钥。

- 为我生成一个密钥对
- 上传公钥文件 (`.pub`)
- 粘贴公钥
- 无 SSH 密钥

```
ssh ubuntu@instance-202110273-1513
```

示例：`ssh-rsa AAAAB3Nza..NwaP6bPr ssh-key-2021-01-27` 查看所有支持的密钥类型

图 12.12 - 粘贴 SSH 密钥

11. 配置实例后，滚动到实例末尾，并点击“创建”：
    ![](img/110fa0d6324f0893fff03cee6394144d_387_0.png)
    图 12.13 - 虚拟机创建

```
$ ssh -i sshkey_private_lab opc193.122.148.147
The authenticity of host '193.122.148.147' (193.122.148.147) can't be established.
ED25519 fingerprint is SHA256:9fIldkd0spWZZiXIFOpJFvzktC8YBI7j61Qm64W3A.
This key is not known by any other host.
Are you sure you want to continue connecting (yes/no/[fingerprint]?) yes
Warning: Permanently added '193.122.148.147' (ED25519) to the list of known hosts.
Activate the web console with: systemctl enable --now cockpit.socket
[opc@instance-20231213-2350 ~]
```
