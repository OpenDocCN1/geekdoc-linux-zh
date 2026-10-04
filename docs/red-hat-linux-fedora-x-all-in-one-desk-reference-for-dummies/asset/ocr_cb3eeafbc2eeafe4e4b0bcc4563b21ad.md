# 498 Rebuilding the Kernel

# Configuring the kernel

The first phase in rebuilding a kernel is to configure it. To configure the kernel, log in root. Then change the kernel source directory by using the command as follows:

```
cd /usr/src/linux*
```

To configure the kernel, you have to indicate which features and device drivers you want to include in your Linux kernel. In essence, you will build your own version of the Linux kernel with just the features you want.

Fedora Core provides several ways for you to configure the kernel:

+   **Type make menconfig** to enter the kernel-configuration parameters through a text-based interface similar to the Fedora Core installation programs.

+   **Type make xconfig** to use an X Window System-based configuration program to configure the kernel. You have to run X to use this configuration program with a graphical interface.

+   **Type make config** to use a script that prompts you for each configuration option, you one by one. You can use this configuration program from the Linux command prompt. When you use this option, you undergo a long question-and-answer process to specify the configuration parameters. For each question, respond with a y to link into the kernel, m to build a module, and n to skip the skip for that specific device.

The makeconfig, make xconfig, and make config commands achieve the same result — each stores your choices in a text file .config located in the /usr/src/linux/ directory. Because the filename starts with a period, you don't see it when you use the ls command alone to list the directory. Instead, type ls a to see the .config file in the directory.

The kernel-configuration merely captures your choices in the .config file. (In fact, the .config file does not exist until you configure the kernel once.) The kernel file does not change until you compile the kernel with the make command. That means you can go through the kernel-configuration option as many times as you want. If you want to start with default settings, type the following command before you start configuring the kernel:

make mrproper

For an overview of the kernel configuration build steps that you can perform with the make command, following the terminal in a window (after you type cd /usr/src/linux* to change the current directory to the correct location):

make help | more

![](bbox=[0.165, 0.699, 0.265, 0.784])

![](bbox=[0.165, 0.849, 0.235, 0.919])