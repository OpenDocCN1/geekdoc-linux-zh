
手动检查 Web 应用或 CMS 上的版本

查看 `robots.txt`、`sitemap.xml`、`.git` 目录

对参数和表单进行手动模糊 (`fuzzing`)

手动测试允许更深入的洞察，通常能发现扫描无法无法的业务逻辑漏洞或缺陷。

# 使用 Exploit-DB 和 SearchSploit 进行漏洞利用

一旦识别漏洞，下一步就是寻找合适的利用程序。`Exploit-DB` 和 `SearchSploit` 是实现此目的的重要资源。

## Exploit-DB

`Exploit-DB` 是利用代码和漏洞研究的公共存档。它包含了针对以下内容的：

- Web 应用
- 本地和远程漏洞
- 权限提升
- 硬件/固件

你可以使用关键词、`CVE` 编号或软件版本搜索利用程序。

## SearchSploit

`SearchSploit` 是 `Exploit-DB` 存档的离线命令行界面，随 Kali Linux 预。

### 使用示例

#### 1. 搜索软件

```bash
searchsploit vsftpd
```

#### 2. 使用 CVE 搜索

```bash
searchsploit CVE-2017-0144
```

#### 3. 镜像利用程序

```bash
searchsploit -m linux/local/37292.c
```

#### 4. 更新漏洞数据库

```bash
searchsploit -u
```

该工具在实战中极其有用，特别是在没有互联网访问的隔离环境中。

# 使用 Metasploit 框架进行利用

`Metasploit Framework` 是渗透测试人员和道德黑客工具库中最强大、最广泛使用的工具之一。它提供了一个全面的环境，用于跨广泛系统的漏洞发现、利用和后渗透利用。作为一个开源项目，`Metasploit` 集成了各种利用程序、载荷、编码器和辅助模块，以实现有效且灵活的渗透测试。

在本章中，我们将深入探索 `Metasploit Framework`，包括其架构、选择利用程序和载荷的过程、使用 `Meterpreter` 进行后渗透、编写自定义利用程序以及在受害系统中维持持久化。

## Metasploit 架构概述

`Metasploit Framework` 遵循模块化架构，使其具有适应性和扩展性。在 `Metasploit` 内部交互的核心组件包括：

### 1. 核心 Core

`Metasploit` 的核心模块负责管理框架的内部操作，包括处理用户输入、管理利用程序和载荷以及处理攻击。它是整合其他其他模块的基础。

### 2. 模块 Modules

`Metasploit` 的强大在于其丰富的模块集合，使渗透测试人员能够执行攻击、收集信息并执行后渗透任务。`Metasploit` 中的模块分类如下：

- **Exploits 利用程序**：设计用于利用目标系统漏洞的代码。
- **Payloads 载荷**：在成功利用后运行在目标系统上的程序或命令。
- **Encoders 编码器**：用于修改载荷以规避病毒和其他安全措施检测的工具。
- **Post-exploitation 后渗透**：在成功利用后使用的模块，用于维持持久化或提升权限等任务。
- **Auxiliary 辅助**：用于扫描、枚举和其他侦察活动的非利用类模块。

### 3. 数据库 Database

`Metasploit` 使用数据库存储有关目标、漏洞和会话的信息。这使得渗透测试过程的跟踪和管理更容易。

### 4. Meterpreter

`Meterpreter` shell 是一种强大且动态扩展的载荷，有助于后渗透活动。它完全在内存中运行，留下极少的痕迹，并为进一步的利用和持久化提供广泛的功能。

### 5. 接口 Interfaces

可以通过多种接口访问 `Metasploit`：

- **msconsole**：命令行界面 `CLI`，提供对 `Metasploit Framework` 功能的完全访问。
- **msfvenom**：用于创建自定义载荷并对其编码的命令行工具。
- **Web Interface Web界面**：允许通过浏览器远程访问 `Metasploit` 以方便使用。
- **API**：允许将 `Metasploit` 集成到其他工具系统中。

### 6. 社区和文档 Community and Documentation

`Metasploit` 拥有庞社区和丰富的文档，使得渗透测试人员更容易学习、贡献并有效使用该框架。

## 利用程序和载荷选择

### 1. 选择正确的利用程序

利用目标的第一步是选择正确的利用程序。这取决于多个因素：

- 目标操作系统 `OS`：利用程序必须针对特定的 `OS` 设计，例如 `Windows`、`Linux`。
- 软件漏洞：利用程序通常针对特定的软件版本。
- 可利用条件：需要满足某些条件，例如目标系统可达、受影响端口已开启且目标应用程序处于可利用状态。

`Metasploit` 提供了一种使用 `search` 命令搜索和选择利用程序的简易方法：

```bash
msf > search vsftpd
```

该命令搜索任何与 `vsftpd` 相关的利用程序并显示可用模块。

#### 示例：利用程序选择

如果你的目标是受漏洞的 `MS08-067` 一个旧的 `Microsoft Windows` 漏洞，以下命令将选择相关的利用程序：

```bash
msf > use exploit/windows/smb/ms08_067_netapi
```

### 2. 选择正确的载荷

选择利用程序后，下一步是选择成功后运行在目标系统上的载荷。`Metasploit` 中的载荷可以是交互式 `shell`、反向 `shell` 或 `Meterpreter` 会话。

载荷的选择取决于攻击目标：

- **Reverse Shells 反向 shell**：连接回攻击者的机器，提供命令 `shell`。
- **Bind Shells 绑定 shell**：在目标系统上开启监听端口供攻击者连接。
- **Meterpreter**：这是最先进且最常用的载荷，提供了完整的后渗透能力。

查看所选利用程序的可用载荷：

```bash
msf > show payloads
```

例如，在选择 `MS08-067` 利用程序后，你可以选择 `Meterpreter` 载荷：

```bash
msf > set PAYLOAD windows/meterpreter/reverse_tcp
```

这配置利用程序使用 `Meterpreter` 反向 `shell` 载荷。

## Meterpreter Shell 使用与后渗透利用

`Meterpreter` 是一种复杂且多功能的载荷，可方便各种后渗透测试活动。一旦与目标系统建立成功连接，就会启动 `Meterpreter` shell，并提供各种命令和功能。

### 1. 基础 Meterpreter 命令

- `sysinfo`: 显示基本系统信息 `操作系统、架构等`。
- `getuid`: 返回当前运行 `Meterpreter` 的用户账户。
- `ps`: 列出目标系统上运行的进程。
- `shell`: 进入目标系统的标准命令 `shell`。
- `upload`: 将文件从攻击者系统上传到目标系统。
- `download`: 将文件从目标系统下载到攻击者系统。
- `keyscan_start`: 开始在目标系统上记录按键记录。
- `screenshot`: 截取目标系统的桌面截图。
- `hashdump`: 从目标系统转储密码哈希值。

### 2. 后渗透任务

`Meterpreter` 提供了强大的后渗透能力，用于进一步攻破系统：

- **权限提升 Privilege Escalation**：如果攻击者获得了低权限 `shell`，他们可以尝试利用已知漏洞或使用本地漏洞等技术将权限提升到管理员/`root` 级别。
- **跳转 Pivoting**：如果受害系统具有对其他机器的网络访问权限，跳转技术允许攻击者访问之前无法到达的系统。
- **持久化 Persistence**：可以使用 `Meterpreter` 安装后门，以便在系统重启或清理后保持对系统的持续访问。

### 3. 会话管理

`Metasploit` 可以同时管理多个 `Meterpreter` 会话。例如：

```
msf > sessions -i 1
```

此命令连接到会话 `1`，允许你与受攻击的目标进行交互。

# 创建和修改自定义漏洞利用

`Metasploit` 提供了一个灵活的框架，用于为特定目标创建自定义的漏洞利用。在处理零日漏洞或公共利用无法按预期工作时，这种方法特别有用。

### 1. 创建自定义漏洞利用

自定义利用通常用 `Metasploit` 使用的 `Ruby` 语言编写。要创建一个自定义利用，你需要定义几个组件：

- **载荷 Payload**：成功利用后在目标机器上运行的恶意代码。
- **利用代码 Exploit Code**：触发漏洞的代码。
- **目标 Target**：被攻击的特定系统或配置。

创建一个自定义漏洞利用的示例：
