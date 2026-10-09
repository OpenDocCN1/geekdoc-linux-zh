+   * SIGEMT, representing hardware fault, is not supported.
+   * SIGINFO, representing keyboard information requests, is supported.
+   * SIGSYS, representing invalid system call, is not supported.
+   * SIGABRT and SIGIOT are identical.
+   * SIGIO, SIGPOLL, and SIGURG are identical.
+   * SIGBUS is defined as SIGUNUSED because there is no “bus error” in Linux.

Table 5.2 lists various signals and their meaning in Solaris and Linux environments. This table can be used to verify if the signals used in your code have different semantics in Linux.

Table 5.2: Semantics of Signals in Solaris and Linux

| Signal | Solaris | Linux |
| :--- | :--- | :--- |
| SIGHUP | Terminate | Ignore |
| SIGINT | Terminate | Ignore |
| SIGQUIT | Terminate, core | Terminate, core |
| SIGILL | Terminate, core | Terminate, core |
| SIGTRAP | Terminate, core | Ignore |
| SIGABRT | Terminate, core | Terminate, core |
| SIGEMT | Terminate, core | Not supported on Linux |
| SIGFPE | Terminate, core | Terminate, core |
| SIGKILL | Terminate | Terminate |
| SIGBUS | Terminate, core | Terminate, core |
| SIGSEGV | Terminate, core | Terminate, core |
| SIGSYS | Terminate, core | Not supported on Linux |
| SIGPIPE | Terminate | Ignore |