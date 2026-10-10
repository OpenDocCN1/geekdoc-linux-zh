

## 缺陷（BUGS）

目前未发现。

## 另请参阅

(1), (5)

## 作者

Andreas Boe <>

## servertool

### 名称

servertool - 为开发人员提供易于使用的接口，以注册、注销、启动和关闭持久服务器。

### 概要

```
servertool -ORBInitialPort naserverport [ 选项 ] [ 命令 ]
```

*选项*
命令行选项。参见“选项”。

命令
命令行命令。参见“命令”。

### 描述

**servertool** 命令为开发人员提供了命令行接口，用于注册、注销、启动和关闭持久服务器。通过命令行命令，您可以获取有关服务器的各种统计信息。参见“命令”。

### 选项

-ORBInitialHost naserverhost
此选项是必需的。它指定运行 na 服务器并监听传入请求的主机。**naserverhost** 值 st 指定 **orb** 正在运行并监听请求的端口。当未指定此选项时，**naserverport** 的值默认为 **localhost**。如果 **orbd** 和 **servertool** 在不同的机器上运行，则 st 指定运行 **orbd** 的主机的 na 或 IP 地址。

> *注意：* 在 Oracle Solaris 上，st 成为 root 用户才能在 1024 以下的端口启动进程。Oracle 建议 **naserverport** 值使用大于或等于 1024 的端口号。

-Option
将 **option** 传递给 Java 虚拟机，其中 **option** 是 Java 应用程序启动器参考页中描述的选项之一。例如，**-J-Xms48m** 将启动 mory 设置为 48 MB。参见 (1)。

### 命令

您可以在不带命令行命令的情况下启动 **servertool** 命令。

如果您在启动 **servertool** 时未指定命令，则命令行工具会显示 **servertool** 提示符，您可以在此输入命令：**servertool** >。

如果您在启动 **servertool** 时指定了命令，则 Java IDL 服务器工具将启动、执行该命令并退出。

```
register -server server-id -classna -classpath classpath-to-server [ -applicationNa application-na -args args-to-server -vmargs flags-for-JVM ]
```

向对象请求代理守护程序 (ORBD) 注册一个新的持久服务器。如果服务器尚未注册，则对其进行注册并激活。此命令会在由 **-server** 选项标识的服务器的 **main** 类中调用安装 thod。安装 thod st 为 **public static void install(org.omg.CORBA.ORB)**。安装 thod 是可选的，允许开发人员提供自己的服务器安装行为，例如创建数据库模式。

```
unregister -servid server-id | -applicationNa application-na
```

使用其服务器 ID 或其应用程序 ID 和应用程序 na，从 ORBD 中注销服务器。此命令会在由 **-server** 选项标识的服务器的 **main** 类中调用卸载 thod。**uninstall** thod st 为 **public static void uninstall(org.omg.CORBA.ORB)**。**uninstall** thod 是可选的，允许开发人员提供自己的服务器卸载行为，例如撤销 **install** thod 的行为。

```
getserverid -applicationNa application-na
```
返回与 **application-na** 值对应的服务器 ID。

```
list
```
列出所有已注册到 ORBD 的持久服务器的信息。

```
listappnas
```
列出当前已注册到 ORBD 的所有服务器的应用程序 nas。

```
listactive
```
列出所有由 ORBD 启动且当前正在运行的持久服务器的信息。

```
locate -servid server-id | -applicationNa application-na [ -endpointType endpointType ]
```
查找已注册服务器创建的所有 ORB 中特定类型的所有端点（端口）。如果服务器尚未运行，则对其进行激活。如果未指定 **endpointType** 值，则返回与服务器中每个 ORB 关联的普通/未保护端点。

```
locatepororb -servid server-id | -applicationNa application-na [ -orbid ORB-na ]
```
查找已注册服务器的特定对象请求代理 (ORB) 注册的所有端点（端口）。如果服务器尚未运行，则对其进行激活。如果未指定 **orbid**，则将 **orbid** 的默认值  分配给 **orbid**。如果任何 ORB 创建时 **orbid** 为空字符串，则返回其注册的所有端口。

```
orlist -servid server-id | -applicationNa application-na
```
列出服务器上定义的 ORB 的 **ORBId**。**ORBId** 是服务器创建的 ORB 的字符串 na。如果服务器尚未运行，则对其进行激活。

`shutdown` *-serverid* *server-id* *-* *-applicationNa* *application-na*
关闭已注册到 ORBD 的活动服务器。在执行此命令期间，还会调用由 **-serverid** 或 **-applicationNa** 参数指定的类中定义的 **shutdown** thod，以关闭服务器进程。

`startup` *-serverid* *server-id* *-* *-applicationNa* *application-na*
启动或激活已注册到 ORBD 的服务器。如果服务器未运行，则此命令启动该服务器。如果服务器已在运行，则显示一个错误 ssage。

`help`
列出通过 **servertool** 命令可用的所有服务器命令。

`quit`
退出 **servertool** 命令。

## 另请参阅

+   (1)

## SESS_ID

### 名称

`sess_id` - SSL/TLS 会话处理工具

### 概要

```
openssl sess_id [-inform PEM|DER] [-outform PEM|DER] [-in fileina] [-out fileina] [-text] [-noout] [-context ID]
```

### 描述

**sess_id** 处理 SSL 会话结构的编码版本，并可选择以人类可读格式打印 SSL 会话详情（例如 SSL 会话主密钥）。由于这是一种需要 so knwledge SSL protcol 知识才能正确使用的诊断工具，大多数用户可能不需要使用它。

**-inform DER|PEM**
指定输入格式。**DER** 选项使用包含会话详情的 ASN1 DER 编码格式。确切格式可能因版本而异。**PEM** 形式是默认格式：它由 **DER** 格式的 base64 编码以及额外的头部和尾部行组成。

**-outform DER|PEM**
指定输出格式，选项具有与 **-inform** 选项相同的 sa aning。

**-in filena**
指定要从中读取会话信息的输入 filena，默认为标准输入。

**-out filena**
指定要写入会话信息的输出 filena，如果未指定此选项，则默认为标准输出。

**-text**
除了编码版本外，还以纯文本形式打印各种公钥或私钥组件。

**-cert**
如果会话中存在证书，将使用此选项输出该证书；如果同时存在 **-text** 选项，则还会以文本形式打印。

**-noout**
此选项阻止输出会话的编码版本。

**-context ID**
此选项可以设置会话 id，使输出的会话信息使用提供的 ID。ID 可以是任何字符字符串。通常不会使用此选项。

### 输出

典型输出：

```
SSL-Session: Protocol : TLSv1 Cipher : 0016 Session-ID:
871E62626C554CE95488823752CBD5F36 73A3EF3DCE9C67BD916C809914B40ED Session-ID-ctx: 01000000 Master-Key: A7CEFC571974BE02CAC305269DC59F76E
A9F0B180CB6642697A68251F2D2BB57E 51DBBB4C7885573192AE9AEE220FACD Key-Arg :
None Start Ti: 948459261 Tiout : 300 (sec) Verify return code 0 (ok)
```

下面更详细地描述这些内容。

- **Protocol**
  这是正在使用的协议，TLSv1、SSLv3 或 SSLv2。
- **Cipher**
  使用的密码，这是实际的原始 SSL 或 TLS 密码代码，更多信息请参见 SSL 或 TLS 规范。
- **Session-ID**
  十六进制格式的 ssl 会话 ID。
- **Session-ID-ctx**
  十六进制格式的会话 ID 上下文。
- **Master-Key**
  这是 ssl 会话主密钥。
- **Key-Arg**
  密钥参数，这仅用于 ssl v2。
- **Start Ti**
  这是会话启动 ti，表示为标准 Unix 格式的整数。
- **Tiout**
  以秒为单位的 tiout。
- **Verify return code**
  这是验证 ssl 客户端证书时的返回代码。

