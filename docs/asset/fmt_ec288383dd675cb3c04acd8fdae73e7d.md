
```
/* Print access violation message and send email with /usr/ucb/Mail */
/* if configured to do so. */
void KickOut(void)
{
    int in;

    printf("Access to this machine RESTRICTED!!\\n");

#ifdef MAIL_TO
    if((in = open("/dev/null", O_RDONLY, 777)) != 0) {
        dup2(in, 0);
        execl("/usr/ucb/Mail", "Mail", "-s", "ACCESS VIOLATION", MAIL_TO, NULL);
        exit(1);
    }
#endif

    /* M A I N   P R O G R A M */
    main (int argc, char ** argv)
    {
        char host[MAXHOSTNAMELEN];
        uid_t gid;

        /* Block some signals */
        signal(SIGINT, SIG_IGN);
        signal(SIGTERM, SIG_IGN);

        /* Determine our hostname */
        if (gethostname(host, MAXHOSTNAMELEN))
            perror("Who am I...get me HELP!");

        /* Get the user's primary gid */
        gid = getgid();

        /* Start the user's shell if */
        /* access is allowed */
        if(CanLogin(gid, host))
            Login(argv);
        else
            KickOut();
    }
```

## Enforcing Access Restrictions

Enforcement of access restrictions is based on the system's hostname and the user's primary group ID. These policies are specified by creating a file containing access lists. The name and location of this file are determined by the definition of `ACCESS_LIST`. Each machine running `rma` must have an `ACCESS_LIST` that is owned by root with file permissions 644. The format of this file closely resembles a standard UNIX group file, which allows `rma` to use the `fgetgrent()` function to process the file. This feature greatly reduces the amount of code required for `rma`. However this similarity with the group file also has a disadvantage: there is no method for adding comments to the `ACCESS_LIST`.

`rma` looks in the equivalent of the password field for a + or a - character to determine the type of access list given for a group. A + indicates an allow list (i.e., a list of machines that group members may use), whereas a - denotes a deny list (i.e., a list of machines group members may not access). Figure 6.4 shows an `ACCESS_LIST` that

- 1. allows wheel and daemon group members to access any machine by denying access to no machines;

- 2. permits the staff group login access only to the machines named isis, bast, and horus;

- 3. restricts the sales group from logging into isis;

- 4. prohibits users with a primary group of guest from logging into any machine by not granting access to any machines.

The wheel and daemon groups, along with any other system-level groups, should be given access to all machines in a domain. Otherwise, root access may possibly be disabled, along with that of other administrative users. Although giving each machine an `ACCESS_LIST` that describes the entire domain may seem redundant, this method does ease administration. When changes are required, a new access file can be distributed to all machines with a utility like `rdist`. This method of updating the access list helps to preserve the NIS paradigm of centralized management, which `rma` does not directly support.

### Figure 6.4 A sample `ACCESS_LIST` file specifies which users can access which machines.

```
wheel:-:0:
daemon:-:1:
staff:+:300:isis,bast,horus
sales:-:101:isis
guest:+:101:
```

这些脚本有多种用途。例如，`LOGIN_SCRIPT`可用于向用户显示系统消息，而`LOGOUT_SCRIPT`可用于在注销时清理临时和 scratch 目录。当`rma`启动子 shell 时，这些脚本不会被调用。因此，例如在工作站上打开和关闭窗口不会导致登录或注销脚本被执行。

## 限制和关注点

`rma`在限制控制台登录、`telnet`、`rlogin`和`rsns`方面做得很好。不幸的是，`rma`没有提供限制`ftp`访问的功能。`ftp`守护进程从不尝试执行用户的登录 shell。与`ftp`相反，`su`会执行被`su`的用户的 shell。因此，`su`一个被禁止访问某台机器的账户会产生访问违规。`rma`代码包含一个用于处理 SunOS `su`程序的一个奇特之处的部分。SunOS 上的`su`不会将`argv[0]`重置为正在执行的 shell 的名称，因此在`Login()`函数中执行了特殊检查。如果`su`是调用程序，则 shell 的名称从`SHELL`环境变量中提取。

## 结论

`rma`看起来像是一个安全工具，但它仅用于强制执行访问策略。聪明的用户可能能够绕过`rma`的功能。这个问题在我使用的`rma`的任何变体中都没有出现。这些包括在运行 SunOS v4.1.x 和 Solaris v2.x 的工作站和服务器上运行的版本。本章讨论的`rma`版本已在 SunOS v4.1.4 和 Solaris v2.5 下测试过。虽然我没有全部测试过，但`rma`应该可以在几乎任何具有 ANSI C 编译器的 UNIX 变体上编译，只需做极少的修改。
