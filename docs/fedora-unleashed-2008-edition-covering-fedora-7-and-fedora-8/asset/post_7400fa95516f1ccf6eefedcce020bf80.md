
Make sure that the desired mount point exists before using the mount command. When you finish using the directory (perhaps for copying backups), you can use the umount command to remove the remote file system. Note that if you specify the root directory (/) as a mount point, you cannot unmount the NFS directory until you reboot (because Linux complains that the file system is in use).

## Putting Samba to Work

Samba uses the Session Message Block (SMB) protocol to enable the Windows operating system (or any operating system) to access Linux files. Using Samba, you can make your Fedora machine look just like a Windows computer to other Windows computers on your network. You do not need to install Windows on your PC.

Samba is a very complex program—so much so that the book *Samba Unleashed* (Sams Publishing, 2000, ISBN 0-672-31862-8) is more than 1,200 pages long. The Samba man page (when converted to text) for just the configuration file is 330KB and 7,013 lines long. Although Samba is complex, setting it up and using it does not have to be difficult. There are many options, which account for some of Samba's complexity. Depending on what you want, Samba's use can be as easy or as difficult as you would like it to be.

Fortunately, Fedora includes two tools: a simplified Samba management tool called system-config-samba, and a much more advanced tool known as SWAT (Samba Web Administration Tool), which can be used to configure Samba with a web browser. SWAT provides an easy way to start and stop the Samba server; set up printing services; define remote access permissions; and create Samba usernames, passwords, and shared directories. This section delves into the basics of configuring Samba, and you should first read how to manually configure Samba to get an understanding of how the software works. At the end of this section, you will see how to enable, start, and use SWAT to set up simple file sharing.

Like most of the software that comes with Fedora, Samba is licensed under the GPL and is free. It comes as both an RPM and as source code. In both cases, installation is straightforward and the software can be installed when you install Fedora or use RPM software packages. The Samba RPMs should be on one of your Fedora install disks, or the latest version can be downloaded from the Internet, preferably from the Fedora Project (at http://fedoraproject.org/) or an authorized mirror site.

Installing from source code can be more time-consuming. If you do not want to install Samba from Fedora's default locations, however, installing from the source code is a more configurable method. Just download the source from http://www.samba.org/ and unpack the files. Change into the source directory and, as root, run the command `./configure` along with any changes from the defaults. Then run `make`, `make test` (if you want), followed by `make install` to install Samba in the specified locations.

If you install Samba from your Fedora DVD, you can find a large amount of documentation in the directory tree, starting at `/usr/share/doc/samba*/doc/` in several formats, including PDF, HTML, and text, among others. Altogether, almost 3MB of documentation is included with the source code.

![](img/34e72348d53ca54c2a1d9c871316691b_448_0.png)

After Samba is installed, you can either create the file `/etc/smb.conf` or use the `smb.conf` file supplied with Samba, which is located by default under the `/etc/samba` directory with Fedora. Nearly a dozen sample configuration files can be found under the `/usr/share/doc/samba*/examples` directory.

> **NOTE**
> Depending on your needs, `smb.conf` can be a simple file of fewer than 20 lines or a huge file spanning many pages of text. If your needs are complex, I suggest picking up a copy of *Using Samba, 3rd Edition* by Carter, Ts, and Eckstein (O'Reilly, 2007).

## Configuring Samba with system-config-samba

Fedora benefits from a slew of utilities that were developed as part of the original Red Hat Linux. Fortunately, work has carried on after Red Hat Linux was discontinued and the Samba configuration tool has lived on. And although it hasn't undergone major enhancements since Fedora Core 1, it is still a very useful tool to have to hand when configuring basic Samba services.

You can access it under System, Administration, Samba, and the opening screen is shown in Figure 19.2.

![](img/34e72348d53ca54c2a1d9c871316691b_449_0.png)

FIGURE 19.2  system-config-samba, a great way to get up and running quickly with Samba.

To get started, just click the Add Share icon in the toolbar, or select Add Share from the File menu. Either way takes you to the basic settings screen shown in Figure 19.3.

![](img/34e72348d53ca54c2a1d9c871316691b_450_0.png)

FIGURE 19.3 Click the Browse button to locate the folder you want to share.

In the basic settings, you need to provide the path to the folder that you want to share via Samba. You also need to give it a share name, and an optional description. If you plan on setting up a number of shares, you might want to consider filling out the description to help you distinguish between them all.

Next up you need to select one or both of the check boxes to allow users to view (visible) and or write (writable) to the folder. Subdirectories underneath the specified directory inherit the permissions stated here.

## Configuring Samba with SWAT

The Samba team went all out to provide a handy GUI tool to administer almost every aspect of Samba, called SWAT. This section provides a simple example of how to use SWAT to set up SMB access to a user's home directory and how to share a directory.

You need to perform a few steps before you can start using SWAT. First, make sure you have the Samba and the `samba-swat` RPM packages installed. To then enable SWAT access to your system, edit the `/etc/xinetd.d/swat` file by changing the following line:

```
disable = yes
```

Change the word `yes` to the word `no`, like so:

```
disable = no
```

Note that you must do this as root, as regular users cannot change this file. Save the file, and then restart the `xinetd` daemon, using either the `system-config-services` client or the `xinetd` shell script under `/etc/rc.d/init.d`, as follows:

```
# service xinetd restart
```

Next, start an X session, launch any web browser, and browse to the `http://localhost:901` uniform resource locator (URL). You are presented a login prompt. Enter the root username and password, and then click the OK button. The screen clears, and you see the main SWAT page, as shown in Figure 19.4.

> **TIP**
> You can also configure Samba with Fedora's `system-config-samba` client. Launch the client from the command line of an X terminal window or select the System, Administration, Samba menu item (as shown later in Figure 19.10).

![](img/34e72348d53ca54c2a1d9c871316691b_451_0.png)

FIGURE 19.4 SWAT can be used to easily configure and administer Samba on your system.

First, click the GLOBALS icon in SWAT’s main page. You see a page similar to the one shown in Figure 19.5. Many options are in the window, but you can quickly set up access for hosts from your LAN by simply entering one or more IP addresses or a subnet address (such as `192.168.0.`—note the trailing period, which allows access for all hosts; in this example, on the `192.168.0` subnet) in the Hosts Allow field under the Security Options section. If you need help on how to format the entry, click the Help link to the left of the field. A new web page appears with the pertinent information.

When finished, click the Commit Changes button to save the global access settings. The next step is to create a Samba user and set the user’s password. Click the PASSWORD icon on the main SWAT page (refer to Figure 19.4). The Server Password Management page opens, as shown in Figure 19.6. Type a new username in the User Name field; then type a password in the New Password and Re-type New Password fields.

> **NOTE**
> You must supply a username of an existing system user, but the password used for Samba access does not have to match the existing user’s password.
