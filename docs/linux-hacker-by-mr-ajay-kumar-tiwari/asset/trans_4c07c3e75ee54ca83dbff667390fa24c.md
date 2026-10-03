
## Linux 技巧

Ajay Kumar Tiwari

## Hack 80. 在 httpd.conf 中显示所有已接受的指令

这就像 httpd 的扩展帮助，它将显示所有 httpd.conf 指令及其有效的位置。对于特定指令，它会列出所有可能的值以及在 httpd.conf 中可以使用的位置。

这在你想快速了解某个 Apache 指令时非常有帮助。

```
# httpd -L
```

HostnameLookups (core.c)
“on” 表示启用，“off” 表示禁用反向 DNS 查找，
或 “double” 表示启用双重反向 DNS 查找
允许在 *.conf 中的任何位置
ServerLimit (prefork.c)
Apache 此次运行的 MaxClients 最大值
仅允许在 *.conf 中 <Directory>、<Files> 或 <Location> 之外
KeepAlive (http_core.c)
是否应将持久连接设为 On 或 Off
仅允许在 *.conf 中 <Directory>、<Files> 或 <Location> 之外
LoadModule (mod_so.c)
一个模块名称以及从中加载它的共享对象文件名
仅允许在 *.conf 中 <Directory>、<Files> 或 <Location> 之外

## Hack 81. 修改后验证 httpd.conf

使用选项 -t 来验证特定 Apache 配置文件是否存在问题。以下示例显示 httpd.conf.debug 第 148 行存在问题。mod_auth_basicso 在 so 之前缺少一个 .（句点）。

```
# httpd -t -f conf/httpd.conf.debug
```

httpd：语法错误在第 148 行的
/etc/httpd/conf/httpd.conf.debug：
无法加载 /etc/httpd/modules/mod_auth_basicso 到服务器：
/etc/httpd/modules/mod_auth_basicso：无法打开共享对象文件：没有此类文件或目录

修复问题后，它将显示 Syntax OK。

```
# httpd -t -f conf/httpd.conf.debug
```

语法正确

## Hack 82. 显示 httpd 构建参数

使用选项 -V（大写 V）来显示 Apache 版本号以及构建 Apache 时使用的所有参数。

```
# httpd -V
```

服务器版本：Apache/2.2.9 (Unix)
服务器构建时间：Jul 14 2008 15:36:56
服务器模块魔术数字：20051115:15
服务器加载：APR 1.2.12，APR-Util 1.2.12
编译使用：APR 1.2.12，APR-Util 1.2.12
架构：32 位
服务器 MPM：Prefork
线程化：否
分叉：是（可变进程数）
服务器编译时使用....

```
-D APACHE_MPM_DIR="server/mpm/prefork"
-D APR_HAS_SENDFILE
-D APR_HAS_MMAP
```

```
APR_HAVE_IPV6 (IPv4-mapped addresses enabled)
APR_USE_SYSVSEM_SERIALIZE
APR_USE_PTHREAD_SERIALIZE
SINGLE_LISTEN_UNSERIALIZED_ACCEPT
APR_HAS_OTHER_CHILD
APR_HAVE_RELIABLE_PIPED_LOGS
DYNAMIC_MODULE_LIMIT=128
HTTPD_ROOT="/etc/httpd"
SUEXEC_BIN="/usr/sbin/suexec"
DEFAULT_PIDLOG="logs/httpd.pid"
DEFAULT_SCOREBOARD="logs/apache_runtime_status"
DEFAULT_LOCKFILE="logs/accept.lock"
DEFAULT_ERRORLOG="logs/error_log"
AP_TYPES_CONFIG_FILE="conf/mime.types"
```

SERVER_CONFIG_FILE="conf/httpd.conf"

如果只想显示 Apache 版本号，请使用以下所示的选项 -v（小写 v）。

```
# httpd -v
```

服务器版本：Apache/2.2.9 (Unix)

服务器构建时间：Jul 14 2008 15:36:56

## Hack 83. 按需加载特定模块

有时你可能不想在 Apache 中加载所有模块。例如

你可能只想在测试 LDAP 时才向 Apache 加载与 ldap 相关的模块。这可以按如下方式实现。

修改 httpd.conf 并添加名为 load-ldap 的 IfDefine 指令（你可以随意命名）。

```
<IfDefine load-ldap>
LoadModule ldap_module modules/mod_ldap.so
LoadModule authnz_ldap_module modules/mod_authnz_ldap.so
</IfDefine>
```

当你正在测试 ldap 并希望加载与 ldap 相关的模块时，将 load-ldap 传递给选项 -D，如下所示：

```
# httpd -k start -e debug -Dload-ldap -f /etc/httpd/conf/httpd.conf.debug
```

```
[Sun Aug 17 14:14:58 2008] [debug] mod_so.c(246):
loaded module ldap_module
```

```
[Sun Aug 17 14:14:58 2008] [debug] mod_so.c(246):
loaded module authnz_ldap_module
```

[注意：传递 -Dload-ldap 以将 ldap 模块加载到 Apache]

```
# apachectl start
```

[注意：如果不想加载 ldap 模块，请正常启动 Apache。]

## 第 11 章：Bash 脚本

## Hack 84. .bash_* 文件的执行顺序

以下文件的执行顺序是什么？

- /etc/profile
- ~/.bash_profile
- ~/.bashrc
- ~/.bash_login
- ~/.profile
- ~/.bash_logout

### 交互式登录 shell 的执行顺序

以下伪代码解释了这些文件的执行顺序。

```
execute /etc/profile
IF ~/.bash_profile exists THEN
  execute ~/.bash_profile
ELSE
  IF ~/.bash_login exist THEN
  execute ~/.bash_login
  ELSE
  IF ~/.profile exist THEN
  execute ~/.profile
  END IF
  END IF
END IF
```

当你退出交互式 shell 时，执行顺序如下：

```
IF ~/.bash_logout exists THEN
  execute ~/.bash_logout
END IF
```

请注意，/etc/bashrc 由 ~/.bashrc 执行，如下所示：

```
# cat ~/.bashrc
if [ -f /etc/bashrc ]; then
. /etc/bashrc
fi
```

### 交互式非登录 shell 的执行顺序

启动非登录交互式 shell 时，执行顺序如下：

```
IF ~/.bashrc exists THEN
  execute ~/.bashrc
END IF
```

注意：当非交互式 shell 启动时，它会查找 ENV 环境变量，并执行 ENV 变量中提到的文件名值。

## Hack 85. 如何在 bash shell 中生成随机数

使用 $RANDOM bash 内置函数生成 0 – 32767 之间的随机数，如下所示。

```
$ echo $RANDOM
106
$ echo $RANDOM
22543
$ echo $RANDOM
25387
$ echo $RANDOM
647
```

## Hack 86. 调试 shell 脚本

要调试 shell 脚本，请在脚本顶部使用 set -xv。

无调试命令的 Shell 脚本：

```
$ cat filesize.sh
#!/bin/bash
for filesize in $(ls -l . | grep "^-" | awk '{print $5}')
do
  let totalsize=$totalsize+$filesize
done
echo "Total file size in current directory: $totalsize"
```

无调试命令的 Shell 脚本输出：

$ ./filesize.sh
当前目录总文件大小：652

带有调试命令的 Shell 脚本：

现在在 shell 脚本中添加 set -xv 以调试输出，如下所示。

```
$ cat filesize.sh
#!/bin/bash
set -xv
for filesize in $(ls -l . | grep "^-" | awk '{print $5}')
do
  let totalsize=$totalsize+$filesize
done
echo "Total file size in current directory: $totalsize"
```

带有调试命令的 Shell 脚本输出：

```
$ ./fs.sh
++ ls -l .
++ grep '^-'
++ awk '{print $5}'
+ for filesize in '$(ls -l . | grep "^-" | awk '{print $5}')'
+ let totalsize=+178
+ for filesize in '$(ls -l . | grep "^-" | awk '{print $5}')'
+ let totalsize=178+285
+ for filesize in '$(ls -l . | grep "^-" | awk '{print $5}')'
+ let totalsize=463+189
+ echo 'Total file size in current directory: 652'
Total file size in current directory: 652
```

使用调试选项执行 Shell 脚本：

除了在 shell 脚本内部给出 set -xv 外，你也可以在执行 shell 脚本时提供它，如下所示。

```
$ bash -xv filesize.sh
```

## Hack 87. 引号

不带特殊字符的 echo 语句。

```
$ echo The Geek Stuff
```

The Geek Stuff

echo 语句带有一个特殊字符 ; 。分号是 bash 中的命令终止符。在以下示例中，“The Geek” 对 echo 有效，而 “Stuff” 被视为单独的 Linux 命令并导致命令未找到。

```
$ echo The Geek; Stuff
```

The Geek

-bash: Stuff: command not found

为避免这种情况，你可以在分号前添加 \，这将移除分号的特殊含义并仅将其打印出来，如下所示。

```
$ echo The Geek\; Stuff
```

The Geek; Stuff

### 单引号

当你想逐字打印单引号内的所有内容时，使用单引号。即使是 $HOSTNAME 这样的特殊变量也会被打印为 $HOSTNAME，而不是打印 Linux 主机的名称。

```
$ echo 'Hostname=$HOSTNAME ; Message=\$ is USD'
```

Hostname=$HOSTNAME ;

Message=\$ is USD

Current User=`whoami` ;

### 双引号

当你想显示特殊变量的真实含义时，使用双引号。

```
$ echo "Hostname=$HOSTNAME ; Message=\$ is USD"
Current User=`whoami` ;
