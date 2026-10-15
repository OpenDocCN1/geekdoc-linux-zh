
```yaml
users:
  - default:
    - name: William B. Smith
      gecos:
        - primary-group: smith
    - sudo:(ALL) NOPASSWD:ALL
    - lock-password: true
    - ssh-authorized-keys:
      - ssh-rsa AAAAB3Nza1yc2EAAAAAAQABABAQAMDzdq6gDHueWz71rUIWjx/RRJY4
        rr/YJ3B3J17Y2d9c7lnznq2P24/2BSbJ3J7KyWymOcweWebh3JrHBAYEQX
        QQKYJUB2E2R6mkmrJ6QBxbz+V*baINC
        YYWwegSUQCNrJ43GV6uSOHdfH77vctJyoOvOt0979Y63UceEybropNrzreG58JBFWPM
        RPMWG8fJMFMW6Wg8J5dHOMEC1IIIdhpovYQvbTnsn/
        ST07zWWy6kfJ0zsvddDCDyChhnPCIKIdifuh/
        JnknZ9qxfeQ+S3+UI2Inw6910fnNpeJPFr+Bjwkwrc58C6uowE5Ngguu7G
```

从前面的信息中，你可以看到 `wmith` 是默认用户。`gecos` 条目通常是用户的全名，用于 `/etc/passwd` 文件的第五字段。该用户的密码已被锁定。然而，来自 host2.example.com 账户的 `ssh-rsa` 条目被提供在该用户的 `ssh-authorized-keys` 下。

# 第 28 章：将 Linux 部署到云

## 使用 OpenStack 部署云镜像

通过 **OpenStack**，你将获得一个不断发展的平台，用于管理你的物理云计算基础设施以及运行在其上的虚拟系统。OpenStack 允许你部署自己的私有云或将其作为公有云提供给世界。

我并不是让你自己搭建 OpenStack 云，而是将向你展示如何使用 OpenStack Dashboard（OpenStack 控制面板）来部署虚拟机。如果你想亲自尝试，可以通过以下方式获取 OpenStack：

- **Linux 发行版**：Fedora、Ubuntu 和 CentOS 都有免费的 OpenStack 版本，你可以自行进行配置。红帽企业 Linux（Red Hat Enterprise Linux）是通过订阅提供的 OpenStack 版本。它的设置起来比较复杂。某些 OpenStack 的一体化方案可以在单台机器上运行，但我认为使用三台物理机器会有更好的体验：一个控制节点和两个虚拟宿主机（hypervisors）。

- **公共 OpenStack 云**：你可以根据不同的成本尝试公共 OpenStack 云。OpenStack 项目网站（http://www.openstack.org/marketplace/public-clouds/）提供了公共 OpenStack 云的列表。

我的第一点是帮助你能够在计算机上实现你想要的功能时，在云中运行 Linux 系统。我的第二点是展示云提供商的 Web 界面（如 OpenStack Dashboard）如何极大简化我们在本章早期使用 `cloud-init` 手动进行的云配置。

### 从 OpenStack Dashboard 开始

我将从一个已经就绪的 OpenStack 设置开始。OpenStack 环境管理员为我创建了一个名为 `cnexus-test-project` 的项目，并允许用户账户 `cnegus` 访问该项目。以下是我的计划：

- **配置网络**。如果我们设置一个路由器并将我的计算机物理连接到该路由器上，我将设置一个虚拟网络。该虚拟网络将包含一组地址，这些地址通过 DHCP 分发给我的虚拟机。

- **配置虚拟机**。我将逐步完成配置和部署几台虚拟机的过程。

本次演示使用的 OpenStack 版本是红帽 OpenStack Platform（RHEL-OSP）。然而，在任何 OpenStack 环境中的体验都是相似的。下一节将为你展示如何开始配置网络。

### 配置你的 OpenStack 虚拟网络

1. 登录 OpenStack。使用 OpenStack 管理员分配给你的用户名和密码，通过浏览器登录 OpenStack Dashboard。你应该看到一个 Overview（概览）屏幕，类似于图 28.2 所示：

#### 图 28.2

登录 OpenStack Dashboard。

![](img/cc1e2b1a5739a47bac1a4c7cfac7c1a6_781_0.png)

2. 创建网络。要创建网络，从 Overview 屏幕左侧列选择 Networks（网络）。在出现的 Networks 屏幕上，按如下步骤创建网络（括号内是我使用的示例）：

    - a. 选择 Create Network（创建网络）按钮。

    - b. 在 Subnet（子网）选项卡上，输入子网名称（`mysub01`）、网络地址（`192.168.100.0/24`）、IP 版本（IPv4）和网关 IP（`192.168.100.1`）。不要勾选 Gateway（网关）。

    - c. 在 Subnet Detail（子网详情）选项卡上，在 Allocation Pool（分配池）框中输入逗号分隔的 IP 地址范围。例如，我选择了 `192.168.100.10,192.168.100.50`，向客户端分发从 `192.168.100.10` 到 `192.168.100.50` 的 IP 地址范围。从你的 OpenStack 云管理员或公共 DNS 服务器（如 Google 的 `8.8.8.8` 或 `8.8.4.4`）获取名称建议。

    - e. 选择 Create（创建）以创建新网络。新网络出现在 Networks 屏幕上。

3. 创建路由器。为了让虚拟机能够访问互联网，你需要标识一个路由器，在一个接口上连接到你的私有网络，在另一个接口上连接公共互联网。操作方法如下：

    - a. 从左侧列选择 Routers（路由器）。

    - b. 点击 Create Router（创建路由器）按钮。

    - c. 输入路由器名称（`myrouter1`）并点击 Create Router（创建路由器）。

    - d. 选择 Gateway（网关）按钮。

    - e. 在 Set Gateway（设置网关）屏幕上，点击 External Network（外部网络）框并从可用的外部网络中选择。保持 Router Name（路由器名称）和 Router ID（路由器 ID）不变。点击 Set Gateway（设置网关）。新路由器出现在屏幕上。

4. 将你的网络连接到外部路由器。从 Routers 屏幕（你应该在该屏幕），选择你刚刚创建的路由器名称（`myrouter1`）。

    - a. 从 Router Details（路由器详情）屏幕选择 Add Interface（添加接口）按钮。

    - b. 从 Add Interface（添加接口）屏幕选择 subnet 框并选择可用子网（`192.168.100.0/24`）。保持 Router Name 和 Router ID 不变。

    - c. Add Interface（添加接口）。

5. 查看你的网络。点击网络名称。

将节将如何配置你的虚拟机。下一节将展示如何为你的虚拟机配置网络。

### 通过 ssh 访问虚拟机

将你的公钥注入到运行中的虚拟机后，它已准备好让你通过 `ssh` 登录。然而，在此之前，你必须执行以下步骤：

- 1. **添加浮动 IP 地址**。从 OpenStack Dashboard 中，选择 instances（实例），在包含实例的条目上点击 More（更多），并点击 Associate Floating IP（关联浮动 IP）。

点击 IP 地址框旁边的加号 (+)，选择一个有可用浮动 IP 的池，并点击“分配 IP”。分配的地址应出现在 IP 地址字段中。选择要关联的端口并点击“关联”。

2. **使用 ssh 访问实例。** 从已分配该浮动地址网络的 Linux 系统，使用 `ssh` 命令进行登录。假设你的密钥 `.pem` 文件名为 `mycloud`，实例上的默认用户为 `cloud-user`，且 IP 地址为 `10.10.10.100`，你可以输入以下内容进行登录：

```bash
# ssh -i mycloud.pem cloud-user@10.10.10.100
```

现在你应该能够无密码直接登录了。如需对系统进行管理，可以使用默认用户执行 `sudo`。

## 使用 Amazon EC2 部署云镜像

Amazon 弹性计算云（Amazon EC2）是一个特别适用于按需付费云计算的云平台。与 OpenStack 类似，它允许你从预配置的机器映像中选择，并根据需要对其进行配置。
