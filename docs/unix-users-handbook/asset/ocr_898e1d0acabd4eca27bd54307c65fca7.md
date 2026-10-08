# shutdown

# **shutdown - Terminate all running processes in an orderly fashion.**

![](bbox=[0.85, 0.13, 0.97, 0.25])

shutdown(1M)

shutdown(1M)

**NAME**
shutdown - terminate all processing

**SYNOPSIS**

```
```bash
/sbin/shutdown [-h|-r] [-y] [-o] [grace]
```
```

**DESCRIPTION**
The shutdown command is part of the HP-UX system operation procedures. Its primary function is to terminate all currently running processes in an orderly and cautious manner. shutdown can be used to put the system in single-user mode for administrative purposes such as backup or file system consistency checks (see fsck(1M)), and to halt or reboot the system. By default, shutdown is an interactive program.

Options and Arguments
shutdown recognizes the following options and arguments.

+   -   **-h**
    Shut down the system and halt.

-   **-r**
    Shut down the system and reboot automatically.

-   **-Y**
    Do not require any interactive responses from the user. (Respond yes or no as appropriate to all questions, such that the user does not interact with the shutdown process.)

-   **-o**
    When executed on the cluster server in a diskless cluster environment, shutdown the server only and do not reboot clients. If this argument is not entered the default behavior is to reboot all clients when the server is shutdown.

-   **grace**
    Either a decimal integer that specifies the duration in seconds of a grace period for users to log off before the system shuts down, or the word now. The default is 60. If grace is either 0 or now, shutdown runs more quickly, giving users very little time to log out.

If neither -r (reboot) nor -h (halt) is specified, standalone and server systems are placed in single-user state. Either -r (reboot) or -h (halt) must be specified for a client; shutdown to single-user state is not allowed for a client. See dcnodes(1M), init(1M).

**Shutdown Procedure**
shutdown goes through the following steps:

+   -   The PATH environment variable is reset to /usr/bin:/usr/sbin:/sbin.
-   The IFS environment variable is reset to space, tab, newline.