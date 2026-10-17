
`print "exists(One) returned success.\n";`

`else`

`print "exists(One) returned an error.\n";`

`exit`

```
```

## exists

## 合规性

## 语法

```
类别 命名的一元运算符 (flow)

参数 表达式

参数 无

返回值 值
```

## 定义

此函数评估作为参数的表达式并带该错误退出程序。如果没有提供参数，默认错误值为 0。注意，`die()` 允许传递错误消息。

## 示例

```perl
exit(16);
```

## exp

## 合规性

## 语法

```
类别 命名的一元运算符 (numeric)

参数 表达式

参数 无

返回值 数值
```

## 定义

此函数返回以自然数底 (`e`) 为底的表达式幂（如果未指定，则为 `$_` 的幂）。

## 示例

```perl
print "exp() e**1 is \,exp(1)\n";
```

## fcnt

## 合规性

## 语法

```
类别 列表运算符 (i/o)

参数 句柄, 函数, 包参数
```

## 定义

此函数等同于 UNIX `fcntl()` 调用。在 Perl 5 中，使用 `fcntl` 模块。在 Perl 4 中，应该有某种机制将 Perl 函数链接到系统函数。这通常在安装 Perl 时执行。

## fileno

## 合规性

## 语法

```
类别 命名的一元运算符 (i/o)

参数 句柄

返回值 描述符
```

## 定义

此函数返回给定文件句柄的文件描述符。

## 示例

```perl
print("fileno() ",fileno(INF),"\n");
```

## flock

# 第 15 章 -- 函数列表

## 合规性

## 语法

```
类别 列表运算符 (i/o)

参数 句柄, 操作

返回值 1（真）''（假）
```

## 定义

此函数等同于 UNIX `fcntl()` 调用。在 Perl 5 中，使用 `fcntl` 模块。在 Perl 4 中，应该有某种机制将 Perl 函数链接到系统函数。这通常在安装 Perl 时执行。

## fork

## 合规性

## 语法

```
类别 列表运算符 (process)

参数 无

返回值 pid
```

## 定义

此函数将控制权从脚本传递到外部系统命令。此调用没有保留，因此没有返回值。注意，`system()` 调用外部命令，并会返回到调用 Perl 程序的下一行。

这等同于 UNIX 系统调用 `execvp()`。

## 示例

```perl
exec("cat /etc/motd");
```

## 定义

此函数根据提供的组 ID (`gid`) 在 `/etc/group` 系统文件中返回下一个组名（或返回未定义）。在列表上下文中，它返回从该文件中获取的额外信息（或返回空列表）。等于 UNIX 系统调用 `getgrgid()`。

## 示例

```
($grname, $grpw, $gid, @members) = getgrgid(0);
print("getgrgid() 返回给定 GID 的组名 [$grname]\n");
```

## getgrname

## 合规性

## 语法

分类命名一元运算符（系统文件）
参数 name
返回值 gid

## 定义

此函数根据提供的组名，在 `/etc/group` 系统文件中返回下一个组 ID，`gid`，（或返回未定义）。在列表上下文中，它返回从该文件中获取的额外信息（或返回空列表）。它等于 UNIX 系统调用 `getgrnam()`。

## 示例

```
($grname, $grpw, $gid, @members) = getgrnam("root");
print("getgrnam() 返回给定名称的 GID [$gid]\n");
```

## gethostbyaddr

## 合规性

## 语法

分类命名一元运算符（系统文件）
参数 address
返回值 name

## 定义

它根据提供的地址，在 `/etc/hosts` 系统文件中（或通过域名服务器查询）返回主机名（或返回未定义）。在列表上下文中，该函数返回从该文件中获取的额外信息（或返回空列表）。它等于 UNIX 系统调用 `gethostbyaddr()`。

## 示例（仅限 Perl 5）

```perl
use Socket;
@a=(140,203,7,103);
$addr=pack('C4',@a);
($name, $alias, $addrtype, $length,@address)=gethostbyaddr($addr,AF_INET);
print("gethostbyaddr() [$alias].\n");
```

## gethostbyname

## 合规性

## 语法

分类命名一元运算符（系统文件）
参数 name
返回值 address

## 定义

它根据提供的名称，在 `/etc/hosts` 系统文件中（或通过域名服务器查询）返回主机地址（或返回未定义）。在列表上下文中，它返回来自该文件的额外信息（或返回空列表）。此函数等于 UNIX 系统调用 `gethostbyname()`。

## 示例

```
($name, $alias, $adtype, $length, @address)=gethostbyname("lynch");
print("gethostbyname() [$alias].\n");
```

## gethostent

## 合规性

## 语法

- 分类（系统文件）
- 参数 无
- 返回值 name

## 定义

`gethostent` 返回 `/etc/hosts` 系统文件中的下一个主机名，或通过域名服务器查询返回未定义。在上下上下文中，它返回从该文件中获取的额外信息（或返回空列表）。此函数等于 UNIX 系统调用 `gethostent()`。

## 示例

```
($name, $alias, $adtype, $length, @address)=gethostbyname("lynch");
print("gethostent() [$alias].\n");
```

## getlogin

## 合规性

## 语法

- 分类（系统文件）
- 参数 无
返回值 name

# 第 15 章 -- 函数列表

## 定义

此函数从 `/etc/utmp` 系统文件中返回当前登录名。它比 `getpwnuid()` 函数更适合获取登录详细信息，因为 `/etc/utmp` 中存储的信息非常有限。

## 示例

```perl
print ("getlogin()", "getlogin(),\n");
```

## getnetbyaddr

## 合规性

## 语法

分类（系统文件）
参数 address
返回值 name

## 定义

`getnetbyaddr` 根据网络地址从 `/etc/networks` 系统文件中返回网络名称。在列表中，它从该文件中提取额外信息。此函数等于 UNIX 的 `getnetbyaddr()` 调用。

## 示例

```perl
($name, $alias, $addrtype, $net) = getnetent();
($name, $alias, $addrtype, $net) = getnetbyaddr($net, $addrtype);
print("getnetbyaddr() 读取 /etc/networks [$name]\n");
```

## getnetbyname

## 合规性

## 语法

```
分类命名一元运算符（系统文件）

参数 name

返回值 address
```

## 定义

根据网络名称从 `/etc/networks` 系统文件中返回地址。在列表上下文中，它返回来自该文件的额外信息。等于 UNIX 的 `getbyname()` 调用。

## 示例

```perl
($name,$alias,$addrtype,$net) = getbyname("localnet");
print("getbyname() 读取 /etc/networks [$name]\n");
```

## getnetent

## 合规性

## 语法

```
分类（系统文件）

参数 无

返回值 name
```

## 定义

此函数从 `/etc/networks` 系统文件中返回下一个网络名称。在列表中，它从该文件中返回额外信息。`getnetent` 等于 `getnetent()` 调用。

## 示例

```perl
($name,$alias,$addrtype,$net) = gethostent();
print("gethostent() /etc/hosts [$")
```

## getpeername

## 合规性

## 语法

```
分类命名一元运算符（系统文件）

参数 socket
```
