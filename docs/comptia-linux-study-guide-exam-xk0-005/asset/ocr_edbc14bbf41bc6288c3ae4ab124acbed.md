In Figure 11.2, there are two drives used on the Linux system. The first drive on the left is associated with the root of the virtual directory. The second drive is mounted at the location /home, which is where the user folders are located. Once the second drive is mounted to the virtual directory, files and folders stored on the drive are available under the /home folder.

# **FIGURE 11.2** The Linux virtual directory structure divided between two drives

![](bbox=[0.2, 0.24, 0.8, 0.55])

Since Linux stores everything in the virtual directory, it can get somewhat complicated. Fortunately, there's a standard format defined for the Linux virtual directory, called the Linux fileystem hierarchy standard (FHS). The FHS defines core folder names and locations that should be present on every Linux system and what type of data they should contain. Table 11.3 shows just a few of the more common folders defined in the FHS.

# **TABLE 11.3** Common Linux FHS folders

| Folder | Description |
| :--- | :--- |
| /bin | Executable programs necessary for the system to run in single-user mode |
| /boot | Contains bootloader files used to boot the system |
| /dev | Device files |
| /etc | System service configuration files |
| /home | Contains user data files |
| /lib | Library files required by executable programs |