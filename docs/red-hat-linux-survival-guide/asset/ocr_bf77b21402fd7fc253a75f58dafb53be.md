# Configuring the kernel using make menuconfig

One major problem with the make config-based configuration script is that if you make a mistake, you can't fix it without starting over. Also, you can't review your choices unless you use a text editor to manually view the /usr/src/linux/.config file. To remedy these shortcomings (at least for beginning kernel hackers), use the make menuconfig utility. This runs a menu-driven configuration tool that is much more user-friendly than the make config script. The Main Menu screen is shown in Figure 11-1.

![](bbox=[0.09, 0.35, 0.75, 0.61])

Figure 11-1 The Main Menu for the make menuconfig script.

As you can see, the user interface is quite simple and easy to navigate. However, the configuration questions are exactly the same as in the make config-based configuration that I discuss in the last section (see that section for help on how to answer these questions). make menuconfig also allows you to save and load configuration files. In other words, you can create multiple configuration files with different settings and use these configuration files to experiment with various features of the new kernel.

![](bbox=[0.09, 0.84, 0.18, 0.91])

Although the make menuconfig is quite user-friendly, it imposes extra requirements on remote kernel configuration. For example, if you plan to configure and compile the kernel over a Telnet connection to a remote server, you have to make sure the Telnet client program on your side is capable