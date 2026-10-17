
- `registry_open_hklm`、`registry_open_hkcu`、`registry_open_hkcr` 在提供套接字、用户 ID、树 ID 和管道名称时返回等于 MSDN `RegConnectRegistry()` 的结果。该返回值适用于 `registry_get_key()`。

- `registry_get_key` 在提供套接字、用户 ID、树 ID、管道名称、键名以及其中一个 `registry_open_gethk*` 函数的响应时返回 `RegOpenKey()`。该返回值适用于 `registry_get_item*()` 函数。

- `registry_get_item_sz` 在提供套接字、用户 ID、树 ID、管道名称、项名以及 `registry_get_key` 函数的响应时，返回提供的注册键下的字符串对象。该返回值需要由 `registry_decode_sz()` 函数处理。

# 第 11 章 了解 Nessus 环境的扩展功能

- `registry_decode_sz` 在提供由 `registry_get_item_sz` 函数返回的响应时，它返回字符串内容。

以下函数未在任何脚本中使用，但对于清理充满间谍软件的计算机可能很有用：

- `registry_delete_key` 在提供套接字、用户 ID、管道名、键名以及 `registry_open_hk` 函数返回的响应时，它删除指定的键。

- `registry_delete_value` 在提供套接字、用户 ID、管道名、键名、`registry_open_hk` 函数返回的响应以及要删除的值名称时，它删除指定的注册表键值。

- `registry_shutdown` 此函数将在指定的超时后关闭或重启计算机。在实际关机之前，如果提供了套接字、用户 ID、树 ID、管道名、要显示的消息、以秒为单位的超时、是否重启或关机以及是否正常关闭所有应用程序，将显示一条消息。

下面的示例显示了如何确定远程主机是否安装了 Norton 杀毒服务以及该服务是否正在运行。如果 Norton 杀毒软件未运行，示例示例展示了如何利用 Microsoft Windows 服务控制管理器启动它。

要确定远程主机是否有 Norton AntiVirus 或 Symantec，首先运行 `snb_enum_services.nas` 测试，该测试将返回远程主机上所有可用服务的列表。接下来，准备 `snb_enum_services.nas` 需要的依赖项（`netbios_name_get.nas`、`smb_login.nas`、`cif445.nas`、`find_service.nes` 和 `logins.nas`）。接着，获取知识库项名为 `SMB/svcs` 的值；该知识库项包含远程主机上所有服务的列表。你可以通过以下代码来实现：

```
service_present = 0;
services = get_kb_item("SMB/svcs");
if(*[Norton AntiVirus Server]* !< services || *[Symantec AntiVirus Server]* !=!< services)
{
    service_present = 1;
}
```

## Windows 测试功能

由 `smb_hotfixes.inc` 文件提供

如果远程主机的注册表允许从远程位置访问，Nessus 就可以从中收集信息并将其存储在知识库中。一旦信息进入知识库，就可以创建不同类型的测试。最常见的测试是补丁包和热修复验证。

所有以下函数仅在远程主机的注册表已枚举的情况下起作用。如果注册表未被枚举，返回版本的函数将返回 `NULL`，而检查安装的函数将返回负一 (-1) 作为结果。此外，由于注册表枚举依赖于成功启动 `smb_hotfixes.nas` 测试的能力，因此在使用以下任何一个函数编写的测试时，必须将其作为依赖项提供：

- `hotfix_check_exchange_installed` 如果远程主机上安装了 Nessus Server，则此函数返回该 Nessus Server 的版本。

- `hotfix_data_access_version` 如果远程主机上安装了 Access 程序，则此函数返回该 Access 程序的版本。

- `hotfix_check_office_version` 此函数返回远程主机 Office 安装程序版本。要确定版本，远程主机上必须安装以下程序之一：Outlook、Word、Excel 或 PowerPoint。

- `hotfix_check_word_version`、`hotfix_check_excel_version`、`hotfix_check_powerpoint_version`、`hotfix_check_outlook_version` 如果远程主机上安装了 Word、Excel、PowerPoint 或 Outlook 程序，这些函数将返回相应的程序版本。

- `hotfix_check_works_installed` 如果远程主机上安装了 MS Works 程序，则此函数返回该程序版本。

- `hotfix_check_iis_installed` 根据远程主机是否安装了 IIS（互联网信息服务器），此函数返回 1 或 0。

- `hotfix_check_wins_installed`、`hotfix_check_dhcpserver_installed` 根据远程主机是否存在 WINS（Windows 互联网命名服务）服务器或 DCHP（动态主机主机控制协议）服务器，这些函数返回 1 或 -1。

- `hotfix_check_nt_server` 根据远程主机是否为 Windows NT 服务器，此函数返回 0 或 1。

- `hotfix_check_domain_controller` 根据远程主机是否为 Windows 域控制器，此函数返回 0 或 1。

- `hotfix_get_programfilesdir` 此函数返回远程主机上 Program Files 目录的位置。

- `hotfix_get_commonfilesdir` 此函数返回远程主机上 Common Files 目录的位置。

- `hotfix_get_systemroot` 此函数返回远程主机上 System Root 目录的位置。

- `hotfix_check_sp` 此函数验证远程主机上是否安装了补丁包。该函数使用提供的包级别来验证远程主机是否正在运行指定的程序类型以及是否安装了该补丁包。如果注册表未枚举，返回 -1；如果未安装包，返回 0；如果已安装，返回 1。

## 存储在知识库中的注册表键

`smb_hotfixes.inc` 函数包含了存储在注册表中的所有值。通过扩展 Nessus 持有的信息量，你可以加快扫描过程。例如，微软最近发布了一份名为“Web漏洞允许远程代码执行”（Vulnerability in Web Allows Remote Code Execution）的公告。该公告中描述的漏洞影响 Windows 2000、98、98SE 和 Windows ME。正如本章后面所示，我们仅支持 Windows NT、2000、XP 的安全测试。此外，公告所述，如果远程主机安装了 Service Pack 5，则 Windows 2000 安装将是免疫的。

要创建一个验证远程主机是否对漏洞免疫的测试，首先需要验证未安装此类补丁包，并且实际上远程主机运行的是 Windows 2000。为此，请使用以下行代码：

```
nt_sp_version = NULL;
win2k_sp_version = 5;
xp_sp_version = NULL;
win2003_sp_version = NULL;
```

```
if ( hotfix_check_sp( nt:nt_sp_version, win2k:win2k_sp_version, xp:xp_sp_version, win2003:win2003_sp_version) <= 0 )
exit(0);
```

在调用上述行之前，必须首先满足 `smb_hotfixes.nasl` 的依赖并验证远程注册表已枚举。这通过确保知识库项 `SMB/Registry/Enumerated` 存在来实现。通过在脚本中添加以下行：

```
script_dependencies("smb_hotfixes.nasl");
script_require_keys("SMB/Registry/Enumerated");
```

接下来，验证远程主机是否安装了热修复 Q894320。通过执行以下行代码来实现：

```
if ( hotfix_missing(name: "Q894320") > 0 )
security_hole(get_kb_item("SMB/transport"));
```

上一个示例代码中的两个函数定义在 `smb_hotfixes.inc` 文件中，必须通过在代码中添加以下行来才能调用这些函数：

```
include("smb_hotfixes.inc");
```

理解 Nessus 环境的扩展能力 • 第11 章 573

# 地下笔记...
