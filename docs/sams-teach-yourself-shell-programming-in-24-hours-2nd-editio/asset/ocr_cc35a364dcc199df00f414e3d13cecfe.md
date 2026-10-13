# Using uname to Determine the UNIX Version

The first step in writing portable shell scripts is to determine which version of UNIX is executing your shell script. This can be determined this using the uname command:
`uname options`

Here, options is one or more of the options given in Table 23.2.

**TABLE 23.2 Options for the uname Command**

| Option | Description |
|---|---|
| -a | Prints all information |
| -n | Prints the current hardware type |
| -n | Prints the hostname of the system |
| -r | Prints the operating system release level |
| -s | Prints the name of the operating system (default) |

![](bbox=[0.22, 0.62, 0.3, 0.68])

> On SunOS, the -a option of uname displays summary information about the system. To get complete information, use the -X option of uname.

By default, the uname command prints the name of the operating system. The output looks like the following:

```
$ uname
Linux
```

Here, the output indicates that the operating system name of the machine is Linux. Usually, this is enough to determine the UNIX version, as you can see from the values listed in Table 23.3.

**TABLE 23.3 Selected UNIX Version names as Displayed by uname**

| Name | Description |
|---|---|
| Linux | A system running Linux |
| HP-UX | A system running Hewlett-Packard's HP-UX |
| FreeBSD | A system running FreeBSD |
| OpenBSD | A system running OpenBSD |
| Darwin | A system running Apple's MacOS X |
| SunOS | A system running Sun Microsystem's SunOS (BSD based) or Solaris (System V based) |