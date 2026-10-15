
容器之间并没有真正的共享空间问题，因为文件系统的层级在它们之间共享的。在 Ubuntu 或 Debian 中设置 LAMP 栈（或带有 nginx 和 MariaDB 的 LEMP 栈）是足够的（即使手动维护数据库有点费劲）——我们将使用 Cloud-Docker 启动，这里有一些指南可以遵循，而且我们将以不同的方式安装 Nextcloud。在 Docker 中，这意味着我们的实例将是可移植的，你可以轻松地从 VPS 迁移到家庭服务器或反之亦然。我们将数据库放在容器外部（你应该认为它是一个相当易变的事物）。

如果你已经在使用旧版本的 Nextcloud，可以从容器 Web 界面进行升级。

运行 Hello World 镜像来检查其运行正常，然后运行 Nextcloud 容器：第一个开关告诉 Docker 运行容器，第二个开关告诉它将端口 80（80 端口正在运行的地方）映射到你主主机上的 8080。现在——几百毫秒后，容器就开始运行了。

此时，我们可以将 Nextcloud 连接到并将它们都放在命名卷中，这将提供可移植性。结果将可以在 `/var/lib/docker/volumes/` 目录下可用。我们还可以给容器命名：

- `docker run -d -p 8080:8080 nextcloud`
- `docker ps --name yournextcloud`

让这两个容器相互通信是棘手的，所以我们将参考此处的文档中的 Docker Compose 部分，但我们很快会回到这里。容器在停止后仍然存在。同一个容器的多个实例

![](img/2f8aba538b6f14f57de8cb694470acb2_65_1.png)

- 安装
- 当前 18.0.1（可用："stable"）
- 升级到 19.0.1
- 安装所有额外软件
- container `registry.docker.com/releases/nextcloud:19.0.1-php-apache`
- 检查预期文件
- 检查写入权限
- 创建备份
- 下载
- 验证完整性
- 解压缩
- 启用独立机模式

# 构建智能家居办公室

用令人眼花目的插件为你的 Nextcloud 增添色彩。我们是 Nextcloud 的忠实粉丝，它让 RSS 变得很棒。

![](img/2f8aba538b6f14f57de8cb694470acb2_66_0.png)

- 应用
- 活跃应用
- 已禁用应用
- 更新
- 扩展包
- 定制化
- 仪表板
- 游戏
- 预约
- 通过在线表单将预约输入你的日历

![](img/2f8aba538b6f14f57de8cb694470acb2_66_1.png)

Nextcloud 日历

特色 ★★★★

下载并分享

下载并启用

由 Collabora Productivity 特色，基于 Roman Kalitsch 和 Viktor Dubinin 的工作

AGPL 许可

![](img/2f8aba538b6f14f57de8cb694470acb2_66_2.png)

这并不是真正的空间问题，因为文件系统的层级在它们之间共享的。但自己整理一下是好的，所以检查一下你偶尔的双击并清除未使用的的，或者另一个，如果你回到了 Nextcloud 设置，然后配置这组免费的终端命令。只需要选择一个管理员密码，使用 `db` 作为数据库（Nextcloud 使用内部数据库）。
