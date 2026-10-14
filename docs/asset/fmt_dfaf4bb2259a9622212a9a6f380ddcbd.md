
基于 Web 的管理控制台还允许管理员同时管理多个 Web 应用程序。图 10.15 显示了管理员如何一起启用、禁用或删除 Web 应用程序。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_470_0.png)

图 10.15 管理控制台—Web应用程序的组操作

### 10.5.4.2 命令行部署

Web 服务器的主要管理命令行界面——`wadm`——提供了以下子命令来支持 Java Web应用程序管理：

- `add-webapp`
- `disable-webapp`
- `enable-webapp`
- `list-webapps`
- `remove-webapp`

以下 shell 模式示例显示了如何使用命令行界面使用某些命令来部署和卸载 Java Web应用程序：

```
wadm> list-webapps --verbose --all --config=test --vs=test
uri enabled
/simple true
wadm> add-webapp --description="JSTL Sample Application" --config=test
--vs=test --uri=jst/c:/sun/webserver7/samples/java/webapps/jst/
webapps-jst.war
CLI201 Command 'add-webapp' ran successfully
wadm> list-webapps --verbose --all --config=test --vs=test
uri enabled
/simple true
/jst true
wadm> remove-webapp --config=test --vs=test --uri=/simple
CLI201 Command 'remove-webapp' ran successfully
wadm> list-webapps --config=test --vs=test --verbose --all
uri enabled
/jst true
wadm>
wadm> deploy-config test
CLI201 Command 'deploy-config' ran successfully
```

与基于 Web 的界面不同，`wadm` 子命令不支持通过单个命令对启用、禁用和删除多个 Web 应用程序进行组操作。

> 注意：在 shell 模式下使用 `wadm` 时，文件路径（即使在 Windows 上使用 `wadm`）始终使用 UNIX 风格的正斜杠 (`/`) 指定，而不是反斜杠 (`\`)。

### 10.5.4.3 自动部署

Web 服务器支持从指定目录快速、迭代地部署 Web 应用程序。从指定目录快速、迭代部署 Web 应用程序的功能都包括“已包”格式（`.war` 文件）和“已解包”格式（文件系统中的目录）。Web Server 7.0 Update 3 是第一个支持 Java 应用程序自动部署的发布版本。用于自动部署 Java 应用程序的指定目录是 `instance/auto-deploy`。向该目录添加 Java 应用程序会导致其部署到所有活动虚拟服务器。从该目录删除 Java 应用程序会导致其从活动虚拟服务器中卸载。在自动部署期间，Web 服务器使用文件名或目录名来确定部署上下文路径。

## 第10章 通过 Java 提供动态内容

在以下阶段：

* 服务器启动
* 动态重新配置

Web 服务器可以配置为定期检查其 `auto-deploy` 目录的添加/删除，并在运行的服务器中反映这些更改。`dynamic-reload-interval`（见10.5.9，“动态配置Web应用程序”）控制服务器检查的频率。

表 10.9 自动应用程序的上下文路径

| 文件/目录名称 | 格式 | 上下文路径 |
|---|---|---|
| simple | 已解包 (目录) | /simple |
| hello_world.war | 已包 (归档) | /hello_world |
| tax-planner | 已解包 (目录) | /tax_planner |
| 100examples.war | 已包 (归档) | /100 |

与之前的部署方法（见“Web部署”和“命令行部署”章节）不同，自动部署（或自动部署）不需要管理服务器运行。

要自动部署封装为 Web 归文件（`.war` 文件）的 Java 应用程序，只需将 `.war` 文件复制到服务器的 `auto-deploy` 目录，如下所示：

```
C:\Sun\WebServer7> copy samples\java\webapps\jst1\webapps-jst.war https-test\auto-deploy
file(s) copied.
C:\Sun\WebServer7>https-test\bin\startserver.bat
Sun System Web Server 7.0 U13 B06/16/2008 11:32
info: CORES076: Using [HotSpot(TM)] Server VM, Version 1.5.0_05 from [MicroSystems Inc.]
info: WEB0100: Loading module in virtual server [test] at [webapps-jst1]
info: HTTP3072: http-listener-1: http://test:9000 ready to accept requests
info: CORES3274: successful server startup
```

> 注意：粗体字体说明了 Web 服务器如何使用 `.war` 文件名作为部署的上下文路径。

现在可以通过浏览器访问自动部署的应用程序，如图 10.16 所示。

之前的示例演示了 Web 服务器如何在启动期间自动部署 `.war` 文件。以下示例演示了通过将 Web 应用程序的内容解包到实例的 `auto-deploy` 子目录后，动态重新配置运行的服务器来自动部署 Java 应用程序：

```
C:\Sun\WebServer7\https-test\auto-deploy>mkdir simple
C:\Sun\WebServer7\https-test\auto-deploy>cd simple
```

## 第 17 章 通过 Java 提供动态内容

```
C:\Sun\WebServer7\https-test\auto-deploy\simple -jar C:\nWebServer7\samples\java\simple\webapps-simple.war
C:\Sun\WebServer7-https-test\bin\reconfig.bat
info (4092): CORE3276: Installing a new configuration
info (4092): WEB0100: Loading web module in virtual server [test] at [/simple]
info (4092): PWC3031: Security role name tomcat used in an <auth-constraint> without being defined in a <security-role> in context [/simple]
info (4092): PWC3031: Security role name role1 used in an <auth-constraint> without being defined in a <security-role> in context [/simple]
```

**注意：** 使用粗体字体是为了了 Web 服务器如何使用目录名称作为部署应用程序的路径。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_474_0.png)

图 10.16 自动部署的 Java Web 应用程序

## 10.5 Java Web 应用程序

删除自动部署的应用程序对应的 `.war` 文件或目录将导致应用程序的卸载。在 UNIX 平台上，可以在服务器运行时执行删除操作。然而，在 Windows 平台上，你必须在删除文件/目录之前停止服务器，因为当服务器运行时删除自动部署的应用程序时，会显示类似下面的错误信息：

```
C:\SunServer7>del https-test-auto-deploy\webapps-jstl.war
C:\SunServer7>https-test-auto-deploy\webapps-jstl.war
The process cannot access the file because it is being used by another process.
```

卸载自动部署的应用程序涉及删除对应的文件/目录，如下所示（在 UNIX 平台上，可以使用 `reconfig.bat` 代替 `startserv` 从正在运行的服务器部署应用程序）：
