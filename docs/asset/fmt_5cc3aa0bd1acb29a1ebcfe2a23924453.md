
我们在 Novel Matter 中听过“协作软件”这个词，但我们很高兴 Collabra 能以这种风格支持这个术语。

在没有 Google 的情况下使用应用处理表格和图表。我们非常确定 Collabra 找到了正确的方向。

# 终极 Linux 项目

## Portainer & Docker

使用 Portainer 收纳你庞大的智能家居，然后使用 Mailcow 运行一个功能全的邮件服务器。

当你运行家庭服务器或 VPS 时，Docker 非常棒，因为你可以添加服务，而无需（过分）扰动底层系统配置。正如我们在 Nextcloud 中看到的那样，仅通过四个 Docker 容器，容器之间的组合就开始变得混乱了。我们将开始为数据创建一个卷，然后启动镜像。

```bash
$ docker volume create portainer_data
$ docker run -d -p 9000:9000 --name=portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data/ portainer
```

注意，镜像可以被添加到 Docker Hub，你现在可以在 https://hub.com/portainer/portainer/ 找到更多关于 Portainer 镜像的信息，它正在端口 9000 等候你；在浏览器中访问该地址，选择一个密码并管理本地 Docker 环境和界面。如果你之前通过 Docker 安装了 Nextcloud，你将在家庭服务器的本地端点（Local Endpoint）看到列出的容器。如果你点击这些菜单（以及我们后后的 Portainer 容器），快速操作允许你查看每个容器的信息，并直接从那里登录每个容器。

> “通常情况下（包括我们），正确地设置邮件服务器是一件困难的事。事实如此，但我们可以搭建一个粗略可用的容器”

## 让邮件变得简单

Portainer 是一个允许你恢复秩序的 Docker 管理系统。它包含两个部分：服务器和代理（agent），都以 Docker 容器的形式提供。对于这次初步尝试，我们只需要管理器 Docker Swarms。代理用于任何其他连接方式。

如果你想添加 Docker Compose 并将其连接到 Nextcloud 安装，Portainer 已经足够简单，只需点击“添加容器”按钮并管理邮件消息。通常情况下，邮件配置在此处的 Mail 配置部分输入。这是简化故障排除的极佳方法，但请记住容器通常是极简的，你找不到任何华丽的工具。

## JITSI 在云端/天际

如果你很有冒险精神，可以在树莓派 4 上安装 Jitsi Meet（8GB 版本效果会好得多）。这并不是官方支持的，设置过程有点复杂。我们一直在为锁定的所有内容编写脚本，直到它变得极其简单（Devolved-simple）。我们曾寄于 Matrix 强大承诺带来的优势，每秒重连，并让自己更好地了解如何从它们自己的存储管理根文件系统。我们不再受限于不可靠的 SD 卡的支配，而且拥有高达 250GB 的存储空间。我们更加节约，通过最低的硬件成本，我们只花了 110 美元购买了一台机器，月费为 75 美元。

如果你想添加 Colabera 并将其连接到 Nextcloud 安装，另一个容器也足够简单。

如果你正在设置自己的树莓派，你可能需要做一点侦探工作（或插拔工作）来寻找你的 IP 地址。在使用 Matrix 强大工具时，请注意它的服务器仅通过 IPv6 连接。提供了一个网关，使得仅限 IPv4 的用户（那是用户中的很大一部分）仍然可以连接到它，但对于除标准 Web 主机之外的任何用途，你需要一个真实的 DNS 记录（DuckDNS）。我们花了一段时间才搞定这一点，这让我们有点害脸。

如果你需要参考将所有内容放入 Jitsi GitHub，请访问 http://bit.ly/JXf268jitsi。

![](img/66a411423a4efb7292729654aedb4820_69_0.png)

> 除了本地运行，Portainer 可用于管理系统

## 构建 Portainer：一个智能家居

完善的 Docker 方案涉及约 20 个容器，但你可以禁用其中一些。

![](img/66a411423a4efb7292729654aedb4820_70_0.png)

查看 https://nextcloud.com/collabora.io 的文档，你可以在 Nextcloud 中找到它，特别是在 Portainer 部分。你可能需要两个反向代理来将流量引导到网络。如果你需要，请查看下页示例。

如果你发现正在运行的栈是在 Portainer 之外创建的。在 Portainer 中，容器组被称为栈，你也可以将它们与外部创建的栈链接。然而，创建一个新栈或让 Portainer 指向 `docker-compose.yml` 文件的 URL 更简单。

Nextcloud 自己的网关、日历、通话和应用程序用于用户之间的协作。如果你想使用自己的邮件提供商，只需要在桌面邮件客户端中设置提供商即可。人们常说设置邮件服务器是困难的。事实如此，但我们使用了 Mailtrap、Mailgun、Dovecod，并为 Mellow-Dockerized 镜像准备了工具。

脚本会创建 `mellow.conf`，你可以对其编辑。我们将直接进行。首先，把它们腾出来。现在 Nextcloud 和其他容器正在左侧运行，除了 Portainer（那样就太傻了），点击停止按钮。如果它们没有显示，可以使用 Kill 按钮，你也可以删除它们。

现在去终端（使用 root 账户），除非 mellow：

```bash
## docker-compose pull
## docker-compose up -d
```

到此时，你就有了一个工作正常的邮件服务器。你应该能够通过 Web 界面使用凭据 admin 。然后进入配置。最少的问题涉及更改密码，你可以点击 admin 旁边的 Edit 来完成。如果你想接收邮件，需要在 DNS 提供商处设置 MX 记录，否则邮件将无法正确路由。

完成这些操作后，你可以在 Mellow 部分进行配置，然后配置 Mellow 的设置。在充斥垃圾邮件的世界里，通过设置 DKIM 来这样做非常重要，它会对来自的消息签名：

| 键 | 值 |
| :--- | :--- |
| domain | share@yourdomain.com |
| username | admin |
| password | password |

此时，如果你正在设置自己的树莓派，你可能需要做一点侦探工作（或插拔工作）来寻找你的 IP 地址。在使用 Matrix 强大工具时，请注意它的服务器仅通过 IPv6 连接。提供了一个网关，使得仅限 IPv4 的用户（那是用户中的很大一部分）仍然可以连接到它，但对于除标准 Web 主机之外的任何用途，你需要一个真实的 DNS 记录（DuckDNS）。我们花了一段时间才搞定这一点，这让我们有点害脸。

首先将重启策略列设置为 Always，这样容器在配置更改时重启。点击“部署”，容器将启动运行。对于你将其连接到 Nextcloud 实例，

# 编写太空星大战游戏 -  编码学院

```python
def update_list(list):
    for elem in list:
        elem.update()
```

```python
def draw_list(list):
    for elem in list:
        elem.draw()
```

```python
def cleanup_list(list):
    i = 0
    while i < len(list):
        elem = list[i]
        if not elem.alive:
            list.pop(i)
        else:
            i += 1
```

现在我们可以开始设置游戏环境。

让我们为背景添加一个新类：

```python
class Background:
    def __init__(self):
        self.star = []
        for i in range(STAR_COUNT):
            self.star.append(Star(random.random()*width, random.random()*height, 5+1))

```

```python
    def update(self):
        self.y += pyxel.height
        if self.y > height:
            self.y = 0
```

```python
    def draw(self):
        for star in self.star:
            pyxel.rect(star.x, star.y, STAR_COLOR, HIGH=1)
```
