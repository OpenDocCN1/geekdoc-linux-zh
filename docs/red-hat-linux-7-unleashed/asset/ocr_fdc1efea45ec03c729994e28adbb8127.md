Unfortunately, the SIOG doesn't tell you which numbers correspond to which sections of code. Instead, the author suggests that keeping such documentation current is a lot of work (which it is), and that you should look at the code itself to discover the correct debugging formulas.

The function `tfd()` is the one to look for. For example, suppose you want to turn on debugging in sendmail's address-parsing code. The source file *parsaddr.c* contains most of this code, and the following command finds the allowable debugging levels:

```
```
$ egrep tfd parsaddr.c
            if (tfd(20, 1))
[...]           if (tfd(24, 4))
                if (tfd(22, 11))
[etc.]
```
```

The egrep output shows that debugging specifications such as -d20.1, -d24.4, and -d22.11 (and others) will make sense to sendmail.

If perusing thousands of lines of C code doesn't appeal to you, the O'Reilly book, *sendmail, Second Edition*, documents the debugging flags for sendmail. Note that the book only covers up to sendmail-8.8; small differences in detail could exist but it is still a good reference.

The -C option enables you to test new configuration files before you install them, which is always a good idea. If you want to test a different file, use -C *path/to/the/file*. You can combine it with the -bt and -d flags. For example, a common invocation for testing new configuration files is

```
`/usr/sbin/sendmail -Ctest.cf -bt -d21.12`
```

**Caution**

For security, sendmail drops its superuser permissions when you use the -C option. You should perform final testing of configuration files as the superuser to ensure that your testing is compatible with sendmail's normal operating mode.

# ## Automatically Generating the sendmail.cf File

Luckily, these days no one has to manually edit a sendmail.cf file. Enter the following command:

```
```
[root@gonzo /]# rpm -q sendmail -cf
sendmail-cf-8.11.0-8
```
```