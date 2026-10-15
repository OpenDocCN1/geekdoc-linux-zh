
> 列表 819 - 使用共享在多个服务器上安装 PowerShell Empire

Empire 允许渗透测试人员通过共享私钥以及共享密码在多个服务器之间进行协作。然而，我们正在安装单个实例，因此将在密码提示处按回车键以生成随机密码。

- > 输入服务器协商密码，按回车进行随机生成：

> 列表 820 - 生成随机服务器密码协商

安装框架后，我们可以使用命名恰当的 Python 脚本 `empire` 启动 Empire。

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

## 23.1 PowerShell 语法

我们可以使用 `help` 列出 Empire 内可用的各种命令，包括监听器（`listeners`）、阶段器（`stagers`）和代理（`agents`）。

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
- `reload` （or `all`）模块生成报告文件：`sessions.csv`, `credentials.csv`。
- `reset` 重置全局选项（例如 IP）。
- `read` 并从文件中读取并执行命令列表。
- `search` 搜索模块名/描述。
- `set` 设置全局选项（例如 IP）。
- `show` 显示全局选项（例如 IP）。
- `use` 使用 Empire

## 23.2 监听器与阶段器

Empire 允许渗透测试人员通过共享私钥以及共享密码在多个服务器之间进行协作。然而，我们正在安装单个实例，因此将在密码提示处按回车键以生成随机密码。

- > 输入服务器协商密码，按回车进行随机生成：

> 列表 820 - 生成随机服务器密码协商
