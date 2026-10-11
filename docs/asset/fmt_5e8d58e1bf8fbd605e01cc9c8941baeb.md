
![](img/e610c7a095fcd2c0c411ff707edde0b3_74_0.png)

> 它们在小空间内的游戏或流媒体体验可能非常好。

例如游戏或视频流媒体，以及带有过滤不适合儿童内容过滤器的家长控制功能。路由器的价格还包含了华硕 AiProtection 安全功能，该功能可以监控您的网络以防止来自恶意网站或下载文件的攻击。

### 结论

开发者：华硕 (ASUS) 价格：£720

>> 8/10

## 网件 Orbi 四频 WiFi Gen 6E

我们要的是 Wi-Fi，而不是去西班牙度假！

### 规格参数

- Wi-Fi：四频 Wi-Fi 6, 2.4GHz, 5GHz, 6GHz
- 速度：10Gbps+
- CPU：四核 2.0GHz
- 内存：1GB
- SSD：512MB
- 波束成形：隐式/用于显式支持
- 以太网 (WAN)：2.5Gb, 1Gb
- 卫星：2.5Gb, 3Gb
- 尺寸：280 x 184 x 836mm

网件 Orbi 四频 WiFi 6E 可能适用于拥有 6E 支持设备的大型家庭。它非常昂贵，这意味着你可以充分利用所有的速度和 Wi-Fi 空间需求。然而，如果你需要空间和惊人的性能，它是值得的，因为我们在整个空间内都使用了最高 Wi-Fi 速度。

网件的智能控制 (`Smart Controls`) 和 Armour 安全功能仅是其中一角，你必须支付额外的订阅费用，这使得原本就昂贵的价格更加昂贵。主路由器现在可以使用 2.4GHz、两个频段和 6.0GHz 路由器提供四频 Wi-Fi 6。

Orbi 至少在设置主路由简单方面值得赞誉，它可以自动将智能手机或平板电脑连接到新的 Orbi 网络，并将卫星连接到您的网络。不过，应用程序并不是没有额外功能，它创建了一个简单的网络，合并了

![](img/e610c7a095fcd2c0c411ff707edde0b3_74_1.png)

> 经典的网件设计适用于任何风格。

5.0GHz 和 6.0GHz 网络将您的计算机和移动设备连接到最快的可用带宽。我们在 30 分钟内就完成了组网网络的搭建和运行。如果不是价格的原因，网件 Orbi 四频版的得分会更高。但如果你能负担得起，它是最强大的 Wi-Fi 6 路由器之一。

### 结论

开发者：网件 (Netgear) 价格：£1700

>> 8/10

## 管理

### 创建快速、简单且可重复的执行脚本

每个人都说 Stuart Burns 是一个 Ansible 粉丝，这与他超光速的通信无关。

都是庞大的 Ansible 粉丝。在管理 PC 时，它让生活变得简单。问题是，有许多东西要学；所以，让我们来看一些不需要即时大量学习、但可以逐步成长的 Ansible 脚本。

`Ansible` 是一个开源自动化工具，以管理基础设施而闻名。通过以 YAML 文件的形式定义任务，`Ansible` 通过 `ssh` 执行这些任务，自动化如安装软件、配置服务等任务。它确保一切都完全符合你的预期，并减少错误。

但它不仅限于管理远程服务器。你可以使用 `Ansible` 配置您的本地机器并简化任务，保持服务器的一致性。它确保一切都如你所希望的那样。它有什么优势？声明式与命令式的区别……`Bash` 脚本是命令式的；告诉计算机具体做什么。

`Ansible` 是声明式的。告诉它你想要的，它会找出如何做。如果某些已经存在，它什么都不会做。这消除了大量精力并减少了错误。`Ansible` 是幂等的（idempotent），这意味着多次运行执行脚本的结果总是相同的。这对一致性是一个巨大的加，而且不必担心运行相同的脚本会搞砸。与 bash 循环不同，`Ansible` 使用简单的格式来声明你想要的，使其更容易读和写。

在开始之前，你需要安装 `Ansible`。`Ansible` 的核心是定义要执行任务的 YAML 文件。一个基础示例是快速设置环境。使用一些实用包如 `git`，`Bash` 脚本可能是这样的：

```bash
#!/bin/bash
```

### 设置 Python 环境

`hosts: localhost`

`tasks:`

- `name: 确保安装 git`
  `apt:`
    `name: git`
    `state: present`
- `name: 确保安装 curl`
  `apt:`
    `name: curl`
    `state: present`
- `name: 确保安装 http`
  `apt:`
    `name: http`
    `state: present`

### RSYNC 时间记录

大家都 `rsync` 是什么。然而，在进行复制时，缺乏对耗时的想法。我们最近添加了 `rsync` 的新开关，对操作时间做了估计。`rsync` 的 `--progress` 开关给了我们持续时间的预估。它非常有用，我们认为应该包含在标准输出中。对于简单的 `rsync` 命令，使用以下示例：

`rsync -av admin@media:/content`

这里我们列出了要执行的任务 - `'command'`：这是一个与管理器交互的 `Ansible` 模块（我们在 Ubuntu/Debian 上）。`state: present` 已安装的包。要安装执行脚本，使用 `ansible-playbook -K myplaybook.yml`

### 管理

`K` 提供了 sudo 权限。这有多简单？一旦运行它，`Ansible` 会检查包是否已经安装，如果是则跳过。这消除了冗余并确保你安装了你需要的。设置配置非常简单。例如：尊重是一个高度自定义的状态。假设你想通过 `/bashrc` 配置环境变量。`Bash` 脚本可以：

`ls -la >> /bashrc; export PATH="$PATH:/opt/bin" >> /bashrc; source ~/.bashrc`

`rsync -avz /data/files/iso/ /data --progress`

发送增量文件列表

`proxox-ve_8.2-iso`

`ubuntu-20.04.1-desktop-amd64.iso 137.8MB/s 100% (08:00:27,to3/6)`

`240.91 118MB 100% (02:05)`

![](img/e610c7a095fcd2c0c411ff707edde0b3_76_0.png)

Stuart Burns 是位于伦敦的一家世界五百强企业的系统管理员。使用 `progress` 显示了同步操作还需要多久。

### 密码实用性

```yaml
- name: 配置 Bash 设置
  hosts: localhost
- name: 向 bashrc 添加 alias
  linefile:
    line: "ls -la" >> /bashrc
    create: yes
- name: 向 bashrc 添加自定义 PATH
  linefile:
    path: /bashrc
    line: export PATH="$PATH:/opt/bin"
    create: yes
```

我认为密码管理器是一个很棒的主意。不幸的是，人们管理密码的方式存在问题。`LastPass` 和我喜欢的 `Bitwarden` 配合 `TOTP`（2FA 码）。目前密码管理器保存并自动填充 `TOTP`。这是一个糟糕的决定，削弱了任何使用者的安全立场。2FA 的整个重点在于它与你是分离的，在理想世界中无法被访问或绕过。现在，如果你的密码被黑客获取，恶人将能够冒充你，因为他们有了你的用户名、密码和代码。我有它，但这意味着你没有防御攻击的线。这是旧式的安全漏洞与便利。承认事情很难，但 `LastPass` 已经被破解 - https://bit.ly/325last 我的建议是不使用它，如果攻击者可以通过破解一个系统获取你的所有信息，这些网站就可以宣布你的信息，因为你没有采取良好的安全措施。现在是确保你在独立设备上使用密码的时候（使用著名的验证器应用）。大多数人只有备份码的物理副本作为补充。不要把它们留在笔记本的任何地方！

```yaml
- name: 更新系统包
  hosts: localhost
- name: 更新包列表
  apt:
- name: 更新所有包
  apt:
    upgrade: all
```

`Ansible` 允许你在本地 PC 上执行任务

保持你的配置

为未来的更新复用你的配置。构建整个脚本是完全可能的。而且 `Ansible` 任务非常微不足道，使用 `ChatGPT` 可以创建一个非常简单且有效的任务。你可以集成它、测试它并反复测试，它是幂等的，所以你可以根据需要多次运行，而只需正常工作

一个 `Ansible` 的 YAML 示例

www.techradar.com/linux | 2025年3月 LFXES | 17

# Intel 新一代 Arc 系列深度解析

## Xe 2: 渲染切片 (Render Slice)

对所有图形加速函数的深度微观和宏观分析

针对降低延迟、消除停顿和改进软硬件交换进行了优化

- 原生支持执行指令 (Execute instinct)
- 单核心性能显著提升
- 命令前端 (Command Front End)

### 渲染切片 (Render Slice)

原生 SIMD-512，全 4 深度 XMX
