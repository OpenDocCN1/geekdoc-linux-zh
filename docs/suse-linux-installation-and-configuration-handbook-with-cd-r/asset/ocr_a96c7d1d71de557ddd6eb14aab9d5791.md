# Checking Your Kernel's Version

Now that you know how to read a kernel's version properly, how do you find out the version of the kernel you are running now? This piece of information might come in handy if you want to know whether there is a newer version of the kernel than yours. The most obvious way is to read it off the login prompt of your Linux machine. If you have configured your Linux to boot in console mode, you will spot the version of the kernel just above the login prompt. Another method you could use is by running the uname command like this:

```
$ uname -r
2.2.13
```

The uname utility, when run with the -a switch, outputs information about the version of the kernel currently running on the system. Here you see that my system is called mymachine and is running kernel 2.2.13. Thanks to your newly acquired knowledge you can quickly tell that this is a stable kernel.

# Checking for the Latest Version of the Kernel

You now know how to read a kernel's version, and you know how to check the version of the kernel you are running. Next, you should know how to check whether you have the latest version of the kernel or if there is a newer one. There are many ways to find this information; major Linux sites announce the release of a new kernel as soon as it happens. These sites even list the new features and drivers included with the new release. Freshmeat (http://www.freshmeat.net) and Linux Today (http://www.linuxtoday.com) are just two of many sites that announce new kernel releases.

Another way you can instantly check for the latest version of the kernel is by using the finger command like this:

```
$ finger @ftp.kernel.org
[linux.kernel.org]
```

```
The latest stable version of the Linux kernel is:      2.2.13
The latest beta version of the Linux kernel is:      2.3.23
The latest prepatch (alpha) version *appears* to be: none
```

From this information along with the output of the uname command, you can tell that you are not running the latest version of the kernel.

> **TIP**
> Most users, upon finding out that a new kernel has been released, rush off to install it. Always remember the golden rule for this: If it's working fine, leave it as is. In other words, if you don't need to upgrade, don't upgrade.