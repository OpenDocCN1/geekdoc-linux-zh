*continued*

gather. Follow the system prompts, entering the information as it is presented: You are asked to select a language and locale. You’ll also need to enter your system’s hostname, IP address, and network information, so have this information available.

3. After the system identification section, you’ll see the following dialogue:

Solaris Interactive Installation:

```
This system is upgradable, so there are two ways to install the Solaris software.

The Upgrade option updates the Solaris software to the new release, saving as many modifications to the previous version of Solaris software as possible. Back up the system before using the Upgrade option.

The Initial option overwrites the system disks with the new version of Solaris software. This option allows you to preserve any existing file systems. Back up any modifications made to the previous version of Solaris software before starting the Initial option.
```

After you select an option and complete the tasks that follow, a summary of your actions will be displayed.

```
F2_Upgrade    F4_Initial    F5_Exit    F6_Help
```

4. Press F4 to select a complete reinstallation of the software. You’ll see the following dialog:

```
You'll be using the initial option for installing Solaris software on the system. The initial option overwrites the system disks when the new Solaris software is installed.
```

On the following screens, you can accept the defaults or you can customize how Solaris software will be installed by:

+   - Selecting the type of Solaris software to install
- Selecting disks to hold software you've selected
- Specifying how file systems are laid out on the disks

After completing these tasks, a summary of your selections (called a profile) will be displayed.

5. Press F2 to continue.

> CAUTION
All data on the operating system partitions will be lost. These partitions include / (root), /usr, /opt, and /var.

> NOTE
Because you want a complete reinstallation of the software, you'll select F4. The upgrade option is available if you are currently running Solaris 7 and you want to upgrade to Solaris 8. With the upgrade option, all customizations you made in Solaris 7 will be saved.