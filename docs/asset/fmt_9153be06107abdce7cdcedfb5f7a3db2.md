
Web Server 7.0 支持允许 Web 应用程序开发者或站点管理员强制重新加载应用程序。当启用此功能时，Web 会在每个 Web 应用程序的文档根目录下查找名为 `.reload` 的文件。服务器将重新加载任何包含 `.reload` 文件的 Web 应用程序，只要该文件自服务器上次检查该应用程序以来已更新。此功能默认是禁用的，但可以通过在 `sun-web.xml` 中设置 `reload-interval` 属性非零值来启用。

以下显示使用 `wadm` 脚本配置 Web 容器每 5 秒检查一次：

```
.servlet-container- dynamic-reload-interval=5
wadm deploy-
-containercontainer-config' 成功
```

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_484_0.png)

图 10.20 动态重配置—Java 应用程序

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_484_0.png)

## Servlet 容器

Servlet 容器是 Web Server 的一个组件，用于托管并与 servlet 交互。它控制映射到 servlet 的请求和响应。

| 属性 | 取值 | 描述 |
| :--- | :--- | :--- |
| Log Level | info, fine, warning, error |  |
| Dynamic Reload Interval | 60000 | 服务器检查应用程序的时间间隔 |
| Anonymous Role | ANYONE |  |
| Servlet Pool Size | 5 | Servlet 实例数量 |
| Dispatcher Max Depth | 100 | 嵌套请求的最大深度 |
| Allow Cross | Enabled | 是否允许跨请求 |
| Enable Cookies | Enabled |  |

图 10.21 控制台—Servlet

当发生以下情况时，服务器会动态重配置：

- 从控制台部署了配置。
- 通过使用 `wadm` 脚本部署了配置。
- 执行了 `reconfig` 命令（`reconfig.bat`）。
- 启用了非零重加载间隔且应用程序的 `.reload` 文件已更新。

在重配置期间，服务器日志指示应用程序已重新加载。以下示例展示了如何使用服务器消息识别：

启动包含两个应用程序的服务器

`C:\Sun\WebServer\test`

## 10.6 Web Server 和 NetBeans

Sun Java System Web Server 7.0U3 B06/16/2008 11:32

info: CORE 使用 [Java HotSpot(TM) Server VM, Version 1.5.0_15]

来自 [Sun Microsystems Inc.]

info: WEBO0100: 在虚拟服务器中加载模块 [/ simple

info: WEBO0100: 在虚拟服务器中加载模块 [/ WebApplication1

info: HTTP3072: http-listener-1: http://test:9000 已准备好请求

info: CORE3274: 启动成功

在不更改任何内容的情况下重配置服务器，注意没有加载相关的消息

`C:\WebServer7-https-test\bin\reconfig.bat`

info: CORE3276: 正在新配置

info: CORE3280: 新配置安装成功

修改一个应用程序的部署描述符

`C:\WebServer7\notepad-test\web-app\simple\WEB-INF\web.xml`

重配置服务器，注意指示该应用程序已重新加载的消息

`C:\WebServer7-https-test\bin\reconfig.bat`

info: CORE3276: 安装新配置

info: WEBO0100: 在虚拟服务器中加载模块 [/ simple

info: CORE3280: 新配置安装成功

### 10.6.1 为 NetBeans IDE 安装 Web Server 7.0 插件

本节简要介绍了 NetBeans IDE 本身以及用于 Java Web 应用程序和 Web Server 7.0 的 IDE 支持模块（插件）。

从 NetBeans 主页 `http://www.netbeans.org` 下载并安装 NetBeans IDE，如图 10.22 所示。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_490_0.png)

图 10.22 NetBeans 首页

启动 NetBeans IDE，并在“工具 (Tools)”菜单中选择“插件 (Plugins)”菜单项，如图 10.23 所示。

在对话框的“可用插件 (Available Plugins)”选项卡中，选择并安装“Sun Java System Web Server 7.0”插件和“Web 应用程序 (Web Applications)”插件，如图 10.24 所示。

## 10.6 Web Server 与 NetBeans

### NetBeans 6.1

| 文件 (File) | 编辑 (Edit) | 视图 (View) | 导航 (Navigate) | 源码 (Source) | 重构 (Refactor) | 构建 (Build) | 运行 (Run) | 属性 (Properties) | 工具 (Tools) | 窗口 (Window) | 帮助 (Help) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 项目 (Projects) | x | 节点 (Nodes) | 服务 (Services) | 首页 (Start Page) | x | | | | | | |
| 添加发布... (Add to Publish...) | | | | | | | | | | | | |
| 服务器 (Servers) | | | | | | | | | | | |
![](img/a3cb513bfd7a0b21f70c67fcaede10f6_491_0.png)
| 库 (Libraries) | | | | | | | | | | | | |
| Java 平台 (Java Platforms) | | | | | | | | | | | | |
| NetBeans 平台 (NetBeans Platforms) | | | | | | | | | | | | |
| 模板 (Templates) | | | | | | | | | | | | |
| Web (Web) | | | | | | | | | | | | |
| XSD 和 J2EE 架构 (XSD and J2EE Schemas) | | | | | | | | | | | | |
| 插件 (Plugins) | | | | | | | | | | | | |
| 其他 (Others) | | | | | | | | | | | | |

增强结构化文档标题...

关于增强可见性和外观的教程...

理解代码和托管代码...

使用 NetBeans IDE 6 开发 Web 应用程序...

假设项目变为现实：热点...

微软已宣布发布 NetBeans

所有新闻 >>

James 的博客：如何制作 SQL 查询...

今天，我决定写一个关于更改 MySQL 密码的提示，以防此类情况再次发生。就在今天。

APISign：回归测试确实很重要...

当你更改 API 时，必须为它设置一个截止日期。API 并不好...

连接机器人：MySQL，我们...

本教程展示了如何将 NetBeans 连接到 MySQL 数据库。它提供了关于的几个事实

# 导航器 (Navigator)

# 特色演示 (Featured Demo)

在 NetBeans IDE 中使用 EclipseLink 的 JPA 支持

| 项目 (PROJECT) | 专用模块 (EXCLUSIVE_MODULE) |
| :--- | :--- |
| 位置 (Location) | 数据项目 (Data Project) |
| 包 (Package) |  |
| <无可用视图> |  |

- 为持久化生成查询注解
- 项目具有一个持久化单元，其
- 创建持久化单元...Create Persistence Unit...)

所有演示 >>

# NetBeans IDE—菜单

| 更新 (23) | 可用插件 (115) | 已安装 (20) | 设置 (50) |
| :--- | :--- | :--- | :--- |

# 重新加载目录 (Reload Catalog)
