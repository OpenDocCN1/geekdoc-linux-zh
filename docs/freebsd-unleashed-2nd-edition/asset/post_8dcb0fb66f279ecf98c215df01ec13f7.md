
other=/dev/hda2
   table=/dev/hda
   label=FreeBSD

Change the line beginning with `other=` to reflect whatever device Linux recognizes your FreeBSD drive as.

After you have changed the configuration file, reinstall LILO by typing **lilo** as the root user.

## Alternate Installation Methods

If you can't or (for whatever reason) don't want to install FreeBSD from the CD included with this book, you have several other options available. These include network installs with FTP or NFS. Installation over the network is especially convenient when you are in a location with a lot of bandwidth and don't have the CD-ROM handy, or if the machine doesn't have a working CD-ROM drive. For many servers or workstations in enterprise environments, installing from a network source is the quickest and most efficient way to get FreeBSD installed.

### Installing FreeBSD over FTP

FTP stands for *File Transfer Protocol*. It is one of the earliest methods of transferring files over the Internet, from one system to another. FTP is still widely used; it's the backbone of file transfers on the Internet, as we will discuss in Chapter 26, “Configuring an FTP Server.”

You can install FreeBSD directly from an FTP server, but you should have a full-time, fast Internet connection available in order to do so. Performing an FTP install over a modem will take a *very* long time.

If you are installing FreeBSD from the FreeBSD sites or one of the official mirrors, you can log in as “anonymous.” In this case, you can skip the next section. If, however, you are installing from an FTP server that does not allow anonymous logins (such as an internal FTP server on a LAN), you will need to follow the procedures in the next section to configure the username first.

### Configuring the Username

From the `sysinstall` main menu, shown in Figure 3.1, arrow down to Options and press Enter. In the Options menu, shown in Figure 3.2, you can set the FTP login name.

![](img/48eec858cce7dfb89da36a4d40b7daf3_98_0.png)

**FIGURE 3.1** The FreeBSD **sysinstall** main menu. From here, select the **Options** menu item.

![](img/48eec858cce7dfb89da36a4d40b7daf3_98_1.png)

**FIGURE 3.2** The **Options** menu, in which you can set the FTP login name (among other installation preferences).

Arrow down to the option that reads **FTP Username** and press the spacebar. A dialog asks you to enter the username for FTP access; the administrator of the FTP server you will be using should furnish you with a username and password that will let you into the server. Enter the username and press Enter. You are asked to supply a password. Enter the password you need to use and press Enter again.

After you have finished, press Q to quit, and you will be returned to the Main **sysinstall** menu.

## Selecting an FTP Install

After you have set the FTP username and password (if necessary), follow the instructions in Chapter 2, found in the “Creating Partitions and Assigning Mount Points” and “Selecting a Canned Distribution Set” sections, until you get to the screen where you are asked to choose the installation media. From this screen, select FTP or FTP Passive if the server you intend to install from is behind a firewall (ask your system administrator if you are not sure). You will then be asked to select a distribution site (see Figure 3.3).

![](img/48eec858cce7dfb89da36a4d40b7daf3_99_0.png)

FIGURE 3.3 The list of available FTP servers from which you can install FreeBSD. Choose the public server closest to you or choose a private server.

If you are installing from one of the FreeBSD mirror sites, you can select the site from the list, using whichever server is listed as being geographically closest to you (to maximize download speed). Otherwise, select URL to specify an FTP server manually. In the dialog that comes up (see Figure 3.4), you will be asked to specify the name of the FTP server as well as the path to where the FreeBSD installation files are located. Figure 3.4 shows an example for an FTP site with the hostname lion located on the network sample.net.org, with the FreeBSD files located in the /FreeBSD directory.

![](img/48eec858cce7dfb89da36a4d40b7daf3_99_1.png)

FIGURE 3.4 Specifying a custom FTP server location by URL.

Once you have configured the FTP server you wish to install from, you will need to configure the network (see Figure 3.5). Follow the procedure in the “Configuring the Network” section of Chapter 2 to complete this configuration. This step only needs to be completed once; after your network has been configured, you can return to sysinstall and perform other post-installation tasks without having to configure the network again. The sysinstall program gives you the option to skip that step or re-enter other network data.

Once you have finished configuring the network, the various distribution sets will download to your computer and install themselves. This process will probably take a long time; you may want to turn your attention to something else for the next few hours. When files have finished copying, you can go ahead with the instructions offered in the “Post-Installation” section of Chapter 2. Because you have already configured the network to do the installation, you can skip the network-configuration portion of those instructions.

![](img/48eec858cce7dfb89da36a4d40b7daf3_100_0.png)

**FIGURE 3.5** Configuring the TCP/IP networking parameters. This information is stored as the system’s TCP/IP configuration.

Note that this chapter has covered only how to install FreeBSD from an FTP server. If you want to set up an “installation server” that can be used by clients to install FreeBSD, see Chapter 26. Once you have an FTP server set up and the FreeBSD installation files available on it, you can have other systems install from it using the procedures in this chapter.

# Performing an NFS Install

NFS stands for *Network File System*. It provides a way for filesystems located on a server elsewhere on the network to be mounted into your own computer’s directory structure, and the files in it to be made accessible as though they were on your own hard disk. File sharing with NFS is fully covered in Chapter 32, “The Network Filesystem (NFS).” FreeBSD can be installed over NFS, assuming that there is an NFS server on your network that has the installation files available.

If your NFS server will work only on a secure port (or if you have a slow Ethernet adapter), follow the procedure in the following section. Otherwise, you can skip immediately ahead to “Selecting an NFS Install.”

## Configuring sysinstall for a Secure Port or Slow Connection

At the sysinstall main menu (shown previously in Figure 3.1), select *Options* and press Enter. The first listing in the Options menu is NFS Secure. If your NFS server only works on a secure port (ask your system administrator if you’re not sure), press the spacebar to toggle this to Yes. The second option (NFS Slow) should be toggled to Yes if you have a slow PC (something from the 386 era) or an Ethernet card with very poor performance. This is almost certainly unnecessary; the only cases where an Ethernet card would be slow enough to necessitate this option is if your own computer’s filesystem is being remotely accessed, as from yet another NFS server, instead of being locally mounted. Once you have made these changes, press Q to return to the sysinstall main menu.

Installation then continues, as discussed in Chapter 2, up to the point where you are asked to choose installation media.

## Selecting an NFS Install

At the Choose Installation Media screen, select NFS. You will then be asked to enter the name of the NFS server followed by the path where the FreeBSD installation files are located. In the example in Figure 3.6, the server is lion and the installation directory is install/FreeBSD.

![](img/48eec858cce7dfb89da36a4d40b7daf3_101_0.png)

**FIGURE 3.6** Specifying the NFS location of the remote FreeBSD installation files.

Once you have entered this information, you will need to configure the network (shown previously in Figure 3.5). Follow the procedure shown in Chapter 2 under the “Configuring the Network” heading for instructions on how to do this.

Once you have finished configuring the network, the various distribution sets will be downloaded from the remote server and installed. This will naturally take longer than installing from a CD-ROM, but it will likely be faster than an FTP installation. When files have finished copying, you can go ahead with the “Post-Installation” section of Chapter 2. Because you have already configured the network to do the installation, you can skip the network-configuration portion.

Note that this chapter has covered only how to install FreeBSD from an NFS server. If you want to set up an installation server that can be used by clients to install FreeBSD over NFS, see Chapter 32. Once you have an NFS server set up and the FreeBSD installation files available on it, you can have other systems install from it using the procedures discussed in this chapter.
