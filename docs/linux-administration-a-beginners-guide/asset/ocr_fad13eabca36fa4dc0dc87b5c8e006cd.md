lent performance. You may find that a box incapable of supporting Windows NT Server is more than enough for a Linux server.

Two steps are required in building a kernel: configuring and compiling. We won’t get into the specifics of configuration in this chapter, which would be difficult because of the fast-paced evolution of Linux kernel distributions. Once you understand the basic process, however, you should be able to apply it from version to version. For the sake of discussion, we’ll cite examples from the v2.2.10 kernel that we unpacked in the previous section.

# ## The make xconfig Process

The first step in building the kernel is configuring the features it contains. Usually your desired feature list will be based on whatever hardware you need to support. This of course, means that you’ll need a list of that hardware. The following command will list all hardware connected to the system via the PCI bus:

```
```
[root@ford src]# cat /proc/pci
```
```

With this list of hardware, you’re ready to start configuring the kernel. Begin by starting X-Windows with the *startx* command. Once X-Windows is up and running, enter these commands:

```
```
[root@ford ~]# cd /usr/src/linux
[root@ford linux]# make xconfig
```
```

The second command invokes the *make* utility. This development tool helps you create scripts describing all the steps necessary for compiling a program, and like many well-designed tools for UNIX other users for *make* have been found. One of these uses it to compile and execute the GUI configuration tool. Non-GUI tool exists as well and can be started with the *make config* or *make menuconfig* commands.

The *make xconfig* command displays a window like that shown in Figure 10-2. In this opening window you’ll see all the top-level configuration menus. By clicking the buttons, you can open *submenus* listing all the specific features that you can enable. A default setting exists for most options, but it is recommended that you review all settings to make sure *they’re* set as desired.

When you’ve worked your way through all the menus, click the Save and Exit button.

# ## Kernel Features and Modules

Figure 10-3 illustrates the General Setup submenu in the configuration utility. The first three columns contain the option buttons Y (Yes), M (Module), and N (No). The fourth column contains the name of the option in question, and the fifth column presents a Help button that will bring up a related window explaining the feature.

Answering Yes or No to enable or disable a kernel feature is simple enough, but let’s take a closer look at the very cool *module* configuration option. As a systems administrator, you will of course find situations where you need a kernel feature only for extremely short