
### NTP 访问控制

对 NTP 服务器的访问控制由 `restrict` 指令决定。NTP 服务器可以从互联网访问，任何人都可以访问它。你可以指定访问选项和允许的主机地址。`default` 选项允许你设置一组默认选项。`noquery`, `nostrust`, `nocoper`, and `modify` 选项拒绝所有访问。`nostrust` 选项除非被明确允许，否则不会信任主机。`modify` 选项除非被明确允许，否则不会信任主机。

```
restrict default noquery, nostrust, nocoper, modify
```

### NTP 时钟支持

你还可以列出本地硬件钟的引用，并在与互联网时间服务器连接时使用该时钟。硬件钟通过前缀为 `127.127` 的 IP 地址进行引用，后跟时钟类型和实例，例如 `127.127.1.1`。本地时钟的类型为 `1`。

```
server 127.127.1.0
```

`fudge` 指令用于指定硬件钟的时间，为该时钟驱动程序传递时间参数。

# 4. 安装和更新软件

- 更新 Fedora
- 使用 PackageKit 管理包
- Fedora 软件仓库
- RPM Fusion
- YUM 配置
- 软件包类型
- RPM 软件包
- 使用 `rpm` 命令管理软件
- 源代码应用程序

# 第 1 部分：系统管理

Fedora 软件已经变得庞大且更新频繁，使用光盘作为主要的分发手段已经没有意义。相反，分发是通过在线 Fedora 软件仓库实现的。表 4-1 列出了 Fedora 软件信息和站点位置。

| 互联网站点 | 描述 |
| :--- | :--- |
| http://fedoraproject.org/get-fedora | Fedora 发行版磁盘，所有格式的下载链接 |
| http://rpmfusion.org | 用于第三方多媒体和符合 Fedora 标准的驱动软件的 RPM Fusion 仓库（Fedora 项目扩展） |
| http://fedoraproject.org/wiki/ForbiddenItems | 未包含在 Fedora 主软件仓库中的软件包。 |
| http://fedoraproject.org/wiki/Multimedia | Fedora 可用多媒体软件包信息 |

表 4-1：Fedora 软件信息与站点

### 软件仓库

你可以通过访问支持 `YUM`（Yellowdog Update, Modified）的软件仓库来向系统添加软件。此外，许多软件应用程序（特别是多媒体类）存在潜在的冲突。通过使用 Fedora，可以避免可能的法律问题。许多流行的多媒体应用程序（如视频和数字音乐软件）可以通过第三方仓库获取，并使用与用于 Fedora 赞助软件相同的 `YUM` 命令。常用的 Fedora 软件仓库列在表 4-2 中。

| 互联网站点 | 描述 |
| :--- | :--- |
| http://download.fedoraproject.com | 指向最佳可用镜像的链接 |
| http://rpmfusion.org/Configuration | 未包含在发行版中的 Fedora 应用以及其他限制。访问配置（Configuration）页面下载 YUM 配置文件。 |
| http://rpm.livna.org | RPM Livna 仓库，仅包含 dvdcss 软件包。点击链接获取 YUM 配置文件。 |
| http://get.adobe.com/flashplayer/ | Adobe 仓库，选择适用于 YUM 的以下载 Adobe YUM 配置文件。从下拉菜单中选择“YUM for Linux”。 |

表 4-2：Fedora 及符合 Fedora 标准的软件仓库

这种方法标志着思维方式的转变：不再认为大多数 Linux 是安装在几块磁盘上的，而是将磁盘仅视为一个核心，你可以像从在线仓库那样从它扩展扩展已安装的软件。现在，大多数软件都位于连接互联网的仓库中。

# 第 4 章：安装和更新软件 123

随着 `YUM` 集成到你的 Fedora 系统，你现在可以将那些软件视为当前集合的易于安装的扩展。从某种上说，依赖磁盘介质获取软件已经过时了。你可以在 Fedora 文档页上的“使用 YUM 管理软件”中找到更多关于如何在 Fedora 上使用 `YUM` 的信息：

```
http://docs.fedaproject.org/yum/en/
```
