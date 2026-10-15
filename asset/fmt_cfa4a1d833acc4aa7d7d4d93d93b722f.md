
- 7 将客户机控制台地址定义为与 z/OS 控制台相同的地址。请注意，由于 z/VM 控制台要求，此阶段必须将其定义为 `3215`。它将在 `IPLSC59 EXEC` 中重新定义为 `3270` 以便 IPL z/OS（参见第 225 页的示例 4-18）。
- 8 将到 z/VM vswitch 的连接定义为 OSA 设备，从地址 `2000` 开始的六个连续地址。
- 9 定义客户机在 CMS 中的 minidisk。用于 CMS 文件系统，例如 `PROFILE EXEC`（后面描述）。
- 10 11 提供 z/OS 所需的 DASD 定义。它们都定义为 minidisks，从第 0 个柱面开始到最高柱面结束（整个磁盘）。在我们的例子中，每个设备的实际地址和虚拟地址是相同的。磁盘地址可以使用除实际地址之外的地址来定义，以简化测试映像的配置管理。还请注意，磁盘定义为访问模式 `MWW`，即多写访问。最后的 `V` 定义 CP 应为此 minidisk 的 I/O 操作使用其虚拟保留/释放支持。这是为了确保如果从多个客户机访问时的完整性。如果有共享只读 DASD，则访问可以定义为只读（`RR`）。

> 注：并非所有磁盘都列出，只有几个示例用于说明目的。还有其他 minidisks 定义给客户机 SC59。

> 提示：你可以将 minidisks 定义为访问模式 `RR` 以防止它们被更新，如果这是期望的。这对于防止对某些磁盘（例如你的 SYSRES 或 IODF 磁盘）的分配或更新很有用，而无需在 RACF 或类似产品中调整任何访问规则。

更新完 USER DIRECT 文件后，保存该文件并执行以下 DIRECTXA 命令，将新的目录加载到 z/VM 存储中。

`directxa user direct c`

## 4.5.4 ZOS1 客机控制台注意事项

在此场景中，为简化操作，我们选择不使用任何通道连接控制台来操作该映像。这意味着我们可以登录到 z/VM 客机用户 ID，IPL z/OS，并将该会话用作 z/OS 操作员控制台。

**警告：** 一个问题是，如果 z/OS 操作员发出 `CP LOGoff`，z/OS 系统将立即终止。应使用 `CP DISConnect` 来保持系统运行。

**重要：** 在 z/VM 客机上运行 z/OS 时，HMC 控制台不能用于 IPL z/OS 客机

这种操作方式还意味着，我们需要在 IPL z/OS 之前将操作员控制台的模式更改为 `3270`，以避免控制台锁定，因为 `3270` 是 z/OS 中支持的终端类型。

## 4.5.5 SC59 客机 PROFILE EXEC 创建

我们为客机用户 ID SC59 创建了一个 `PROFILE EXEC` 文件来定义额外的 CPU。您可以根据各安装的要求添加其他定义。`PROFILE EXEC` 在每次执行 CMS IPL 时都会执行。该 exec 在用户 ID 自动登录到 z/VM 系统时也会执行。从断开的虚拟机重新连接不会执行 `PROFILE EXEC`。

图 4-37 显示了 SC59 用户 ID 的 `PROFILE EXEC` 文件。

```
PROFILE EXEC  F1 V 130  Trunc=130

00000 * * * Top of File * * *
00001 /* PROFILE EXEC FOR SC59 */
00002 set pf12 ret
00003 'CP DEFINE CPU 1'
00004 'CP DEFINE CPU 2'
00005 'CP DEFINE CPU 3'
```

*图 4-37 SC59 的 PROFILE EXEC*

重要：通过我们的方式定义 `PROFILE EXEC`，您无法 AUTOLOG 此机器并使 z/OS 系统自动 IPL。该文件不包含实际 IPL z/OS 映像的任何语句。

与其将执行 z/OS 映像 IPL 所需的语句和命令放在配置文件中，我们创建了一个 exec 来实际执行此操作。简而言之，此 exec 执行以下任务：

- 1. 将控制台模式切换为 `3270`
- 2. 发出命令 `SET RUN ON`
- 3. IPL z/OS 映像

图 4-38 显示了 `IPLSC59 EXEC` 的内容。

```
IPLSC59 EXEC      A1  V 130  Trunc=130 Size=14 Line=0 Col=1 Alt=2
00000 * * * Top of File * * *
00001 /* Exec to IPL the SC59 guest system */
00002 trace 'o'
00003 'vmfclear'
00004 cmd = 'TERM CONMODE 3270' || '15'X
00005 cmd = cmd || 'SET RUN ON' || '15'X
00006 say '**************************************************'
00007 say '*'
00008 say '*    This is a z/OS 1.9 system,'
00009 say '*    WAIT, the system is coming up... SC59'
00010 say '*'
00011 say '**************************************************'
00012 cmd = cmd || 'IPL D42A LOADPARM C73059M1 CLEAR'
00013 push cmd
00014 exit
00015 * * * End of File * * *
```

图 4-38 IPL 内容

`IPLSC59 exec` 中的重要项目在以下列表中描述：

- `TERM CONMODE 3270` 这会将模式（或终端类型）切换为 `3270`。
- `'15'x` 这是每个命令之后出现的换行指示符。命令本身被堆叠，并在 exec 结束之后发出（不受 exec 本身中的任何逻辑控制）。
- `SET RUN ON`

这用于避免虚拟机进入 CP 读取模式导致 z/OS 停止

- `IPL D42A`

这是 z/OS 的实际 IPL 命令，如果您在 LPAR 中运行 z/OS，通常在 HMC 中输入。

> 注意：`IPLSC59 EXEC` 中的以下重要语句或命令，都可以作为来自虚拟机本身的单独命令发出，而不是执行 `IPLSC59 EXEC`：
>
> ► `TERM CONMODE 3270`
>
> ► `SET RUN ON`
>
> ► `IPL D42A LOADPARM C73059M1 CLEAR`

## 4.5.6 作为 z/VM 客机 IPL 系统

创建了前面的文件后，我们关闭了在 LPAR 中运行的 z/OS 系统。然后，我们登录到 z/VM 用户 ID SC59 并运行 `IPLSC59 EXEC`。过了一会儿（就像正常 IPL LPAR 一样），我们看到了初始消息，我们的会话看起来与正常的 z/OS 操作员控制台完全相同。在启动所有必要的 started-task 和子系统后，我们发出 `CP DISC` 命令以从系统控制台断开连接，使 z/OS 系统继续运行。

> 注意：在我们定义控制台的方式中，有一个特殊之处，即在初始 IPL 时，我们必须在操作员响应前加上 `#CP VINPUT VMSG` 才能在 NIPCON 模式下与 z/OS 通信；例如：
>
> `#CP VINPUT VMSG R 00,CONTINUE`
>
> 进入正常控制台模式后，这就不再是事实了。在操作物理连接的控制台时，这不应是必要的。

## 4.5.7 z/OS 注意事项

从 z/OS 角度来看，需要注意的一点是，任何使用 symbolics `HWNAME` 和 `LPARNAME` 的情况。如果这些在 PARMLIB 成员（例如您的 `IEASYMxx`）或驻留在 PARMLIB 或 `SYSn.IPLPARM` 中的成员 `LOADxx` 中使用，它们就需要您关注。当 z/OS 作为 z/VM 客机运行时，`LPARNAME` 永远无法解析，因此对这些变量值的任何过滤都会失败。根据您包含的逻辑，IPL 可能因此问题而失败。如果您对 `HWNAME` 有过滤器，您应考虑将其更改为 `VMUSERID`。详情请参阅 z/OS: MVS Initialization and Tuning Reference，SA22-7592。

# 4.5.8 向 z/OS 客户机添加 3390 磁盘

与在 LPAR 中运行的任何 z/OS 系统一样，有时系统需要额外的 I/O 设备，例如 DASD。在 LPAR 中，在该 LPAR 的 `IOCDS` 中定义新的 DASD 即可使新卷可供 z/OS 系统使用。当 z/OS 系统作为 z/VM 客户机运行时，也存在类似的功能。在 z/OS 客户机系统启动后，我们进行了一系列步骤，在不中断系统或需要 IPL 的情况下，将新的 3390 磁盘卷上线到客户机系统。我们还决定将物理设备地址 `8222` 作为设备地址 `6000` 在 z/OS 上定义的那样上线到 z/OS 客户机。该磁盘的 volser 为 `DK8222`。我们首先将其作为客户机用户（在 USER DIRECT 文件中）的 minidisk 添加，如示例 4-18 所示。
