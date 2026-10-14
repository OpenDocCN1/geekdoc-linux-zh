
root 1418 1417 1 00:22:09 ? 0:00 `webservd-wdog` -d `/sun/`

`webserver7/`

`admin-server/config` -r `/sun/webserver7` -t `/tmp`

root 1418 1417 0 10:22:09 ? 0:02 `webservd` -d `/sun/webserver/`

`admin-server/`

`config` -r `/sun/webserver7` -t `/tmp/admi`

```
```

**注意：** Web Server 进程的解释可以在第 3 章“Web Server 7.0 安装与迁移”中找到。

如果你没有看到管理实例正在运行，可以使用 `startserv` 命令启动它，如下：

```
install_dir/admin-server/bin/startserv
```

在管理服务器上运行此命令将得到类似下面的响应：

- - Sun Java System Web Server 7.0 B12/04/2006 10:15
- info: CORE3016: daemon is running as super-user
- info: CORE5076: Using [Java HotSpot(TM)] Server VM, Version 1.5.0_0 from [Sun Microsystems Inc.]
- info: WEB1000: Loading module in virtual server [admin-server]
- info: WEB1000: Loading module in virtual server [admin-server]
- info: HTTP3072: admin-port:8889 ready to accept requests
- info: CORE3274: successful startup

## 4.4.2 在类 UNIX 系统上停止

在类 UNIX 系统上，你可以使用 `stopserv` 命令停止管理实例，如下：

```
install_dir/admin-server/bin/stopserv
```

当服务器停止后，你将看到类似下面的响应：

> server has been shut down

没有办法跨多个节点集中启动/停止实例。因此，你需要通过 SSH 或 TELNET 连接到每个节点，并在每个节点上手动运行 `stopserv` 命令。

### 4.4.3 在 Windows 系统上启动和停止

在 Windows 平台上有多种停止和启动管理实例的方法。

#### 4.4.3.1 命令行方法

与类 UNIX 系统类似，在 Windows 系统上你可以直接从命令行运行启动和停止脚本，如下：

- `install_dir/admin-server/bin/startserv.bat`
- `install_dir/admin-server/bin/stopserv.bat`

#### 4.4.3.2 程序组方法

此外，安装过程会创建一个名为 Web Server 7.0 的程序组，其中分组合了若干用于与管理服务器交互的图标。该组可以在以下位置找到：

`Programs -> Sun Microsystems -> Web Server 7.0`

该程序组包含了用于启动、停止或访问管理服务器管理界面的各种图标：

- Administration Console（管理控制台）
- Start Administration Server（启动管理服务器）
- Stop Administration Server（停止管理服务器）

只需点击 Start Administration Server 图标即可启动该服务器进程。

#### 4.4.3.3 服务方法

管理服务器作为服务程序小组件运行。因此，你也可以使用服务应用程序 (`services.msc`) 直接启动和停止此服务。

## 4.5.1 管理控制台 (Administration Console)

管理控制是一个专门设计的 Web ，仅部署在管理服务器上。它由 HTML 页面、Java 页面 (JSP)、JavaScript 技术、基于核心 Java 技术的类以及基于 XML 的部署描述、各种组件的数据文件等组成。构成管理控制台的文件是私有的；管理员无需对其进行编辑。

### 4.5.1.1 访问管理控制台

管理员通过浏览器访问管理控制台。与管理控制台的通信通常通过 SSL（默认情况下）进行，但您可以在安装期间指定一个非 SSL 管理端口。以下 URL 提供了在使用默认设置时，您将如何访问管理控制台的示例：

```
https://adminhost.admindomain:8989
```
