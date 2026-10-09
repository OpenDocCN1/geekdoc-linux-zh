
## Kernel Options

Kernel options enable you to set the runlevel of the kernel. Some of the common kernel options are listed in the following table.

| Kernel Option | If You Need To |
| :--- | :--- |
| 1 or s | Switch to runlevel 1. |
| 2 | Switch to runlevel 2. |
| 3 | Switch to runlevel 3. |
| 4 | Switch to runlevel 4. |
| 5 | Switch to runlevel 5. |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_320_0.png)

## Types of Kernel Configuration

Linux kernels can be configured in two different ways. One form of configuration is persistent and the other is transactional.

| Kernel Configuration Type | Description |
| :--- | :--- |
| Persistent | A persistent kernel configuration refers to the configuration of kernel settings that do not change even after the system is rebooted. The changes made to the kernel are permanent. |
| | The kernel configuration with the sysctl.conf file is persistent and does not get effaced when the kernel is initialized again. |
| Transactional | A transactional configuration refers to updating the kernel settings for a required service. These settings are not permanent and are reverted when the system is rebooted. The settings hold good only for a particular transaction of the kernel. |
| | The kernel configuration with the /proc file is transactional and the changes are reflected immediately. |
| | This type of configuration can be used for network services modification and features related to memory subsystems. |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_320_1.png)

## The /proc/version File

The /proc/version file specifies the version of the Linux kernel, the GNU Compiler Collection (GCC), and the Linux distribution installed on the system.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_321_0.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_321_1.png)

**Figure 8-4:** Details displayed by the /proc/version file.

> GCC originally stood for GNU C Compiler because it was produced by the GNU project.

## The /proc Directory

The /proc is a directory in the Linux virtual filesystem, which provides elaborate information about the kernel’s running process. Some of the files in the /proc directory are listed in the table below.

| File | Description |
| :--- | :--- |
| /proc/cmdline | Contains the command line passed to the kernel by the bootloader at boot time. This file contains no information. |
| /proc/cpuinfo | Stores the CPU information and system architecture dependent items. |
| /proc/devices | Contains the list of device drivers configured into the currently running kernel. |
| /proc/filesystems | Contains the list of filesystems that are configured into the kernel. |
| /proc/partitions | Contains partition information including the major and minor number of each partition, partition name, and number of blocks. |
| /proc/ip_forward | Permits interfaces on the system to forward packets to one other. |
| /proc/meminfo | Contains memory information such as the used and unused memory on the system and the shared memory and buffers used by the kernel. |

## The sysctl Command

The sysctl command is used to view or set the kernel parameters at runtime. It has various options. Persistent kernel settings are added in the sysctl.conf file.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_322_0.png)

| Command Option | Used To |
| :--- | :--- |
| -w variable={value} | Set a parameter value or to change the sysctl setting. |
| variable={value} | Set a key parameter value. |
| -n | Disable the printing of the key name while displaying the kernel parameters. |
| -e | Ignore errors about unknown keys. |
| -a | Display all parameter values that are currently available. |
| -A | Display all parameter values that are currently available in a table format. |

```text
[root@localhost ~]# sysctl
usage:   sysctl [-n] [-e] variable ...
     sysctl [-n] [-e] [-q] -w variable=value ...
     sysctl [-n] [-e] -a
     sysctl [-n] [-e] [-q] -p <file> (default /etc/sysctl.conf)
     sysctl [-n] [-e] -A
[root@localhost ~]#
```

Figure 8-5: The different options of the sysctl command.

### Syntax

The syntax of the sysctl command is `sysctl [command options] {kernel parameter}={value}`.

## How to Customize Kernel Modules

### Procedure Reference: Load Modules Using the insmod Command

To load modules using the insmod command:

- Log in as root in the CLI.
- Enter `insmod *{module name}*` to insert a specified module into the kernel.
- Enter `modinfo [command options] {module name}` to view detailed information about the inserted module.

### Procedure Reference: View Information About the Running Kernel Modules

To view information about the running kernel modules:

- Log in as root in the CLI.
- Enter `lsmod` to view the status of all loaded modules.
- Enter `clear` to clear the terminal screen.

### Procedure Reference: Add or Remove Modules Using the modprobe Utility

To load modules using the modprobe utility:

- Log in as root in the CLI.
- Enter `modprobe *{module name}*` to add the specified module and all its dependant modules into the kernel.
- Enter `lsmod` to view the status of the loaded modules.
- If necessary, enter `modprobe -r *{module name}*` to remove a loaded module.

### Procedure Reference: Configure Modules Using the modprobe.conf File

To configure modules using the modprobe.conf file:

- Log in as root in the CLI.
- Enter `cd /etc` to navigate to the `/etc` directory.
- Enter `vi modprobe.conf` to open the modprobe.conf file.
  - Specify the parameter to pass through when the module is loaded.
  - Set the aliases for a module name.
- Save and close the file.

### Procedure Reference: Manage the Kernel Using the /etc/sysctl.conf File

To manage the kernel using the /etc/sysctl.conf file:

- Log in as root in the CLI.
- Open the /etc/sysctl.conf file.
- Make the necessary modifications to the kernel settings.
- Save and close the file.
- Reboot the system.

### Procedure Reference: Configure the Kernel Using the /proc Directory

To configure the kernel using /proc:

- Log in as root in the CLI.
- Enter `echo {value} > /proc/{file location whose value in the kernel needs to be changed}` to configure the kernel parameters.
- Save and close the file.

### Procedure Reference: Configure the Kernel Using the sysctl Command

To configure the kernel using the sysctl command:

- Log in as root in the CLI.
- Enter `sysctl [command options] {kernel parameter}={value}` to configure the kernel parameters.

## ACTIVITY 8-2
Inserting and Configuring a Kernel Module

**Before You Begin:**

1. You have logged in as root in the GUI and the terminal window is displayed.
2. Enter `cd /` to change to the / directory.
3. On the terminal window, enter `modprobe -r bcm203x` to unload the kernel module for Bluetooth devices.
4. Enter `clear` to clear the terminal screen.
5. Switch to the first terminal in the CLI.

**Scenario:**

Your colleague, Mark, tried to transfer some documents from his Linux system to his mobile device. However, he was not able to do so. After examining the system, you find that the kernel module required for the Bluetooth support is not available.

| What You Do | How You Do It |
| :--- | :--- |
| 1. Insert the bluetooth kernel module. | a. Log in as **root** in the CLI. |
| | b. Enter `insmod /lib/modules/2.6.18-53.el5/→ kernel/drivers/bluetooth/bcm203x.` to insert the bluetooth module. |
| 2. View information about the inserted bluetooth module. | a. Enter `modinfo → /lib/modules/2.6.18-53.el5/→ kernel/drivers/bluetooth/bcm203x.` to view information about the bluetooth module. |
| | b. Observe the displayed information about the loaded bluetooth module. |
| 3. Configure the bluetooth kernel module. | a. At the command prompt, enter `cd /etc` to navigate to the `/etc` directory. |
| | b. Enter `vi modprobe.conf` to open the modprobe.conf file for modification. |
| | c. Press `Shift+G` to go to the last line. |
| | d. Press `O` to switch to the insert mode and move to a new line. |
| | e. On a new line, enter `alias blue bcm203x` to specify an alias name for the bluetooth module. |
| | f. Press `Esc` to switch to the command mode. |
| | g. Save and close the file. |
| | h. Enter `logout` to log out. |
