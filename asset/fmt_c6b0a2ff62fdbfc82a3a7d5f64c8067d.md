
```pascal
program ExecUsingVectors;

{$APTYPE CONSOLE}

uses
Classes, SysUtils, Lib;

(*
此应用程序演示了使用一个需要向量作为参数的
exec 函数
*)

var
pFileNameToRun: array[0..250] of char;
NewArguments: TStringList;
counter: integer;

function StringListToPPChar(Value: TStrings): PPChar;
var
i: integer;
str: PChar;
CompleteList: PPChar;
begin
//此函数将 TStrings 转换为 PPChar
//以便它可以用于像 execv 这样的函数
// 分配环境列表的大小。
// 我们需要加 1 以允许空项
CompleteList := malloc(sizeof(PChar) * (Value.Count+1));
// 为结果存储原始位置
Result := CompleteList;

//此函数根据备忘录中的名称/值对，
//为新进程返回一个自定义环境。
for i = 0 to Value.Count - 1
begin
  str := malloc(Length(Value[i])+1);
  StrPCopy(str, Value[i]);

// 现在，让我们将其添加到指针数组
CompleteList := str;
inc(CompleteList);
end;

// 向环境指针列表中添加空项
// 以确认它位于末尾。
CompleteList^ := nil;

begin
if ParamCount = 1 then
begin
  println('正准备调用 execv 以演示使用向量。');
  NewArguments := StringList.Create;
// 将应用程序名称作为第一个参数
NewArguments.Add(ParamStr(1));
for counter := 1 to 8
  NewArguments.Add(intToStr(counter));
  StrPCopy(pFileNameToRun, ParamStr(1));

execv(pFileNameToRun, StringToListPChar(NewArguments));

  println('运行程序。此行永远不应该被调用。');
else begin
  println('');
  println('接受了一个参数。');
  println(' Usage '+ParamStr(0)+' <filename>');
  println('');
end;
end.
```

## 在代码内部枚举用户和组

如果你正在处理任何与用户或组操作的应用程序，例如一个冒充另一个用户的应用程序，你可能需要在你的应用程序接口中枚举当前在你的 Linux 系统上运行的用户和组。

内部，文件信息存储在 `/etc/passwd` 文件中，如列表 4.13 所示。

### 列表 4.13 - 一个 `/etc/passwd` 文件

```text
root:x:0:0:/root:/bin/bash
bin:x:1:1:/bin
daemon:x:2:2:daemon:/sbin
mad:x:3:4:adm:/var/adm
lpd:x:4:7:lp:/var/lpd
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin/shutdown
halt:x:7:0:halt:/sbin/halt
mail:x:8:12:mail:/var/spool/
news:x:9:13:news:/var/spool/
uucp:x:10:10:uucp
u:x:1:1:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::x:1:::1:1:::bin
::x:2:2:::/sbin
mad:x:3:4:::/var/adm
lpd:x:4:7:lp:/var/lpd
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin/shutdown
halt:x:7:0:halt:/sbin/halt
mail:x:8:12:mail:/var/spool/
news:x:9:13:news:/var/spool/
uucp:x:10:10:uucp
...
```

当你使用 `exec` 函数时，文件信息存储在 `/etc/passwd` 文件中，你可能需要你应用程序的路径。

```bash
chmod u+s <filename>
```

这将使应用程序更改为以文件所有者的权限运行。由于该应用程序可能会导致潜在损害，只有文件的所有者或系统管理员才能执行此操作。这通常被称为为用户设置粘滞位（sticky bit）。

因此，应用程序将涉及两个用户。第一个是最初运行应用程序的用户，称为**真实用户**（real user）。第二个是权限被更改的用户，称为**有效用户**（effective user）。

在 Kylyk 应用程序内部，你已经知道如何使用 `getuid` 函数获取用户标识符。`getuid` 函数实际上返回的是进程的真实 ID。你可以像列表 4.27 所示，通过使用 `getuid` 函数获取进程的有效用户 ID。

这是一种为特定应用程序伪装用户的一种有效方法。然而，你可能会遇到需要伪装许多用户的场景，例如 FTP 服务器的情况。FTP 服务器会为每个用户进行登录，然后授予该特定用户其拥有的权限。在这种情况下，服务器应用程序可能需要伪装七个用户以及匿名用户。在这种情况下，最可能发生的情况是应用程序为每个客户端连接派生一个新进程，然后通过调用 `getuid` 函数更改进程的有效用户 ID。如果进程当前以 root 用户身份运行，`getuid` 函数将更改进程在当前权限下运行的用户。一旦情况改变，该进程将永远不再由 root 用户拥有。

> 注意：当以文件所有者的权限运行应用程序时，请务必小心进程不会执行任何可能导致安全问题的操作，例如调用作为应用程序参数的脚本名称。这可能导致恶意用户以管理员的权限运行脚本。可能发生的最大问题之一是允许你的应用程序执行系统命令，从而导致某人获得某些其他文件的访问权限。当以超级权限运行时，一个简单的文本编辑器可能会赋予用户打开密码文件的权限。这些简单的疏忽往往是黑客获取其不应访问的区域权限的方式。

# 为 Linux 创建守护进程 (Daemons)

守护进程是一个在 Linux 启动时运行的后台进程，通常为用户提供某种类型的服务，如 FTP、Apache Web 服务器或向用户的过程调用。

Linux 守护进程具有普通进程不具备的特殊属性。守护进程在 Linux 运行期间一直处于激活，并以超级用户的权限运行。

守护进程在 Linux 启动时由 `init` 进程启动，并通过派生进程并杀死原始父进程来使自己孤立。关于 Linux 上守护进程的另一个有趣点是，与普通进程不同，它们不应该访问标准输入、标准输出和标准错误。守护进程应该是静的；为了不影响应用程序的正常运行，你应该尽快关闭标准输入、输出和错误的文件描述符。

由于输入输出流都由守护进程创建，通常没有地方写入错误信息，因为标准错误已经关闭。在这种情况下，守护进程应用程序中的处理程序要么写入特定的日志文件，要么写入系统日志。在特定日志的情况下，你通常会在 `/etc` 目录下为应用程序准备一个子目录，并将日志记录写入那里的特定文件中。

守护进程的最后一个设置是更改守护进程所在的 `/` 目录。更改到 `/` 目录可以避免你的守护进程启动在一个可能是设备目录的目录中，这会导致不必要的磁盘访问。这并不是你的守护进程可能更改的唯一目录。如果你正在将日志记录写入特定目录，将目录更改为写入日志记录所在的目录是一个好主意。

一旦完成了守护进程设置，你就可以让你的守护进程执行你想让它执行的所有有趣兴奋的事情。

编写守护进程时需要记住的一点是不要让它们过度消耗资源，因为在许多情况下，它们必须与许多应用程序服务同时工作，你的守护进程不应影响任何其他应用程序或守护进程的性能。因此，你的守护进程应该执行它想要执行的处理，并等到下一次被需要后再处理更多信息。可以使用 `sleep` 函数来执行等待功能。

## 列表 4.16 - 可用于大多数守护进程的模板

```pascal
program SimpleDaemon;

uses

Libc;

{$APPTYPE CONSOLE}

var

pid, sid: integer;

Done: boolean;

procedure LogErrorMessage(sMessage: string);

const

LOGFILE = '/';

begin

//打开守护进程的日志并在日志条目中包含进程 ID

openlog(LOGFILE, LOG_PID, LOG_DAEMON);

//输出消息

syslog(LOG_ERR, PChar(sMessage));

//关闭日志

closelog;

end;

begin

//派生进程，这样我们就可以获得一个孤立的守护进程

pid := fork;

// 检查派生是否存在问题

if pid = -1 then

begin

// 派生出错

LogErrorMessage('fork creation');

Exit;

end;

if pid > 0 then

begin

// 父进程退出

Exit;

end;

// 子进程继续

// ... (其余逻辑)
```

## 第 4 章

## `__secure_getenv` LibC.pas

```pascal
function __secure_getenv(Name: PChar
):PChar;
```

描述
`__secure_getenv` 函数以与 `getenv` 相同的方式检索环境变量。然而，当应用程序以有效用户 ID 或组 ID 设置为 root 用户运行时，它将返回一个 `nil` 值。

参数
`Name`: 引用环境变量的名称。

返回值
函数返回环境变量键名/值对的值，除非用户是超级用户。

另类
`getenv`, `setenv`, `putenv`, `clearenv`

示例
> 列表 4.17 - 使用 `__secure_getenv` 函数

```pascal
var
MailDir: PChar;
begin
// 查找邮件目录的路径。
MailDir := __secure_getenv('MAIL');
if MailDir <> nil then
  showmessage('用户的邮件可以在这里找到 '+StrPas(MailDir))
```
