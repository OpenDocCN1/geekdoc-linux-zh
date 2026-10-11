
## 16.2.5 进程优先级与友好度（Niceness）

内核会为每个进程维护其选定的调度优先级。大多数交互式任务和短任务通常会被赋予更高的优先级。UNIX 的 `nice` 命令允许你修改进程的调度优先级。在中等或高负载系统上，让 CPU 密集型任务运行得更慢可能对你有利，这样需要更高优先级的任务就能更快地访问 CPU。那些不独占处理器资源的任务被称为“友好”（nice）的。

`nice` 值用于计算进程的优先级。具有正 `nice` 值的进程以低优先级运行，意味着它获得的 CPU 时间份额较少。具有负 `nice` 值的进程以高优先级运行，获得比其份额更多的处理器资源。`nice` 值的范围从 -20 到 19。大多数进程以零优先级运行，以平衡其对 CPU 的访问。（只有超级用户才能设置负 `nice` 值。）

以下函数 `getpriority` 和 `setpriority` 的命名源自对应的系统调用，可在 UNIX 手册页的第 2 节中找到。

### getpriority 函数

`getpriority` 函数返回某个进程、进程组或用户的当前优先级（`nice` 值）。并非所有系统都支持此函数。如果未实现，`getpriority` 将产生致命错误。`WHICH` 是以下三个值之一：0 表示进程优先级，1 表示进程组优先级，2 表示用户优先级。`WHO` 根据进程优先级、进程组优先级或用户优先级相对于进程标识符进行解释。零值代表当前的进程、进程组或用户。

#### 语法

```perl
getpriority (WHICH, WHO);
```

#### 示例 16.36

```perl
(脚本内容)
1 $niceval = getpriority(0, 0);
2 print "The priority, nice value, for this process is $niceval\n";
```

```text
(输出内容)
1 The priority, nice value, for this process is 0.
```

#### 解释

- `getpriority` 函数将返回当前进程的 `nice` 值。
- 此进程的 `nice` 值为零。这意味着该进程在从 CPU 获取时间份额时没有获得任何特殊优待。

### setpriority 函数（nice）

`setpriority` 函数用于设置进程、进程组或用户的当前优先级（`nice` 值）。它用于修改进程的调度优先级。如果你的系统未实现 `setpriority` 系统调用，`setpriority` 将抛出错误。

`WHICH` 是以下三个值之一：0 表示进程优先级，1 表示进程组优先级，2 表示用户优先级。`WHO` 根据进程优先级、进程组优先级或用户优先级相对于进程标识符进行解释。零值代表当前的进程、进程组或用户。`NICEVALUE` 是 `nice` 值。较低的 `nice` 值会提高进程优先级，较高的 `nice` 值会降低进程优先级。（这很容易混淆！）

除非你拥有超级用户权限，否则不能使用负的 `nice` 值。这样做不会改变当前的 `nice` 值。

#### 语法

```perl
setpriority(WHICH, WHO, NICEVALUE),
```

#### 示例 16.37

```perl
(脚本内容)
1 $niceval = getpriority(0,0);
2 print "The nice value for this process is $niceval.\n";
3 setpriority(0,0, ( $niceval + 5 ));
4 print "The nice value for this process is now", getpriority(0,0);
```

```text
(输出内容)
2 The nice value for this process is 0.
4 The nice value for this process is now 5.
```

#### 解释

- `getpriority` 函数将返回当前进程的 `nice` 值。
- 打印该 `nice` 值。
- `setpriority` 函数将当前进程的 `nice` 值增加 5。该进程的优先级将会降低。它表现得“更友好”。
- `getpriority` 函数返回的新 `nice` 值为 5。

## 16.2.6 密码信息

**UNIX.** 以下函数通过遍历 `/etc/passwd` 文件，并将该文件中的信息检索到数组中。这些函数的命名与系统库中找到的同名函数（参见 UNIX 手册第 3 节）相同，并执行相同的任务。如果你有兴趣获取关于 `/etc/group` 文件的信息，Perl 函数 `getgrent`、`getgrgid` 和 `getgrnam` 都会返回一个包含组条目信息的四元素数组。这些函数的描述见 UNIX 手册页。以下是一个 `/etc/passwd` 文件的示例：

```text
root::YhTLR4he8dxfw:0:1:Operator:/:/bin/csh
nobody::*::65534:65534::/: 
sys::*:2:2:/:/bin/csh
bin::*:3:3:/:/bin
uucp:*:4:8:/var/spool/uucppublic:
news:*:6:6:/var/spool/news:/bin/csh
sync:*:11::/bin/sync
ellie:aVD17T88mBMfGy:9496:40:Ellie Shellie:/home/jody/ellie:/bin/ksh
```

**Windows.** Windows 将用户信息存储在一个名为 SAM（Security Accounts Manager，安全账户管理器）的二进制数据库中，它是注册表的一部分。由于数据以二进制格式存储，普通的 Perl 读取操作无法正常工作。最好使用 Win32 扩展来获取用户信息。Win32.NetAdmin 随 ActiveState 一起捆绑，位于 `per\site\lib\win32` 目录下。（参见表 16-9。）你可以使用该模块的两个函数 `UserGetAttributes` 和 `UserSetAttributes` 来操作用户账户。

Win32 的 `net.exe` 命令也显示关于用户和系统的信息。

#### 示例 16.38

```text
    1. C:\ net help
        The syntax of this command is:

        NET HELP command
            -or-
        NET command /HELP

        Commands available are:
        NET ACCOUNTS      NET HELP      NET SHARE
        NET COMPUTER      NET HELPMSG   NET START
        NET CONFIG        NET LOCALGROUP  NET STATISTICS
        NET CONFIG SERVER NET NAME        NET STOP
        NET CONFIG WORKSTATION NET PAUSE   NET TIME
        NET CONTINUE      NET PRINT       NET USER
        NET FILE          NET SEND        NET VIEW
        NET GROUP         NET SESSION

        NET HELP SERVICES lists the network services you can start.
        NET HELP SYNTAX explains how to read NET HELP syntax lines.
        NET HELP command | MORE displays Help one screen at a time.

    2. C:\ net user

        User accounts for \HOMEBOUND

        Administrator    Ellie Quigley    Guest.
        The command completed successfully.
```

### 表 16.9 Win32::NetAdmin 扩展

| 函数 | 参数 |
| :--- | :--- |
| `Win32::NetAdmin::UserGetAttributes` | `$Machine`, `$UserName`, `$Password`, `$PasswordAge`, `$Privilege`, `$Homedir`, `$Comment`, `$Flags`, `$ScriptPath` |
| `Win32::NetAdmin::UserSetAttributes` | `$Machine`, `$UserName`, `$Password`, `$PasswordAge`, `$Privilege`, `$Homedir`, `$Comment`, `$Flags`, `$ScriptPath` |

#### 示例 16.39

```perl
1 use Win32::NetAdmin qw(GetUsers UserGetAttributes);
2 GetUsers('*', FILTER_NORMAL_ACCOUNT) or die;
3 foreach $key (sort keys %hash) {
    print "$key\n";
}
```

```text
(输出内容)
Administrator
Elise Quigley
Guest
```

你不能将加密的密码从 UNIX 系统传输到 Win32 系统，反之亦然。它们在密码学上是不兼容的。要管理密码，请使用 Win32::AdminMisc 或 Win32::NetAdmin 模块扩展。参见表 16.10。

## 16.2 进程

### 表 16.10 Win32 密码扩展

| 函数 | 参数 |
| :--- | :--- |
| `Win32::AdminMisc::UserCheckPassword` | `$Machine`, `$User`, `$Password` |
| `Win32::AdminMisc::SetPassword` | `($Machine \| $Domain)`, `$User`, `$NewPassword` |
| `Win32::AdminMisc::UserChangePassword` | `($Machine \| $Domain)`, `$User`, `$OldPassword`, `$NewPassword` |
| `Win32::NetAdmin::UserChangePassword` | `($Machine \| $Domain)`, `$User`, `$OldPassword`, `$NewPassword` |

对于 Windows 用户，以下用于获取组和用户信息的函数尚未实现：

- `endgrant()`, `endpwent()`, `getgrent()`, `getgrgid()`, `getgrnam()`
- `getpent()`, `getpwnam()`, `getpwuid()`, `setgrent()`, `setpwent()`

在你的提示符下，输入 `perldoc perlport` 以帮助解决不同操作系统之间的可移植性问题。

**获取密码条目（UNIX）——getpwent 函数。** `getpwent` 函数从 `/etc/passwd` 文件中检索信息。`getpwent` 的返回值是一个九元素数组，包含：

- 登录名
- 加密的密码
- 用户 ID
- 组 ID
- 配额
- 注释
- Gcos（用户信息）
- 主目录
- 登录 Shell

#### 语法

```perl
$(name, $passwd, $uid, $gid, $quota, $comment, $gcos, $dir,
$shell) = getpwent;
```

#### 示例 16.40

```perl
(脚本内容)
1 while( @info=getpwent) {
2 print "$info[0] \n" if $info[1] =~ /^\*/;
}
```
