![](bbox=[0.17, 0.14, 0.86, 0.45])

# Customizing the uClibc configuration

The previous section used Buildroot to build a uClibc-based toolchain, using the default uClibc options for our target architecture. These default options are very reasonable, and it is recommended you stick with them, at least in your first attempt to build a uClibc-based system.

Having said that, we recognize it is sometimes desirable to fine-tune and optimize certain options in the uClibc configuration itself. This can be done through Buildroot, after it is configured using the procedure outlined in the previous section, by issuing the following command:

```
$ make uclibc-menuconfig
```

You will be presented with the uClibc configuration menu, which includes the following submenus and options:

+   Target Architecture
+   Target Architecture Features and Options
+   General Library Settings
+   Advanced Library Settings
+   Networking Support
+   String and Stdio Support