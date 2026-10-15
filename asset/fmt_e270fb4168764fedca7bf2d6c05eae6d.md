
### 3.5. 验证 `httpd` 服务的运行状态。

```
[student@server ~]$ sudo systemctl enable --now httpd
```

```
[student@server] $ systemctl is-active httpd
active
[student@server] $ systemctl is-enabled httpd
enabled
```

### 3.6. 以学生用户返回工作站机器。

```
[student@server ~]$ exit
logout
Connection to server closed.
[student@workstation ~]$
```

### 4. 从工作站测试访问 `http://server.lab.example.com` 上的默认 Web 服务器以及 `http://nserver.lab.example.com:1001` 虚拟主机。

#### 4.1. 测试访问 `http://server.lab.example.com` Web 服务器。该服务器应返回 SERVER B。

```
[student@workstation ~]$ curl http://server.lab.example.com
SERVER B
```

#### 4.2. 测试访问 `http://server.lab.example.com:1001` 虚拟主机。测试仍然失败。

```
[student@workstation ~]$ curl http://server.lab.example.com:1001
curl: (7) Failed to connect to server.lab.example.com port 1001: No route to host
```

### 5. 登录服务器以确定防火墙是否分配了正确的端口。

#### 5.1. 以学生用户登录服务器机器。

```
[student@workstation ~]$ ssh student@server
...输出省略...
[student@server ~]$
```

#### 5.2. 验证默认区域是否设置为 `public` 区域。

```
[student@server ~]$ firewall-cmd --get-default-zone
public
```

#### 5.3. 如果上一步没有返回 `public` 作为默认区域，请使用以下命令进行更正：

```
[student@server ~]$ sudo firewall-cmd --set-default-zone public
```

#### 5.4. 确定 `public` 网络区域中列出的开放端口。

```
[student@server ~]$ sudo firewall-cmd --permanent --zone=public --list-all
[sudo] password for student: student
public
target: default
icmp-block-inversion: no
interfaces:
sources:
services: cockpit dhcpv6-client ssh
ports:
protocols:
forward: yes
masquerade: no
forward-ports:
source-ports:
icmp-blocks:
```

### 6. 将 `1001/TCP` 添加到 `public` 网络区域的永久配置中。验证你的配置。

#### 6.1. 为 `public` 网络区域添加 `1001/tcp`。

```
[student@server ~]$ sudo firewall-cmd --permanent --zone=public \
--add-port=1001/tcp
success
```

#### 6.2. 重载防火墙配置。

```
[student@server ~]$ sudo firewall-cmd --reload
success
```

#### 6.3. 验证你的配置。

```
[student@server ~]$ sudo firewall-cmd --permanent --zone=public --list-all
public
target: default
icmp-block-inversion: no
interfaces:
sources:
services: cockpit dhcpv6-client ssh
ports: 1001/tcp
protocols:
forward: yes
masquerade: no
forward-ports:
source-ports:
icmp-blocks:
```

#### 6.4. 以学生用户返回工作站机器。

```
[student@server ~]$ exit
logout
Connection to server closed.
[student@workstation ~]$
```

### 7. 从工作站测试访问 `http://server.lab.example.com` 上的默认 Web 服务器以及 `http://nserver.lab.example.com:1001` 虚拟主机。

#### 7.1. 测试访问 `http://server.lab.example.com` Web 服务器。该服务器应返回 SERVER B。

```
[student@workstation ~]$ curl http://server.lab.example.com
SERVER B
```

#### 7.2. 测试访问 `http://server.lab.example.com:1001` 虚拟主机。测试仍然失败。

```
[student@workstation ~]$ curl http://server.lab.example.com:1001
curl: (7) Failed to connect to server.lab.example.com port 1001: No route to host
```

# 使用图形界面安装 RHEL

当从二进制 DVD 或启动 ISO 启动系统时，Anaconda 会作为一个图形化应用程序启动。

在“WELCOME TO RED HAT ENTERPRISE LINUX 9”界面，选择安装期间使用的语言并点击“继续”按钮。此按钮还会设置安装后的系统默认语言。单个用户可以在安装后选择偏好的语言。

Anaconda 会显示“安装摘要”，这是在开始安装之前自定义参数的核心界面。

![](img/2eff90170b8c94cce3a908ab927e38c2_304_0.png)

在此窗口中，可以按任意顺序选择图标来配置安装参数。选择某项以查看或编辑。在任何项目中，点击“完成”即可返回当前屏幕。

Anaconda 用三角形警告符号和消息标记项目。屏幕底部的橙色状态栏提醒您在安装开始前完成所需信息。

根据需要完成以下操作：

- **键盘：** 添加额外的键盘布局。
- **语言支持：** 选择要安装的额外语言。
- **时间与日期：** 通过点击交互式地图或从列表中选择来选择系统位置。在使用网络时间协议 `NTP` 时指定本地时区。
- **连接到 Red Hat：** 使用您的 Red Hat 账户注册系统并选择系统用途。系统用途允许注册过程自动为系统附加最合适的订阅。您必须首先通过**网络与主机名**连接到网络以注册系统。
- **安装源：** 提供 Anaconda 安装所需的软件包源包位置。当使用二进制文件时，安装源字段已指向 DVD。
- **软件选择：** 选择要安装的元素并添加任何额外的插件。**最小化安装**将仅向 Red Hat Enterprise Linux 安装基本软件包。
- **安装目标：** 选择包含 Red Hat Enterprise Linux 安装内容的分区。要完成此操作，管理员必须理解分区方案和文件选择标准。“自动分区”默认按钮将使用所有可用空间分配所选设备。
- **KDUMP：** 内核转储 `kdump` 会收集内核崩溃时系统状态的信息。Red Hat 工程师通过分析 `kdump` 来识别崩溃原因。使用此 Anaconda 工具启用或禁用 `kdump`。
- **网络与主机名：** 检测到的网络将连接在列表中。选择一个连接以显示其详情。默认情况下，Anaconda会自动激活网络。点击**配置**按钮配置所选的网络连接。
- **安全配置：** 通过激活安全配置，Anaconda 在安装期间应用由配置定义的限制和建议。
- **Root 密码：** 安装程序提示设置 `root` 密码。在定义 **root** 密码之前，安装过程的最后阶段将不会继续。
- **创建用户：** 创建非 `root` 账户。创建本地用户是一项推荐做法。您也可以在安装完成后创建账户。

> 在设置 `root` 密码时，Red Hat Enterprise Linux 9 启用了一个锁定 `root` 用户访问系统的选项。它还启用了基于密码的 `root` SSH 访问。

完成安装并解决所有警告后，点击**开始**按钮。点击**退出**按钮将中止安装且不对系统进行任何更改。
