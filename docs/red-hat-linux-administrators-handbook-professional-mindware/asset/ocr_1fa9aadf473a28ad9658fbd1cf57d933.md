The series of commands that you have to perform to arrive at this stage might look like the following:

```
```
cd /usr/src
tar xvfz linux-2.2.2.tar.gz
rm -f /usr/src/linux
ln -s linux-2.2.2 linux
```
```

> **Tip**
> When I extracted the source distribution in the /usr/src directory, it created a linux subdirectory, and therefore the symbolic link was unnecessary. However, if you plan to experiment with various kernels, I recommend that you keep a particular source distribution in the /usr/src/linux-x.x.x directory and always point a symbolic link (linux) to the kernel you are currently working on.

Although a freshly downloaded source distribution is not going to have any stale object files, it is wise to run the following command to clean up any such files just in case:

```
`make mrproper`
```

You are ready to configure (that is, customize) the kernel. You have multiple choices as to how you can customize the kernel.

# Configuring the kernel the old-fashioned way

To configure the kernel the old-fashioned way, you need to run the following command from the /usr/src/linux directory:

```
`make config`
```

This is the simplest way to configure a kernel; however, it might not be the most suitable for beginning kernel hackers. Next, I will discuss a sample kernel configuration session using the make config method. However, you should know that as features and support for various devices are added to Linux, the exact steps that make config shows also change. Therefore, what you will see in the following section might not be exactly what you see when you run make config on your system. I discuss the major decision