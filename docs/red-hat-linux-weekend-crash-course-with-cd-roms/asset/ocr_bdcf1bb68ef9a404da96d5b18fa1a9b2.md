Red Hat provides a generic kernel along with a large number of modules to support many different types of hardware. Then, the installation program configures the system to load only those modules that are needed to support the hardware installed in a user's system.

![](bbox=[0.18, 0.24, 0.3, 0.32])

> When you create a custom kernel for your hardware configuration, you may link in all required device drivers into the kernel. You can keep the size of such a monolithic kernel under control because you only link in device drivers for the hardware actually installed on your system.

# Configuring the Kernel

The first phase in rebuilding a kernel is configuring the kernel. To configure the kernel, log in as root. Then change the directory to /usr/src/linux by using the cd command as follows:

```
cd /usr/src/linux
```

To configure the kernel, you have to indicate the features and device drivers (covered in the previous section) that you want to include in your Red Hat Linux system. In essence, you build a copy of Linux with the mix-and-match features that you want.

Red Hat Linux provides three ways for you to configure the kernel:

+   - Type make menuconfig to enter the kernel configuration parameters through a text-based interface, similar to the one used by the Red Hat installation program.
+   - Type make xconfig to use an X Window System-based configuration program to configure the kernel. You have to run X to use this configuration program with a graphical interface.
+   - Type make config to use a program that prompts you for each configuration option one by one. You can use this configuration program from the Linux command prompt. When you use this option, you undergo a long question-and-answer process to specify the configuration parameters.

As you configure the kernel, you have to select how to include support for specific devices. Typically, for each configuration option, you must type one of the following choices:

+   - y to link support into the kernel