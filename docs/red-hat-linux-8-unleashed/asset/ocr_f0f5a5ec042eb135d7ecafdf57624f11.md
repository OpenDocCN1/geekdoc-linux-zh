# Using Red Hat's kickstart Installation Method

> > **TIP**
> 
> 
> As a general rule, it is a good idea to segregate user and system data. Although a Red Hat Linux system can be quickly restored, user data has a much greater value and can be much more difficult to replace. Segregating data can make the job of backing up and restoring him much easier.

# # Using Red Hat's kickstart Installation Method

Automating the installation process can save system administrators a lot of time and effort during an initial Red Hat Linux deployment, upgrade, or maintenance cycle by managing multiple computers at one time. Red Hat offers a highly automated installation technique called kickstart, which can be used for unattended installation of Linux.

Red Hat's kickstart installation uses a single configuration file with a special, extensive syntax on a server, boot floppy, or other medium to install Red Linux via CD-ROM, a hard drive partition, or a network connection. Using kickstart is easy and involves passing a kernel argument to the Red Hat Linux boot kernel. The various arguments tell the boot kernel to look for a configuration file on floppy, a designated server, via a network, specific file, or CD-ROM.

You can use kickstart to install Red Hat on one or more computers at the same time. First, set up a Web or FTP server with Red Hat's installation files. For directions, see the section "Installing Using a Network" in Chapter 3. Next, create a Red Hat network boot floppy using the techniques described in this chapter "Creating a Boot and Auxiliary Driver Disk" section. Follow the directions given here (choosing an FTP install) and then copy the custom kickstart file to the network boot floppy. You can then use this floppy (and copies) to boot one or more PCs to a Red Hat network install using your FTP server.

To begin the automated installation process, you create the configuration file that will be used by kickstart as an installation profile. You can configure the complex configuration file with Red Hat's Kickstart Configurator. To start the configuration, log in as the root operator, and then run the ksconfig command, like so:

```
# /usr/sbin/ksconfig
```

After you press Enter, you will see the Kickstart Configurator dialog box, as shown in Figure 2.3.

Click to select various options, and then enter the specifies for the target system. Start by selecting the default system language, type of keyboard, mouse, and so on. On course, automated installations work best when installing to similar equipment. When finished, click the Save to File button, and the configuration is saved with the name ks.cfg. When you use the kickstart installation method, the kickstart file will be read by computers booting to the install. The kickstart language covers nearly every aspect of an install with the exception of sound card, printer, or modem setup.