
### 启动 NTP 服务

- 4. 点击`ntpd`条目旁边的框，并点击工具栏上的`启动`（`Start`）。
  - 打开信息对话框，告诉`ntpd`已成功启动。
- 5. 点击`OK`关闭对话框。
- 6. 点击`保存`（`Save`）关闭对话框。
- 7. 关闭服务配置。

现在`ntpd`正在运行，你准备好启用网络时间协议了。为了同步你的系统，请遵循以下步骤：

### 配置日期与时间

- 1. 打开主菜单并选择`系统设置—日期与时间`。
  - 打开对话框提示你输入`root`密码。
- 2. 输入你的`root`密码并点击`OK`。
  - 打开日期/时间窗口，如图 29-4 所示。
- 3. 勾选`启用网络协议`（`Enable Network Protocol`）框。
- 4. 使用下拉菜单选择你的服务器。
- 5. 点击`OK`。
  - 打开服务配置窗口，如图 29-3 所示。

![](img/907133bedebb1d692bfe1e0f76996df1_215_1.png)

**图 29-4：** 日期/时间窗口。

![](img/907133bedebb1d692bfe1e0f76996df1_215_2.png)

**图 29-5：** 服务配置窗口。

## 使用 PAM 和 Kerberos 提供身份验证

如果你的本地网络不包含域控制器，`PAM`可以简化身份验证。`Kerberos`是一种使用受信第三方来验证身份验证信息的安全协议。通过`PAM`和`Kerberos`协同工作，你可以获得一个单一、安全的网络登录系统，这为你节省大量时间。

## 设置密钥发行中心

### 测试你的域（DNS）

![](img/907133bedebb1d692bfe1e0f76996df1_216_0.png)

**图 29-5：** 配置。

`Kerberos`广泛使用`DNS`。在设置`Kerberos`之前，最好确保`DNS`正在工作。验证`DNS`最简单的方法是使用一系列`ping`：

- 从每个客户端`ping`密钥发行中心。
- 从发行中心`ping`每个客户端机器。
- 每个潜在客户端应该`ping`它将访问的任何潜在客户端（通过地址）。

以下是设置密钥发行中心的方法：

1. 登录到你想作为`KDC`的计算机。
2. 打开终端并使用`su`命令赋予自己超级用户权限。
3. 插入并挂载`Fedora`发行版。
4. 移动到包含`RPM`包的目录`(/mnt/cdrom/Fedora/RPM)`并使用以下命令安装`Kerberos`包：

你的机器向另一台机器发送一条通知，要求其回传数据包。如果`DNS`服务工作正常，获取响应流看起来如下：

```bash
$ ping machinename
PING (192.168.0.2): 56 data bytes
64 bytes from 192.168.0.2: icmp_seq=0 ttl=64 time=34.83 ms
64 bytes from 192.168.0.2: icmp_seq=1 ttl=64 time=2.918 ms
2 packets transmitted, 2 packets received, rtrip min/avg/max = 2.918/18.905/34.893 ms
```

```bash
# rpm kerb5-libs-1.3.1-6.1386.rpm
# rpm kerb5-server-1.3.1-6.1386.rpm
# rpm kerb5-workstation-1.3.1-6.1386.rpm
```

## 技术：使用自定义身份验证保护大型网络

你可以手动进行所有这些更改，但为了节省时间，我们添加了一个快速脚本来更新配置文件。只有当你的`DNS`服务器正在运行且其中包含一个域名时，此工具才能生效。

该脚本会保存原始文件的副本，并使用在网络上找到的默认值来更新工作配置文件。`fixrealm`在运行时会显示其进度。

- 6. 将以下代码添加到`/tmp/fixrealm`：

```bash
#!/bin/bash

OLDDOMAIN=example.com
OLDREAL=EXAMPLE.COM
OLDKDC=kerberos.example.com

NEWDOMAIN=$($dnsdomain)
NEWREAL=$(echo $NEWDOMAIN | tr '[:lower:]' '[:upper:]')
NEWKDC=$($hostname)
```

- 10. 使用以下命令创建`KDC`数据库：

```bash
# kdb5_util -s
```

系统会提示输入`KDC`数据库主密钥（`masterkey`）。

- 11. 输入密码并按回车。
  - 系统会提示再次输入`KDC`数据库主密钥以验证输入。
- 12. 重新输入你的密码并按回车。

> 不要忘记这个密码。

- 13. 使用以下命令将你的名称添加到`KDC`数据库：

```bash
# kadmin.local -q addprinc username username
```

- 14. 输入你想用于登录的密码。
- 15. 在收到提示时重新输入你的密码。

`Kerberos`将验证你的用户账户的创建。

```bash
function fixup() {
  cp $1 $1.orig
  sed s/\$OLDDOMAIN/$NEWREAL/ $1.orig |
  sed s/\$OLDREAL/$NEWDOMAIN/ |
  sed s/\$OLDKDC/$NEWKDC/ > $1
}

fixup /etc/krb5.conf
fixup /var/kerberos/krb5kdc/conf
fixup /var/kerberos/krb5kdc/kadm.ac5
```

- 7. 保存文件并关闭编辑器。

在保存代码之前双双检查你的输入（我们仅因为几个拼写错误就删除了所有的`Kerberos`配置文件）。

现在，需要使用服务配置工具启动`KDC`。要启动`KDC`服务，请遵循以下步骤：

- 1. 打开主菜单并选择`Settings::Server Settings::Services`。
  - 打开一个对话框，提示输入根密码。
- 2. 输入根密码并点击`OK`。
- 3. 使用滚动条找到以下服务：
  - `krb524`
  - `krb5dc`
  - `kadmin`
- 4. 每次勾选一个服务旁边的复选框并点击`启动`（`Start`）图标。

- 8. 使用以下命令使脚本具有执行权限：

```bash
# chmod a+x /tmp/fixrealm
```

- 9. 使用以下命令运行脚本：

```bash
# /tmp/fixrealm
```

## 使用 PAM 和 Kerberos 服务身份验证

你必须在勾选每个复选框后点击“启动”图标。如果你勾选所有三个后再点击“启动”，`Fedora`只启动你最后勾选的那个。

- 2. 输入根密码并点击`OK`。

当每个服务启动时，会弹出一个对话框确认服务已成功启动。点击`OK`（弹出窗口）并启动下一个服务。

打开身份验证配置窗口。

- 3. 勾选`身份验证`（`Authentication`）选项卡。
- 4. 勾选`启用 Kerberos`（`Enable Kerberos`）框。
- 5. 配置`Kerberos`。

- 当所有三个服务启动后，点击工具栏上的`保存`（`Save`）按钮并关闭服务配置窗口。

如图 29-6 所示`Kerberos`设置对话框。

你的`KDC`可能已经运行并准备好分发票据。忘记将每个请求身份验证的用户（或程序）添加到`KDC`数据库。

![](img/907133bedebb1d692bfe1e0f76996df1_218_0.png)

跳转到“向密钥中心添加用户”获取有关向`KDC`数据库添加主体（`principals`）的详情。

## 使用 Kerberos 和 PAM 设置自动票据管理

在同步时钟、测试`DNS`并在网络上建立密钥中心（`KDC`）之后（在前面的章节中已解释过），你就可以准备配置工作流，让`PAM`管理你的`Kerberos`登录会话。

> 图 29-6：Kerberos 设置对话框。

要设置`Kerberos`身份验证，你需要以下两项之一：

在对话框中填写有关你的`Kerberos`领域（`realm`）的信息。

- 信任`KDC`身份验证的计算机工作组（`Kerberos`领域）
- 6. 在`Realm`字段中输入领域名称。

- 充当你的`KDC`的计算机名称
- 7. 在`KDCs`字段中输入`KDC`，后面跟一个冒号和端口号 88。

```
computername:88
```

- 8. 在`Admin Servers`（管理服务器）字段中输入`KDC`，后面跟一个冒号和端口号 749。

```
computername:749
```

按照以下步骤启用`Kerberos`身份验证：

- 1. 打开主菜单并选择`System Settings: Authentication`。
- 9. 点击`OK`关闭对话框并保存设置。
  - 打开一个对话框，提示输入根密码。
- 10. 点击`OK`关闭身份验证窗口。

## 使用自定义身份验证保护大型网络

现在你的用户账户的创建已通过`Kerberos`验证。

- 4. 在收到提示时重新输入你的密码。
