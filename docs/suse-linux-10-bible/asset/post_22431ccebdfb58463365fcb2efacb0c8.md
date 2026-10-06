
## 118 Part II + The SUSE System

The ckconfig command takes a few arguments that you will probably use quite a lot. To list all of the applications in runlevels that are controlled by init with details of whether they are on (started in a runlevel) or off (not started in a runlevel), you can just run ckconfig --list.

When you are viewing the output of ckconfig -list, you will see a list of all processes controlled by init with their status on the screen. You can use the pipe ( | ) to push the output through by issuing ckconfig -list | |. This will enable you to move up and down with the cursor keys and see all of the output regardless of whether it is longer than the screen you are viewing it. This is something that can be used with any textual output that scrolls past because there is too much data. You can read more about list and other command-line interfaces you might want to perform on a regular basis in Chapter 2.

The ckconfig -list produces a useful summary of what is running in your runlevels. If this is the case, you can stop services from loading in your runlevel by using ckconfig -d service (delete) to turn off the named service. Similarly, you can use ckconfig -a service (add) to add a service to a multiuser. As a shortcut, you can use the command ckconfig service to activate or deactivate (off) the named service at all multiuser runlevels. To specify that a named service is started at one or more specific runlevels, you can append those ckconfig commands configure your system to start the apache server at runlevels 3 and 5:

```
ckconfig apache2 3
ckconfig apache2 35
```

When explicitly specifying the runlevels at which Apache should start, the command is implied.

## Customizing Runlevels for Different Types of Systems

As a general rule, if you are running a server using SUSE (or any other operating system for that matter), you turn off any services that are not needed for the running of that specific server. For example, if you were running a web server for your organization, you would not run X Windows because it is not needed to run Apache. In this situation, you would probably run in a default runlevel of 3 (multiuser, with network, no X Windows) and turn off (or remove) any non-essential services using the ckconfig program. Listing 4-1 shows the output of ckconfig-list after you have turned off any services that are not needed to run Apache.

### Listing 4-1: Output of chkconfig -list with a Customized Runlevel

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|---|
| apache2 | 0off | 1off | 2off | 3can | 4off | 5can | 6off |
| cron | 0off | 1off | 2can | 3can | 4off | 5can | 6off |
| fleetd | 0off | 1can | 2can | 3can | 4off | 5can | 6off |
| kswapd | 0off | 1can | 2can | 3can | 4off | 5can | 6off |
| network | 0off | 1off | 2off | 3can | 4off | 5can | 6off |
| ndis | 0off | 1off | 2can | 3can | 4off | 5can | 6off |
| postfix | 0off | 1off | 2can | 3can | 4off | 5can | 6off |
| ramdd | 0off | 1off | 2off | 3can | 4off | 5can | 6off |
| rsysgrd | 0off | 1off | 2can | 3can | 4off | 5can | 6off |
| splash | 0off | 1can | 2can | 3can | 4off | 5can | 6off |
| splash early | 0off | 1off | 2can | 3can | 4off | 5can | 6off |
| splash late | 0off | 1off | 2can | 3can | 4off | 5can | 6off |
| sshd | 0off | 1off | 2can | 3can | 4off | 5can | 6off |
| syslog | 0off | 1off | 2can | 3can | 4off | 5can | 6off |

If you are customizing a runlevel for a specific purpose (again, for Apache in this example), you should choose the runlevel that is closest in principle to what you need to run for Apache and customize it to your situation. Because we do not need X Windows, but we do need a multiuser system with networking, we choose 3 as a default and then customize it down.

## Boot Managers

We will now go back to the beginning of the boot process and talk about boot managers. As you saw earlier in the chapter, the boot loader helps the system load other operating systems. You should see it as a stepping stone from the BIOS to the operating system itself.

Two boot loaders are used in Linux — the traditional LILO boot loader and the newer GRUB boot loader.

## LILO

The Linux Loader (LILO) was one of the first boot loaders available for Linux. It is a relatively simpler loader that was designed for the start for simplicity and stability. One downside to using LILO is that its configuration information is stored in the MBR (Master Boot Record) for your primary hard drive. Any changes you make to the configuration means that your MBR has to be updated every time. Changing your MBR is something that should not be taken lightly because if you corrupt it, the system will not boot. The MBR is what the BIOS looks for a hard disk to see it can boot from it. If this is corrupt or does not exist, the BIOS will not boot from the media.

The configuration file for LILO is stored in /etc/lilo.conf. The layout of the lilo.conf file is relatively easy to read, and we set up a simple LILO configuration for a Linux system and a Windows system for dual-booting purposes (see List 4-2).

The lilo.conf file has a general configuration section that sets default values for LILO, followed by specific entries for different boot configurations that can be used to boot operating systems. Each boot configuration in the lilo.conf is referred to as a boot profile because.

### Listing 4-2: Sample lilo Configuration

```
message = /boot/message
timeout = 80
prompt
default = Linux

image = /boot/vmlinuz
label = Linux
initrd = /boot/initrd
root = /dev/hda3
append = "noresume nosmp"

image = /boot/vmlinuz
label = Windows
initrd = /boot/initrd
root = /dev/hda
```

## 120 Part II ♦ The SUSE System

### Chapter 4 ♦ Booting the System

### Table 4-3: Sample lilo Configuration Description

| lilo Parameter | Description |
|---|---|
| boot = /dev/hda | Defines the default device for the system. |
| default = Linux | If there has no user intervention, this is the profile that is loaded when the timeout value has been exceeded. |
| image = /boot/vmlinuz | The kernel image for the profile. |
| initrd = /boot/initrd | The initial ramdisk for this configuration. |
| label = Linux | The name of the profile. This is used to select this profile at the prompt. |
| other=/dev/hda2 | To boot "other" operating systems, you can specify the other class. LILO will load and execute the boot sector of the specified partition at boot time. As with the standard Linux profile, a label can be added to allow to load the profile for a specific operating system, in this case, Windows. |
| message | Defines the file containing a text message that is displayed by LILO. |
| prompt | Causes LILO to display its prompt, enabling you to select a nondefault boot profile. |
| root = /dev/hda3 | The root filesystem used for this profile. This is the / (root) partition that we discussed earlier in the chapter. |
| timeout = 80 | The timeout value until the default profile is used when there no user intervention. |

When the edit of the lilo.conf file configuration has been completed, you then need to commit those changes to the MBR on the hard disk by typing lilo at the command prompt. Adding -v to the lilo command line will print out verbose messages describing what lilo is doing. This is an intricate part of the system, we recommend always run lilo with the -v option to make sure it executed successfully and diagnose any problems you may find.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_165_0.png)

In general, Linux commands support a -v (verbose) option. When you are first learning Linux, using the -v option with commands such as mv, chown, and others can help you see exactly what a command is doing, especially if you are using a single command to work with multiple files, such as the contents of a directory.
