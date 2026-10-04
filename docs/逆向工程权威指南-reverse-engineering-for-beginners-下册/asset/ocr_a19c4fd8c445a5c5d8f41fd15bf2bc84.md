# 第81章 Oracle DBMS

# 81.1 V$VERSION表

Oracle DBMS包含2个规模巨大的数据库系统。其主程序oracle.exe包含近14000个函数。相比之下，Windows 7 x86的内核ntoskrnl.exe有近11000个函数；Linux 3.9.8的内核（默认编译/带有默认驱动程序）包含的函数不超过31000个左右。

本章首先演示一个简单的Oracle查询命令。我们可以通过下述查询Oracle RDBMS数据库的版本信息：

```
SQL> select * from V$VERSION;
```

上述指令的返回结果如下：

```
Oracle Database 11g Enterprise Edition Release 11.2.0.1.0 - Production
PL/SQL Release 11.2.0.1.0 - Production
CORE 11.2.0.1.0 Production
TNS for 32-bit Windows: Version 11.2.0.1.0 - Production
NLSRTL Version 11.2.0.1.0 - Production
```

第一个问题就来了：字符串“V$VERSION”存储在Oracle RDBMS的什么地方？