
![](img/9129877170834ca9d5fdac5319bf5f12_609_0.png)

If you do not include the key in the initrd, AutoYaST installations will ignore the files in the updates directory unless you include instructions in your AutoYaST control file to accept unknown keys:

```
<general>
<signature-handling>
<accept_unknown_gpg_key
config:type="boolean">true</accept_unknown_gpg_key>
</signature-handling>
```

8. During installation, select Add-on Products and then Add to be able to select your packages in the Software dialog.

## Configure the NFS Server

To make a directory available via NFS, you need to complete the following steps:

1. Edit the /etc/exports file. This file defines which directories are shared with which machines. You can also define restrictions; for example, you could make a directory read-only. To find out more about the syntax of the file, have a look at the output of the command man 5 exports.

An entry to make the /export/sled10 directory available to all machines in read-only mode looks like the following:

```
/export/sled10 *(ro,sync)
```

![](img/9129877170834ca9d5fdac5319bf5f12_609_1.png)

To find out about other options that can be used in that file, have a look at the manual page with the man 5 exports command.

2. Start the NFS server by entering
rcnfsserver start

3. Make sure the NFS server is started automatically when the system boots up by entering
insserv nfsserver

4. (Conditional) If SuSEFirewall is running, you have to start YaST, select Security and Users > Firewall, and add NFS Server within the Allowed Services dialog. If you omit these steps, clients might be unable to connect to your NFS server.

## Use the Installation Server

To use the installation server, you have to specify the server when the initial boot screen shows up. With the Down key, move to Installation; press F3 and then F4. In the menu, select the installation server type you want to use, as shown in Figure 15-4.

![](img/9129877170834ca9d5fdac5319bf5f12_610_0.png)

Figure 15-4

In the dialog that appears, enter the hostname of the server and the directory on the server. Depending on the server type, you might need to enter additional parameters.

Instead of choosing NFS in the menu and entering the IP address and path in the dialog, you can type `install=nfs://IP_address/path/` in the Boot Options line.

After you press Enter, the installation system connects to the installation server and loads all files needed for installation over the network.

![](img/9129877170834ca9d5fdac5319bf5f12_611_0.png)

## Exercise 15-2: Set Up an Installation Server

In this exercise, you copy the files of the installation DVD to a directory and make this directory accessible over the network using NFS.

Create the /export/sled10 directory. Copy all files from the DVD to this directory. Edit /etc/exports and start the NFS server to make these files accessible over the network.

### Detailed Steps to Complete This Exercise

To set up an installation server, do the following:

- 1. In a terminal window, run the su -- command to switch to root (password n0v311).
- 2. Create the /export/sled10 directory by entering
  `mkdir -p /export/sled10`
- 3. Insert the SUSE Linux Enterprise Desktop DVD. Copy the content of the DVD to the directory you just created by entering
  `cp -a /media/mountpoint/* /export/sled10`
- 4. Because copying the content will take some time, open another terminal window and switch to root (su -, password n0v311).
- 5. Edit the /etc/exports file to add the following line:
  `/export/sled10 *(ro,sync)`
- 6. Start the NFS server by entering
  `rcnfsserver start`
- 7. Make sure the NFS server is started each time the system starts up by entering
  `insserv nfsserver`

You can also use the YaST Runlevel Editor instead of insserv.

## Objective 5—Automated Installation

To start the automated installation, make the AutoYaST control file available on the machine to be installed. This can be combined with any installation method, be it from the installation media, or an installation server in the network.

To perform automated installations, you need to:

- Provide the Control File
- Boot and Install the System

### Provide the Control File

Various ways exist to make the control file available.

One way is to copy the file to a floppy disk containing a FAT file system format.

![](img/9129877170834ca9d5fdac5319bf5f12_612_0.png)

Do not use a floppy disk with Ext2 file system format.

If you name the file on the floppy disk autoinst.xml and insert the floppy, it will be automatically used. If you use a different name, you have to add the following to the kernel command line at the boot prompt of the installation:

```
autoyast=floppy:///myconfig.xml
```

Another way to make the control file available is via the network. That is especially useful in combination with an installation server. In this case, the kernel command line would look similar to the following:

```
autoyast=nfs://10.0.0.254/export/sled10/myconfig.xml
```

### Boot and Install the System

Once you have your control file created and tested, you have several options to install machines with it:

- Boot and Install from DVD
- Boot from DVD, Install from an Installation Server
- Boot via PXE, Install from an Installation Server

### Boot and Install from DVD

It is possible to use a control file (on a floppy disk or on an exported file system) in combination with the installation DVD to boot and install the computer. However, for larger deployments, this is not really efficient. While it saves the typing of configuration information, you still have to walk from computer to computer, insert the media, and start the installation manually. Later, you have to come back to remove the installation media again.

### Boot from DVD, Install from an Installation Server

Even when using the DVD or a floppy to boot, an installation server has the advantage that you can remove the boot media as soon as the actual installation has started.

Provided you have a DHCP server running that provides all network information during installation, the steps are as follows:

- 1. Insert the installation DVD into your machine and start the boot process.
- 2. On the first boot screen, select Installation (be sure to do this within 10 seconds; otherwise, the system starts from hard disk).
- 3. Provide the information that you want used with AutoYaST.

At the boot prompt, enter the following parameters (we assume here that the installation repository is available via NFS from 10.0.0.254/export/sled10/, and that the control file is available at the same location):

```
autoyast=nfs://10.0.0.254/export/autoinst.xml
install=nfs://10.0.0.254/export/sled10
splash=verbose
```

The last parameter switches to the detailed display during the boot process, so you can easily look at the boot messages.

After a short time, YaST starts. At this point, you can remove the boot medium. The installation proceeds as usual, but because of the control file, no user interaction is necessary. After some checks, the packages are copied from the NFS server.

The system is rebooted at the end of the installation process. After the reboot, you may log in as root without a password if no password was set in the AutoYaST configuration file. In this case, you should immediately set a password for root.

### Boot via PXE, Install from an Installation Server

The advantage of using PXE for installation is that you do not have to bring a separate boot medium to the computer. With a suitable configuration, you can offer a menu to select what to install.

In fact, if the network card supports Wake on LAN, you do not have to walk to the machine at all.

The setup to support booting via the network is not covered in this course. Information can be found in /usr/share/doc/packages/autoyast2/autoyast.pdf.

![](img/9129877170834ca9d5fdac5319bf5f12_613_0.png)

## Exercise 15-3: Perform an Automated Installation of SLED 10

In this exercise, you perform an automated installation of SUSE Linux Enterprise Desktop 10.

If you have any files on your machine that you created during the course and that you want to keep, copy them to an external medium (such as a USB stick), because they will be gone after this exercise.

In this exercise, you work with a partner. One machine serves as the installation server; the other one will get reinstalled.

If no partner is available (in a self-study environment, for example), you can set up the installation server on the da1 virtual machine, or use the DVD as installation medium.

### Detailed Steps to Complete This Exercise

To start the installation of SUSE Linux Enterprise Desktop 10, do the following:

- 1. Decide which machine you will use as the installation server and which machine will be rebooted.
- 2. On the machine that will act as installation server, create the /export/sled10/autoyast/ directory and copy the autoyast file into this directory as sled10.xml.
