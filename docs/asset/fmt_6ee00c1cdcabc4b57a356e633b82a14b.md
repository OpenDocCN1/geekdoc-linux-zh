
![](img/a3cb513bfd7a0b21f70c67fcaede10f6_90_0.png)

# 第 3 章 WEB 服务器 7.0 迁移

## 3.4 安装软件

| 参数 | 可能的值 | 描述 |
|---|---|---|
| `IS_ADMIN_NODE` | true 或 false | 仅适用于管理服务器和管理节点安装；对于管理命令行安装为 null。 |
| `JDK_LOCATION` |  | 此 Web 服务器使用的 JDK 路径。它要么包含系统上现有 JDK 的路径，或者在将 `USE_BUNDLED_JDK` 参数设置为 true 时则为空。 |
| `NODE_HOST` |  | 正在安装管理节点的计算机完全限定名。 |
| `NODE_SSL_PORT` | 0–65535 | 用于 SSL 通信的管理节点端口号。 |
| `REGISTER_NODE` | true 或 false | 指定管理节点实例应在安装时或稍后注册到管理服务器实例。 |
| `SELECTED_COMPONENTS` |  | 选择安装的产品组件的逗号分隔列表。 |
| `SIXTYFOURBIT_INSTALL` | true 或 false | 标识 64 位安装。 |
| `SKIP_INSTANCE_CREATION` | true 或 false | 不创建默认实例。 |
| `STARTUP_ONBOOT` | true 或 false | 系统启动时启动选项。 |
| `USE_BUNDLED_JDK` | true 或 false | 安装安装程序捆绑的 JDK；如果为 false，`JDK_LOCATION` 不能为空。 |
| `WEB_DOCROOT` |  | Web 服务器实例的主要文档目录；如果为空，则创建一个默认文档目录。 |
| `WEB_PORT` | 0–65535 | 在 HTTP 模式下运行 Web 服务器实例的有效默认端口。 |
| `WEB_SERVERNAME` |  | 正在安装管理节点的计算机完全限定名。 |
| `WEB_UID` | （仅 UNIX）运行管理服务器的有效 UNIX 用户 ID。 |  |

### 参数

| 参数 | 可能的值 | 描述 |
|---|---|---|
| `ADMIN_PORT` | 0–65535 | 用于非 SSL 通信的管理服务器端口号。 |
| `ADMIN_SSL_PORT` | 0–65535 | 用于 SSL 通信的管理服务器端口号。 |
| `ADMIN_UID` | 有效的 UNIX 用户 ID | （仅 UNIX）运行管理服务器的有效 UNIX 用户 ID。 |
| `CONFIG_NAME` | https-host.domain | Web 服务器用于创建配置、与节点关联并创建实例的默认配置名称。 |
| `currentInstall-Directory` |  | 存储安装二进制文件和其他组件的位置。 |
| `defaultInstall-Directory` | `/sun/webserver7` (Unix) `C:\Program Files\Sun\WebServer7` (Windows) | 存储安装二进制文件和其他组件的默认位置。 |
| `IS_ADMIN_NODE` | true 或 false | 仅适用于管理服务器和管理节点安装；对于管理命令行安装为 null。 |
| `JDK_LOCATION` |  | 此 Web 服务器使用的 JDK 路径。它要么包含系统上现有 JDK 的路径，或者在将 `USE_BUNDLED_JDK` 参数设置为 true 时则为空。 |
| `NODE_HOST` |  | 正在安装管理节点的计算机完全限定名。 |
| `NODE_SSL_PORT` | 0–65535 | 用于 SSL 通信的管理节点端口号。 |
| `REGISTER_NODE` | true 或 false | 指定管理节点实例应在安装时或稍后注册到管理服务器实例。 |
| `SELECTED_COMPONENTS` |  | 选择安装的产品组件的逗号分隔列表。 |
| `SIXTYFOURBIT_INSTALL` | true 或 false | 标识 64 位安装。 |
| `SKIP_INSTANCE_CREATION` | true 或 false | 不创建默认实例。 |
| `STARTUP_ONBOOT` | true 或 false | 系统启动时启动选项。 |
| `USE_BUNDLED_JDK` | true 或 false | 安装安装程序捆绑的 JDK；如果为 false，`JDK_LOCATION` 不能为空。 |
| `WEB_DOCROOT` |  | Web 服务器实例的主要文档目录；如果为空，则创建一个默认文档目录。 |
| `WEB_PORT` | 0–65535 | 在 HTTP 模式下运行 Web 服务器实例的有效默认端口。 |
| `WEB_SERVERNAME` |  | 正在安装管理节点的计算机完全限定名。 |
| `WEB_UID` | （仅 UNIX）运行管理服务器的有效 UNIX 用户 ID。 |  |

## 表 3.9 常见状态文件参数

| 参数 | 可能的值 | 描述 |
|---|---|---|
| `ADMIN_PORT` | 0–65535 | 用于非 SSL 通信的管理服务器端口号。 |
| `ADMIN_SSL_PORT` | 0–65535 | 用于 SSL 通信的管理服务器端口号。 |
| `ADMIN_UID` | 有效的 UNIX 用户 ID | （仅 UNIX）运行管理服务器的有效 UNIX 用户 ID。 |
| `CONFIG_NAME` | https-host.domain | Web 服务器用于创建配置、与节点关联并创建实例的默认配置名称。 |
| `currentInstall-Directory` |  | 存储安装二进制文件和其他组件的位置。 |
| `defaultInstall-Directory` | `/sun/webserver7` (Unix) `C:\Program Files\Sun\WebServer7` (Windows) | 存储安装二进制文件和其他组件的位置。 |
| `IS_ADMIN_NODE` | true 或 false | 仅适用于管理服务器和管理节点安装；对于管理命令行安装为 null。 |

## 表 3.9 参数

| 参数 | 可能的值 | 描述 |
|---|---|---|
| `ADMIN_PORT` | 0–65535 | 用于非 SSL 通信的管理服务器端口号。 |
| `ADMIN_SSL_PORT` | 0–65535 | 用于 SSL 通信的管理服务器端口号。 |
| `ADMIN_UID` | 有效的 UNIX 用户 ID | （仅 UNIX）运行管理服务器的有效 UNIX 用户 ID。 |
| `CONFIG_NAME` | https-host.domain | Web 服务器用于创建配置、与节点关联并创建实例的默认配置名称。 |
| `currentInstall-Directory` |  | 存储安装二进制文件和其他组件的位置。 |
| `defaultInstall-Directory` | `/sun/webserver7` (Unix) `C:\Program Files\Sun\WebServer7` (Windows) | 存储安装二进制文件和其他组件的位置。 |
| `IS_ADMIN_NODE` | true 或 false | 仅适用于管理服务器和管理节点安装；对于管理命令行安装为 null。 |

## 表 3.9 管理节点实例参数

| 参数 | 可能的值 | 描述 |
|---|---|---|
| `ADMIN_PORT` | 0–65535 | 用于非 SSL 通信的管理服务器端口号。 |
| `ADMIN_HOST` |  | 正在安装管理节点的计算机完全限定名。 |
| `_SSL_PORT` | 0–65535 | 用于 SSL 通信的管理节点端口号。 |
| `REGISTER_NODE` | true 或 false | 指定管理节点实例应在安装时或稍后注册到管理服务器实例。 |
| `SELECTED_COMPONENTS` |  | 选择安装的产品组件的逗号分隔列表。 |
| `SIXTYFOURBIT_INSTALL` | true 或 false | 标识 64 位安装。 |
| `SKIP_INSTANCE_CREATION` | true 或 false | 不创建默认实例。 |
| `STARTUP_ONBOOT` | true 或 false | 系统启动时启动选项。 |
| `USE_BUNDLED_JDK` | true 或 false | 安装安装程序捆绑的 JDK；如果为 false，`JDK_LOCATION` 不能为空。 |
| `WEB_DOCROOT` |  | Web 服务器实例的主要文档目录；如果为空，则创建一个默认文档目录。 |
| `WEB_PORT` | 0–65535 | 在 HTTP 模式下运行 Web 服务器实例的有效默认端口。 |
| `WEB_SERVERNAME` |  | 正在安装管理节点的计算机完全限定名。 |
| `WEB_UID` | （仅 UNIX）运行管理服务器的有效 UNIX 用户 ID。 |  |
