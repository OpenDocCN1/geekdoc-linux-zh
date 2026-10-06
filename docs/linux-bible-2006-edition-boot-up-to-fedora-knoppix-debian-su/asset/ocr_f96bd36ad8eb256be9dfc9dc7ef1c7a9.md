# Chapter 12 ♦ Running Yellow Dog Linux 379

| Option | Description |
|---|---|
| yum update | Updates all packages on the system. (Same as preceding option but does not specify package name.) |
| yum remove package | Removes the package identified in package. |
| yum info package | Provides detailed information on the package identified in package. |

Using this information, assume that you want to run gimp—GNU Image Manipulation Project (GIMP) is a very popular graphics editing program—and you haven't installed it previously. If you want to get more information on it, run:

+   - yum info gimp

If you decide to install it:

+   - yum install gimp

If an update becomes available a week later and you want to patch it:

+   - yum update gimp

If it has been a month and you decide no longer need gimp, you can remove it with the following:

+   - yum remove gimp

Yum makes updating packages very easy and should be used regularly to keep your system updated with the latest patches (you can even run it from a cron job for true automation).

# Running Mac Applications with Mac-Linux

Mac-Linux is a very interesting project that enables Mac users to have the best of both Linux and Mac. With this software, you can run Linux as the primary operating system and still access your Mac OS or OS X operating systems (even another Linux operating system) a window within your operating Linux session.

Mac-linux presents a virtual machine that provides a real environment to the Mac OS or OS X installation. Because there is no emulation, Mac-Linux is very fast and capable. Mac-Linux is very stable and works with minimal configuration. For more information on what Mac-Linux provides and on instructions for its use, visit http://maclinux.org/.