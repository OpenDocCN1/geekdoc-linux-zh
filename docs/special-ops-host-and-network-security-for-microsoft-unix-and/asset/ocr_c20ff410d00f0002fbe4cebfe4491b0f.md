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