
```xml
            xmlns="http://schemas.microsoft.com/SMI/2005/WindowsSettings">

            <dpiAware>true</dpiAware>

            <autoElevate>true</autoElevate>

        </asmv3:windowsSettings>

    </asmv3:application>

</assembly>
```

快速查看结果可知，该应用程序旨在由管理员用户运行，因此需要完整的管理员访问令牌。此外，自动提升标志设置为 `true`，这允许可执行文件自动提升到高级完整性，而无需提示管理员用户同意。

我们可以使用 Sysinternals 套件中的 Process Monitor 来收集有关此工具在执行过程中的更多信息。

> **注意：** 以下来自第 534-535 页的内容似乎是关于完整性级别的前文，引出了 UAC 绕过部分。为了保持逻辑流程（按照要求“合并连续段落”），以下是整理后的前一部分：

如输出最后一行所报告，此命令提示符当前正以中级完整性运行。

让我们尝试从这个命令提示符更改 `admin` 用户的密码：

```text

C:\Users\admin> net user admin Evi@pass

System error 5 has occurred.

Access is denied.

```

请求被拒绝，即使我们以管理员用户身份登录。

为了更改 `admin` 用户的密码，即使是以管理员用户身份登录，我们也必须切换到高级完整性级别。在我们的示例中，实现这一点的一种方法是通过使用 `powershell.exe` 和 `Start-Process` cmdlet，并指定“以管理员身份运行”选项：

```text

C:\Users\admin> powershell -Use Start-Process cmd.exe -Verb runAs

```

提交此命令并接受 UAC 提示后，我们会看到一个新的高完整性 `cmd.exe` 进程。

让我们使用 `whoami` 实用程序及其 `/groups` 参数来检查我们的完整性级别，并再次尝试更改密码：

```text

C:\Windows\system32> whoami /groups

GROUP INFORMATION

-------------------

Group Name                           Type            SID          Attributes

--------------------------------  --------------  ------------  -------------

Everyone                                 Well-known group S-1-1-0        Mandatory group,

NT AUTHORITY\Local account and member   Well-known group S-1-5-114     Mandatory group,

BUILTIN\Administrators                   Alias          S-1-5-32-544   Mandatory group,

BUILTIN\Users                            Alias          S-1-5-32-545   Mandatory group,

NT AUTHORITY\INTERACTIVE                 Well-known group S-1-5-4      Mandatory group,

CONSOLE LOGON                            Well-known group S-1-2-1       Mandatory group,

NT AUTHORITY\Authenticated Users            Well-known group S-1-5-11   Mandatory group,

NT AUTHORITY\This Organization              Well-known group S-1-5-15   Mandatory group,

NT AUTHORITY\Local account                    Well-known group S-1-5-113  Mandatory group,

LOCAL                                       Well-known group S-1-2-0     Mandatory group,

NT AUTHORITY\NTLM Authentication             Well-known group S-1-5-64-10 Mandatory group,

Mandatory Label\High Mandatory Level       Label                S-1-16-12288

```

```text

C:\Windows\system32> net user admin Ev!lpass

The command completed successfully.
```
