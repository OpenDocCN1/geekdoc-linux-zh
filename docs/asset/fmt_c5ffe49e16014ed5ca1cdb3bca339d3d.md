
`protonvpn`

0 upgraded, 0 newly installed, 1 to remove and 567 not upgraded.

After this operation, 9,216 B disk space will be freed.

Do you want to continue? [Y/n]

```

这可以用于推荐将以某种方式安装的包，例如，由于某种原因（稍后会讨论）。总之，依赖求解器将利用数据作为洞察来搜索可选配置。

要删除与包相关的所有信息，我们可以使用 `dpkg -P package` 清除包，或使用合适的清除指令。这将彻底清除包以及客户端信息，并且由于使用了合适的指令，也会清除配置状态。

### `dpkg -r Debian-cd`
### `dpkg -P Debian-cd`

注意！鉴于清除的权威性，请谨慎执行。你将丢失与该包相关的所有内容。

Secbay 出版 | 122 | 页

## 总结

- `Debian` 包是产品应用程序的压缩记录。二分二进制包（`.deb` 文档）包含可以直接使用的记录（例如，项目或文档），而源包包含产品的源代码以及构建配对包所需的指令。
- `dpkg` 工具设计用于处理和安装 `.deb` 包，但如果它遇到阻止包安装的未满足依赖关系（缺失的库），`dpkg` 仅仅会列出这些包，因为它没有感知能力或内置逻辑来查找或处理满足这些依赖的包。
- 高级包工具 (APT)，包括 `apt` 和 `apt-get`，设计用于解决这些缺陷并自动解决 `dpkg` 的问题。
- `sources.list` 文件是定义包源的关键配置文件，了解它的布局以及如何配置它至关重要，因为没有正确定义的包源列表，APT 将无法运行。
- `Debian` 和 `Kali` 使用三个部分根据每个作品作者选择的许可来区分包。`Main`（主）包含完全符合 `Debian` 自由软件指南的所有包。`non-free`（非免费）存档不同，因为它包含了不（完全）符合这些原则的软件，但尽管可以无限制地发布。`Contrib`（贡献）是一组开源软件，如果没有某些非免费元素无法运行。
- `Kali-Rolling` 仓库 - 这是面向终端用户的主要仓库。它应该始终包含可安装的最新包。
- `Kali` 仓库从 `Git`（或 `Subversion`）仓库自动构建。

## 章节习题

1. `Debian` 包是产品应用程序的压缩记录。二分二进制包（`.deb` 文档）包含可以直接使用的记录（例如，项目或文档），而源包包含产品的源代码以及构建配对包所需的指令。
   - A. `.deb` 文件
   - B. `.exe` 文件
   - C. `.apt` 文件
   - D. `.mp4` 文件

2. APT 的缩写是什么？
   - A. 高级包工具 (Advanced Package Tool)
   - B. 高级包工具 (Advanced packet toolkit)
   - C. 自动包工具 (Automatic package management tool)
   - D. 高级包跟踪器 (Advanced packet tracer)

3. 这些是 `Kali` 仓库的类型
   - A. `main`, `security`, `update`
   - B. `main`, `contrib` 和 `non-free`
   - C. `contrib`, `security`, `free`
   - D. `update`, `security`, `non-free`

4. 哪个 `Kali` 仓库包含可安装的最新包？
   - A. `main`
   - B. `Kali rolling`
   - C. `Kali dev`
   - D. `bleeding edge`

5. 哪个 `Kali` 仓库不供公共？
   - A. `Kali rolling`
   - B. `main`
   - C. `Kali dev`
   - D. `bleeding edge`

6. 哪个 `Kali` 仓库包含未经测试或验证的包？
   - A. `Kali rolling`
   - B. `main`
   - C. `bleeding edge`
   - D. `Kali dev`

7. 哪个是开发用于克服 `apt-get` 缺陷的工具？
   - A. `apt-remove`
   - B. `apt-get-install`
   - C. `apt`
   - D. `sudo`

8. 哪个是 `Linux` 中安装包的核心工具？
   - A. `apt`
   - B. `apt-get`
   - C. `dpkg`
   - D. `dp`

9. 使用 `dpkg` 安装包的命令是什么？
   - A. `dpkg -i`
   - B. `dpkg -l`
   - C. `dpkg -o`
   - D. `dpkg-install`

10. 哪个命令在安装包时解决所有依赖关系？
    - A. `dpkg -i`
    - B. `dpkg -l`
    - C. `sudo -i`
    - D. `apt-get install`

7. 答案：C

解释：为了克服 `apt-get` 设计缺陷而开发的工具仅仅是 `apt`，它是基于 `Debian` 的系统中用于软件包包的改进型命令行界面。因此，选项 C 是正确的。

8. 答案：D

解释：`Linux` 中用于安装软件包的核心工具是 `dpkg`，它负责单个软件软件包的安装、卸载和管理。因此，选项 D 是正确的。

9. 答案：A

解释：使用 `dpkg` 安装软件包的正确命令是 `dpkg -i`，其中 `-i` 代表 install（安装）。因此，选项 A 是正确的。

10. 答案：D

解释：`apt-get install` 命令在安装软件包时会解析所有依赖关系，确保所有必要的依赖项都将与所请求的软件包一起被安装。因此，选项 D 是正确的。

# 第 6 章

# 在 `Kali Linux` 上安装 LAMP

## 6.0 在 `Kali Linux` 上安装 LAMP

LAMP 栈是一组用于创建网站和 Web 应用程序的开源软件。

LAMP 是一个缩写，这些堆栈通常包含：

- `Linux` 操作系统。
- `Apache HTTP` 服务器。
- `MySQL` 关系数据库管理系统。
- `PHP` 编程语言。

在本章中，你将学习如何安装 `apache2`、`PHP`、`MySQL` 和 `NodeJS`。你还将运行你的第一个本地 Web页面。LAMP 实际上是 `Linux`、`Apache`、`MySQL` 和 `PHP` 的缩写，即它们基本上是一组用于运行 Web 服务器的开源软件。

## 6.1 Web 服务器

使用 `HTTP` 请求来提供文件以为用户创建 Web 页面并响应请求的程序，其响应通过计算机的 `HTTP` 连接发送。Web 服务器是 Web 托管的核心。托管有许多类型，但我们主要使用：

- `Apache Web` 服务器，
- `IIS Web` 服务器，
- `Nginx Web` 服务器

## 6.2 Web 服务器的组件有哪些？

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_128_0.png)

图 44 Web 服务器

### 6.2.1 Web 2.0 的组件有哪些？

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_128_1.png)

图 45 Web 2.0

# `Secbay` 出版

Web 1.0 的特征是：

- 站点与 Web 用户之间的交互非常有限
- 门户：用户被动地接收信息
- 用户仅作为“消费者”

Web 2.0 的特征：

请记住，Web 2.0 是一个已经存在超过 15 年的术语。该术语出现于 2000 年中期。它代表了从静态网页向动态交互网站的转变，允许用户现在积极参与并提供内容。

- 由交互式数据组成
- 促进 Web 用户与站点之间的交互
- 鼓励参与、协作和信息共享
- 用户被视为“生产者”
- 丰富的媒体
- 个性化
- 社交媒体

## 6.3 安装并配置 `Apache2`

步骤 1：在左侧边栏中找到终端（terminal）。点击终端。

步骤 2：在终端中运行 `sudo apt-get update` 命令。在终端输入该命令后按回车。

步骤 3：Apache 必须安装，因为它没有预装。运行 `sudo apt-get install apache2`，通过这样做我们正在 `Kali Linux` 上安装 `apache2`。Apache2 是 `Kali` 中的软件包名称。

步骤 4：调整防火墙允许流量。

接下来，验证你的防火墙是否接受 `HTTP` 和 `HTTPS` 流量，假设你遵循了初始服务器设置说明并配置了 `UFW` 防墙。你可以通过以下操作查看 `UFW` 是否有 Apache 配置文件：

```
sudo ufw list
```

Apache Full 配置应该反映出它允许通过端口 80 和 443 访问流量。

```
sudo ufw app info "Apache Full"
```

为此配置允许传入的 `HTTP` 和 `HTTPS` 流量：

```
sudo ufw allow in "Apache Full"
```
