The command-line-based interface may not be elegant, but it works for most scenarios, and you should consider it the default method of configuration when the following two methods are unusable.

# Configuring the kernel using make menuconfig

One of the major problems with the make config–based configuration script is that if you make a mistake, you can't go back to fix it without starting over. Also, you can't review your choices unless you use a text editor to view the /usr/src/linux/.config file manually.

To remedy these shortcomings, the following command can be used:

```
make menuconfig
```

This runs a menu-driven configuration tool that is much more user-friendly than the make config script.

The user interface is quite simple and easy to navigate. However, the configuration questions are exactly the same. This configuration program also allows you to save and load configuration files. In other words, you can create multiple configuration files with different settings and use these configuration files to experiment with various features of the new kernel.

Although the make menuconfig script is quite friendly, it does impose some extra requirements on remote kernel configuration. For example, if you plan to configure and compile the kernel over a Telnet connection to a remote server, you have to make sure that the Telnet client program on your side is capable of good terminal emulation, which is required for a full-screen menu application. Also, make menuconfig is not the fanciest way to configure a kernel. That title goes to the make xconfig script.

# Configuring the kernel using make xconfig

As you may have guessed from the script name, this method of kernel configuration requires the X Window System. Because I do not recommend installation of the X Window System on server systems, I can't recommend this method either. However, I must say that on systems with X Window, this is the preferred method of kernel configuration. Run the Make xconfig script (wish -f scripts/kconfig.tk) from /usr/src/linux to start xconfig.