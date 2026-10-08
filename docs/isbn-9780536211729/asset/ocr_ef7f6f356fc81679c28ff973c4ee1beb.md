> According to SANS on March 23, 2000, there have been reports that deja.com still was not filtering these possible exploits out of Usenet News postings that it serves up.

# ### B.28 Format Problems with syslog()

![](bbox=[0.1, 0.25, 0.98, 0.33])

The `syslog()` routine enables programs to generate entries that will be logged to disk by `syslogd`, the standard Linux error logging mechanism. Its first argument is a priority and its subsequent arguments are interpreted similarly to those of `printf()` or `sprintf()`. For unvarying messages, this second argument may be a simple string constant. Unfortunately, some standard Linux programs instead use a string variable, containing arbitrary user data as the second argument. This problem was discovered by the Linux auditing project, which is sure to discover other problems and fixes; a similar project for the BSD UNIX code was quite successful.

This problem also may exist in privileged programs that use other variants of the `printf()` family, including `fprintf()`, `sprintf()`, and even `v*printf()`. This allows a variety of exploits, including buffer overflow attacks. A clever cracker also may provide a “format string” that causes arbitrary areas of memory, perhaps containing confidential data, to be printed to log files that might be world-readable. At the present time, the names of the programs affected have not been made public. The following `find` command, invoked at the root of your system’s source tree, will find most lines containing this problem; the appropriate directory usually is `/usr/src`.

```
```
find . -name '*. [hc]' -print | xargs -n 50 grep \
'syslog *([^"]*, *[^"`]) *([^"`])*' /dev/null
```
```

As you can see, it finds each C source and include file (`*. [hc]`) and invokes `grep` to find each one that invokes `syslog()` with only two arguments, where the second argument is not a string literal. It uses `xargs` to fork `grep` only once for every 50 source files, rather than for each file. This dramatically improves performance.

> The programs `gdm`, `rpc.statd`, and vopmail's `vchkpw` (prior to version 4.8) are known to have this formatting problem. The `inn` program and other RPC programs might have the problem too, as may other programs.