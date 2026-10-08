```
# ls -l /boot
total 452
-rw-r--r-- 1 root root 15954 Feb 11 1997 WHATSIN
-rw-r--r-- 1 root root 15954 Feb 11 1997
WHATSIN-2.0.29-modular
-rw-r--r-- 1 root root 204 Jul 24 1996 any_b.b
-rw-r--r-- 1 root root 204 Jul 24 1996 any_d.b
-rw-r--r-- 1 root root 512 Nov 5 01:44 boot.0300
-rw-r--r-- 1 root root 4416 Jul 24 1996 boot.b
-rw-r--r-- 1 root root 88 Jul 24 1996 chain.b
-rw------- 1 root root 7680 Nov 5 01:44 map
-r-r-r-r-- 1 root root 1565 Mar 7 1997 message
-rw-r--r-- 1 root root 192 Jul 24 1996 os2_d.b
-rw-r--r-- 1 root root 404158 Feb 11 1997 vmlinuz-
2.0.29-modular
```

![](bbox=[0.87, 0.08, 0.97, 0.18])

As a user, you are probably most concerned with your home directory, assigned to you by your system administrator, which is most likely in the /home directory. I think, however, that as a UNIX user you need to understand the overall UNIX file system layout. Keep in mind that you may find minor differences in the file system layout going from one UNIX variant to another, but in general the layout is similar.

If you're running a graphical user interface on your Linux system, you can view the file system graphically. Figure 2-2 shows the Red Hat Linux File Manager that is part of the Gnome user interface.