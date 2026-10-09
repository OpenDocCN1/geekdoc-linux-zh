```
# brandelf /bin/sh
File '/bin/sh' is of brand 'FreeBSD' (9).
```

No surprise there. This is a FreeBSD binary, so it'll be executed under the FreeBSD ABI. Let’s try a Linux binary:

```
# brandelf /usr/compat/linux/bin/sh
File '/usr/compat/linux/bin/sh' is of brand 'Linux' (3).
```

See the brands FreeBSD supports with the -1 flag.

```
# brandelf -1
known ELF types are: FreeBSD(9) Linux(3) Solaris(6) SVR4(0)
```

If you have a foreign program that won’t run, check its branding. If it isn’t branded or is branded incorrectly, you’ve probably discovered your problem: FreeBSD is trying to run the program under the native FreeBSD ABI. Change this by setting the brand manually with brandelf - t. For example, to brand a program Linux, do this:

```
# brandelf -t Linux /usr/local/bin/program
```

The next time you try to run the program, FreeBSD will run it under the Linux ABI and the Linux userland, and the program should work as expected.

You can also use sysctls to set a fallback brand. All FreeBSD binaries get branded properly, but random programs you copy to your host might not be. Unbranded binaries get treated with the chosen fallback brand. The sysctl kern.elf32.fallback_brand gives a fallback brand for 32-bit hosts, while kern.elf64.fallback_brand sets the fallback brand for 64-bit hosts. This sysctl takes the brand’s numerical identifier, which for Linux is 3.

```
# sysctl kern.elf64.fallback_brand=3
```

You should now be able to run Linux programs without any further configuration. All that’s left are the minor annoyances and peccadilloes of Linux mode. Sadly, there’s a few of those, as we’ll illustrate next.