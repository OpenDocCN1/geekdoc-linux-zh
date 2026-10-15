

`-u units` 列出所有超过 `units` 未登录的用户。显示的字段为 `time_last_login`、`tty_last_login`、`host_last_login` 和 `unsuccessful_login_count`。

`units` 是一个数字，可选择后跟字母 M、h、d、w 或 m，其中 M 代表分钟，h 代表小时，d 代表天，w 代表周，m 代表月。指定的数字按该单位计算并转换为秒。

只有当所有条件都满足时条目才匹配，并且只能指定标志 l、r 或 u 中的一个。如果未指定标志，则假定为 -10。user 可以是一个或多个用户名，以空格分隔。如果未给出，则检查所有用户条目。

## Listing 8.2 (continued)

```c
if( argv[optind] ){
    char *endptr;
    errno = 0;
    /*
    ** Check if number is not too big for us to handle
    */
    epoch = strtol(argv[optind], &endptr, 10);
    if( errno == ERANGE ){
        fprintf(stderr, "%s: parameter %s out of range\n", Prog, argv[optind]);
        exit(2);
    }
    /*
    ** If parameter epoch doesn't start with a digit or doesn't
    ** entirely consist of digits print an error and give up.
    */
    if( strlen(argv[optind]) == 0
        || strlen(argv[optind]) != strspn(argv[optind], "0123456789") ){
        fprintf(stderr, "%s: parameter '%s' is invalid\n", Prog, argv[optind]);
        exit(3);
    }
}
/*
** Default format is output of the date command
*/
if( format == NULL )
    format = "%c%n";
}else{
    if( format == NULL ){
        /* Just print current time in seconds since epoch */
        printf("%ld\n", epoch);
        return 0;
    }

    /* Convert time to human readable format */
    tmpt = localtime(&epoch);
    strftime(buf, sizeof buf, format, tmpt);
    printf("%s", buf);
    return 0;
}
```

terminallist 和 hostlist 在标志 -r 被指定的情况下按以下示例映射到不成功的终端或主机名。

```
User  FailedDate  Time    Tty     Host
guest1  08-Jul-94 10:30 pts/0 os2box
adm     0   22-Aug-94 16:01 pts/3 9.20.183.155
root    0   29-Aug-94 13:29 hft/0 tiger
richter 0   8-Sep-94 16:58 hft/0 tiger
```

lastlogin -u10 -htiger 的输出如下。

```
User  FailedDate  Time    Tty     Host
root    0   29-Aug-94 13:29 hft/0 tiger
```

## Time Conversion

/etc/security/lastlog 以自 epoch 以来的秒数存储时间。cvttime.c（Listing 8.2）将自 epoch 以来的秒数转换为用户可读格式，类似于 date 命令的输出。不带任何参数调用时，它返回自 epoch 以来的当前时间，单位为秒。可选标志 -f 决定应打印时间的哪些部分。格式与 C 库函数 strftime 相同。

## Logfiles Maintenance

logins shell 脚本（Listing 8.3）由 cron 每天调用一次。它检查压缩文件 sulog.MM.Z 或 wtmp.MM.Z（其中 MM 代表月份）是否已存在于目录 /var/adm/local 中。如果该文件不存在或是在去年创建的，则对应的 /var/adm 文件会被压缩并存储在 /var/adm/local 目录中。原始文件随后会被缩减为零大小。请注意，必须存在这些文件才能写入条目。

如果 /etc/security/failedlogin 的大小大于零，则文件内容会被邮件发送给系统管理员。随后该文件也会被缩减为零大小。

## Summary

这些工具使登录日志文件保持小巧，同时为参考维护最近几个月的备份副本。lastlogin 使系统管理员能够查询用户账户登录数据并自动监控用户账户。

## References

+ 1. Wood, Patrick H., and Stephen G. Kochman. *UNIX System Security*, Indianapolis, IN: Hayden Books, 1985.
+ 2. Farrow, Rik. *UNIX System Security*. Reading, MA: Addison Wesley, 1991.
+ 3. IBM. "File Reference (IBM RISC System/6000)", GC23-2200-04. 1988.

## Password Verification
in AIX v4

Thomas Richter

AIX v4 引入了控制系统访问的新工具和扩展工具。它允许系统管理员编写自己的密码验证函数，并扩展系统登录过程以调用这些新函数进行用户密码验证。它允许系统管理员为每个用户指定允许和禁止的登录时间、终端和端口，并在一定次数的登录失败后锁定账户。端口可以独立于账户进行监控：端口在登录失败后可被锁定一段时间，并在给定间隔内超过失败登录尝试阈值后可被完全关闭。锁定后的端口可在闲置一段时间后自动启用。这些功能可防止密码破解程序在同一端口上探测不同的用户 ID。

在 v4 中，密码历史记录可用。系统可防止在给定时间范围内和密码循环内重复使用密码。例如，如果密码在最近使用密码列表中，则不能重复使用。列表的大小可配置，并且可以指定字典来检查新密码。

本章探讨了 v4 中引入的登录配置和用户验证功能，然后解释如何编写和实现系统密码验证函数。

