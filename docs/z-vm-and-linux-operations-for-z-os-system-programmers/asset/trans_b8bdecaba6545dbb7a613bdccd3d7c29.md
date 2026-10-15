

## 2.8.1 CP

与 CP 的交互主要通过命令行界面进行。您可以在命令行中键入命令并按 Enter 键提交处理，从而向 CP 发出命令。

CP 命令的长度始终为 1 到 12 个字符，并且不区分大小写。命令通常接受参数，所有参数均以空格分隔（与大多数命令行环境一样）。

许多命令可以缩写，但缩写形式更晦涩难懂。例如，QUERY NAMES 命令可以缩写为 Q N。执行任一版本的命令都会完成相同的任务。

本章始终使用完整命令，而非缩写形式。如果您想知道某个命令的缩写，请参阅 help 命令或《CP 命令和实用程序参考》（SC24-6073）。

## 进入 CP 模式

登录后，可能会发生各种情况，具体取决于您的虚拟机所运行的客户操作系统。由于我们在此只关心 CP，因此在我们的场景中，我们将关闭正在运行的客户操作系统并进入 CP 模式，以便直接向 CP 发出命令。

您的虚拟机很可能运行的是 CMS 操作系统。要确定是否正在运行 CMS，请查看登录时获得的输出。如果输出类似于示例 2-10，则表示您正在运行 CMS。最后一行（以 z/VM V5.3.0 开头）是 CMS 输出的第一行。

示例 2-10 登录时运行 CMS 所看到的输出

```
z/VM Version 5 Release 3.0, Service Level 0701 (64-bit),
built on IBM Virtualization Technology
There is no logmsg data
FILES: 0001 RDR,  NO PRT,  NO PUN
LOGON AT 09:54:43 EDT MONDAY 06/04/07
z/VM V5.3.0    2007-05-02 16:25
```

如果没有出现输出，您可能仍在运行 CMS。输入 QUERY CMSLEVEL 命令进一步检查。如果输出类似于第 67 页上的示例 2-11，则您正在运行 CMS。

## 示例 2-11 QUERY CMSLEVEL 命令的输出

```
QUERY CMSLEVEL
CMS Level 23, Service Level 701
Ready; T=0.01/0.01 09:57:17
```

重要说明：要停止 CMS 并进入 CP 模式，请发出 #CP SYSTEM CLEAR 命令。但请注意，如果您没有运行 CMS，此命令也可能有效，但它可能会损坏您的客户操作系统。发出 SYSTEM CLEAR 命令等同于将台式个人计算机的电源线从墙上插座中拔出。它会立即停止系统，不给操作系统完成当前操作和执行清理任务的机会。如果此时操作系统正在写入文件，您可能会丢失该文件的内容，甚至可能永久损坏文件系统。

因此，如果您没有运行 CMS，请查阅客户操作系统手册以获取正确的关闭说明。

z/OS 类比：对于 z/OS 用户而言，这类似于在 HMC 上对 LPAR 执行 SYSTEM RESET。

## 示例 2-12 #CP SYSTEM CLEAR 命令的输出

```
#CP SYSTEM CLEAR
Storage cleared - system reset.
```

此命令会清除虚拟机的内存，并停止和重置其所有虚拟处理器。

如果您确实处于 CP 模式，并且没有运行任何客户操作系统，则应该能够发出 BEGIN 命令并看到示例 2-13 中显示的输出。

## 示例 2-13 未运行客户操作系统时 BEGIN 命令的输出

```
BEGIN
HCPGIR453W CP entered; program interrupt loop
```

如果显示的内容不同，则很可能您仍在运行客户操作系统。

## 检查您的虚拟机

CP 有许多命令涉及获取有关您的虚拟机的信息以及定义其虚拟硬件配置。在本节中，我们将介绍用于获取有关您的虚拟机信息的命令。

首先，我们讨论 QUERY 命令，它提供有关您的虚拟机及其所运行系统的有用信息。该命令接受多个参数，其中大多数参数本身还有子参数。我们只介绍 query 命令功能的一部分。

z/OS 类比：Query 类似于 z/OS 中的各种 DISPLAY 命令。

### CP 版本

QUERY CPLEVEL 命令指示您正在运行的 CP 版本。您可以在登录虚拟机时运行此命令。在 z/VM 术语中，版本通常称为级别（level）。请参阅示例 2-14。

z/OS 类比：对于 z/OS，在发出系统命令 D IPLINFO 时会显示类似信息。也可以通过 TSO 和 ISPF 中的变量显示。

示例 2-14 QUERY CPLEVEL 命令的输出

```
QUERY CPLEVEL
z/VM Version 5 Release 3.0, service level 0701 (64-bit)
Generated at 05/02/07 16:28:04 EDT
IPL at 05/03/07 13:06:26 EDT
```

### 您的客户机名称

如果您刚刚登录，您可能知道您的客户机名称是什么（客户机名称是赋予您虚拟机的唯一标识名称）。但是，如果您同时打开了多个终端，并且忘记了哪个终端对应哪个客户机，则可以使用 CP 命令 QUERY USERID 来确定客户机名称；请参阅示例 2-15。

z/OS 类比：在 z/OS 中（登录到 ISPF 时），您的用户 ID 通常会显示在主选项面板中。

示例 2-15 QUERY USERID 命令的输出

```
QUERY USERID
TUX1 AT VMLINUX6
```

