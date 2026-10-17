
```
[+] 10.11.0.4:443 request from 10.11.0.22: Encoded stage with shikata_ga_nai

[*] 10.11.0.4:443 request from 10.11.0.22: Staging x86 payload (180854 bytes)

[*] Meterpreter session opened (10.11.0.4:49783 -> 10.11.0.22:49783)

[*] Session ID 1 (10.11.0.4:49783 -> 10.11.0.22:49783) processing AutoRunScript windows/manage/migrate

[*] Running module against CLIENT251

[*] Current server process: test.exe (7528)

[*] Spawning notepad.exe process to migrate to

[*] Migrating to 4724

[*] Successfully migrated to 4724
```

## 22.6.1.1 练习

- 1. 使用第二阶段编码器和自动运行脚本创建一个资源脚本，并将其与 `meterpreter` 载荷配合使用。

### 22.7 总结

`Metasploit Framework` 在渗透测试的几乎每一个阶段都具有巨大的价值，包括被动和主动信息收集、漏洞研究与开发、客户端攻击、后渗透（post-exploitation）等等方方面面。

在本模块中，我们浏览了 `Metasploit Framework` 的一些主要功能。然而，由于模块和功能极其繁多，人们很容易在其中迷失。为了巩固这些技术，我们强烈建议您彻底完成本模块中的练习，并参考免费的 `Offensive Security` 在线课程 `Metasploit Unleashed`⁷¹⁸，以获取更深入的培训和信息。

> ⁷¹⁸ (Offensive Security, 2017), https://www.offensive-security.com/metasploit-unleashed/Using_the_Database

## 23. PowerShell Empire

`Empire`⁷¹⁹ 是一个基于 `PowerShell` 和 `Python` 的后渗透代理，重点侧重于客户端利用以及对活动目录（AD）部署的后渗透。

利用和后渗透在 Windows 上使用 `PowerShell` 执行，在 Linux 和 macOS 上使用 `Python`。`Empire` 依赖于标准的预装库和功能；`PowerShell` 执行只需要 `PowerShell` 版本 2（Windows 7 起预装），而 Linux 和 Mac 模块需要 `Python` 2.6 或 2.7。

> 历史上，`PowerShell Empire` 侧重于 Windows 利用，而另一个名为 `Empire`⁷²⁰ 的独立项目针对 Mac OS/macOS 和 Linux。在 `PowerShell Empire` 的第二个版本中，这些项目合并了，并保留了原始名称，通常称为 `Empire`。`PowerShell Empire` 项目不再由原始开发者支持，但已经创建了更新的分支，例如 `BC-SECURITY`⁷²¹。该分支版本最近发布了 3.0⁷²² 版本。

`Empire` 与 `Metasploit Framework` 共享许多功能，但它们的本质是不同的。`Metasploit` 是一个用于获取初始访问的庞大漏洞集合。而 `Empire` 被设计为一种主要针对活动目录环境的后渗透工具。它倾向于利用目标操作系统及其主要应用程序的内置功能。

### 23.1 安装、设置与使用

要在 Kali 上安装 `Empire`，我们使用 `git` 从 GitHub 仓库克隆项目并运行 `install.sh` 脚本：

```
kali@kali:~$ cd /opt
```

```
kali@opt:~$ sudo git clone https://github.com/PowerShellEmpire/Empire.git

Cloning into 'Empire'...

remote: Enumerating objects: 12216.
remote: Total 12216 (delta 0), reused 0 (delta 0), pack-reused 12216
Receiving objects: 100% (12216/12216), 21.96 MIB | 3.22 MiB/s, done.
Resolving deltas: 100% (8312/8312), done.
```

```
kali@opt:~$ cd Empire/
```

⁷¹⁹ (Empire Project, 2019), https://github.com/EmpireProject/Empire

⁷²⁰ (Will Schröder, 2016), https://harmory.net/blog/empy/building-an-empy-python/

⁷²¹ (BC Security, 2019), https://github.com/BC-SECURITY/Empire

⁷²² (BC Security, 2019), https://github.com/BC-SECURITY/Empire/tree/dev

## 使用 Kali Linux 2.0 进行渗透测试

```
kali@kali:/opt/Empire sudo ./setup/install.sh
```

> 列表 819 - 使用共享在多个服务器上安装 PowerShell Empire

`Empire` 允许渗透测试人员通过共享私钥以及共享密码在多个服务器之间进行协作。然而，我们正在安装单个实例，因此将在密码提示处按回车键以生成随机密码。

- > 输入服务器协商密码，按回车进行随机生成：

> 列表 820 - 生成随机服务器密码协商

安装框架后，我们可以使用命名恰当的 Python 脚本 `empire` 启动 `Empire`。

```
kali@kali:/opt/Empire sudo ./empire

===========================
[Empire] Post-Exploitation Framework
===========================
[Version] 2.5 | [Web] https://github.com/EmpireProject/Empire
===========================
28 modules currently loaded
@ listeners currently active
@ agents currently active
```

> 列表 821 - 启动 PowerShell

### 23.1 PowerShell 语法

我们可以使用 `help` 列出 `Empire` 内可用的各种命令，包括监听器（listeners）、阶段器（stagers）和代理（agents）。

```
(Empire) > help
```

Commands
======
- `agents` 跳转到 Empire 菜单。
- `creds` 从数据库中添加/显示凭据。
- `exit` 退出 Empire
- `help` 显示帮助菜单。
- `interact` 与特定代理交互。
- `list` 列出活跃的代理或监听器。
- `load` 从非标准文件夹与活跃的监听器交互。
- `load` 插件以扩展 Empire。
- `list` 列出所有可用插件。
- `reload` (or `all`) 模块生成报告文件：`sessions.csv`, `credentials.csv`。
- `reset` 重置全局选项（例如 IP）。
- `read` 并从文件中读取并执行命令列表。
- `search` 搜索模块名/描述。
- `set` 设置全局选项（例如 IP）。
- `show` 显示全局选项（例如 IP）。
- `use` 使用 Empire

### 23.2 监听器与阶段器

`Empire` 允许渗透测试人员通过共享私钥以及共享密码在多个服务器之间进行协作。然而，我们正在安装单个实例，因此将在密码提示处按回车键以生成随机密码。

- > 输入服务器协商密码，按回车进行随机生成：

> 列表 820 - 生成随机服务器密码协商
