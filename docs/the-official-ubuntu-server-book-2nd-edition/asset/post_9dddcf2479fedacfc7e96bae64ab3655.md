
```text
kernel ubuntu-installer/i386/linux
append vga=normal initrd=ubuntu-installer/i386/initrd.gz -- quiet
label cli
    menu label ^Command-line install
    kernel ubuntu-installer/i386/linux
    append tasks=standard pkgsel/language-pack-patterns= pkgsel/install-language-support=false vga=normal initrd=ubuntu-installer/i386/initrd.gz -- quiet
```

The default line tells pxelinux that the section labeled install is the one to load by default if a user just presses Enter at the boot prompt. The label install section defines a particular configuration a user can select. Every section that begins with a label defines another configuration. As you look through this configuration file, you will see a number of different labels already set up for you. You can choose between different sections by typing the specific label at the boot prompt and pressing Enter. So while I could just hit Enter to select the section above labeled install, since it is set as the default, I could also type install at the boot prompt and press Enter. All we need to do to this file is change the default boot options so that they also point to our Kickstart file. To do this I just add my options to the append line. The beginning section of the file changed from this:

```text
default install
label install
    menu label ^Install
    menu default
    kernel ubuntu-installer/i386/linux
    append vga=normal initrd=ubuntu-installer/i386/initrd.gz -- quiet
```

to this:

```text
default install
label install
    menu label ^Install
    menu default
    kernel ubuntu-installer/i386/linux
    append vga=normal initrd=ubuntu-installer/i386/initrd.gz ks=http://10.1.1.5/ks.cfg -- quiet
```

Save your changes and exit your text editor. Pxelinux is now configured and you are ready to move on to the final step.

## Web

The last step in the process is to set up a Web server to host your Kickstart and preseed files and any custom scripts you might have. First install the apache2 package, which will provide your Web server software and all its necessary dependencies:

```text
$ sudo apt-get install apache2
```

The apache2 package will automatically set up and start a functioning Web server for you with a default docroot of /var/www. I won’t cover any more advanced configuration of Apache here because all we want is a Web server to host a few text files. At this point all you need to do is move your ks.cfg file to /var/www on this server. You will need to make only one change to your ks.cfg file for PXE booting. Since we won’t be pulling down files from the CD-ROM, we need to tell our Kickstart file to grab files from an Ubuntu mirror, so find and change the line that reads

```text
cdrom
```

to

```text
url --url http://us.archive.ubuntu.com/ubuntu
```

> **NOTE** Since this server will be pulling all of its packages directly from an Ubuntu mirror, the installation will undoubtedly take longer than it would from the CD-ROM. If you plan to do a lot of automated Ubuntu installs, you will probably want to consider setting up your own mirror of the Ubuntu archive.

Before you go any further, try to access your ks.cfg file either from a Web browser or using a tool like wget and make sure that Apache is serving that file. If you can’t access the file, check the Apache error logs in /var/log/apache2/error.log for clues as to what may be wrong, and check the permissions on ks.cfg to make sure that it is world-readable. If not, type chmod a+r ks.cfg to make it so.

## Test Your PXE Server

At this point you should be ready to test your PXE server with a new install. There’s no single instruction on how to set a server to PXE boot. On some servers it’s just a matter of hitting a function key to get a list of boot options and then selecting network boot. On other servers you need to go into the BIOS and change the boot order. Still other servers provide a function key that automatically netboots. You will need to research how to tell your particular server to netboot and also make sure that it is connected to the same subnet as your PXE boot server.

Once you PXE-boot your server, you will be greeted with an Ubuntu menu as shown in Figure 4-3. Since we set up the default label to boot with our Kickstart options, all we need to do here is press Enter.

> **NOTE** Even this automated install requires some user interaction since you need to at least hit Enter at every boot prompt to start the installation process. This is a safety mechanism in a sense, since what happens if six months from now one of your servers reboots and then netboots? If everything were completely automated, that server would start the installation process again and potentially overwrite all of its current files—which could be a very bad thing. Now for some organizations this is desirable behavior (particularly for large clusters of identical machines). They have put in appropriate safeguards so that no machine boots on the network unless they want it to, and if it does, they definitely want it to perform a reinstall. If you want a 100% automated install that requires no user interaction apart from turning on the server, then just locate the TIMEOUT value in the pxelinux.cfg/default file. By default it is set to 0, which means that it will never time out. Just change that to a 1 and any server that boots and grabs that configuration file will automatically load the default label after a one-second time-out.

![](img/304f637afcecc491b152ee8ac5afadee_173_0.png)

Figure 4-3 Ubuntu PXE boot menu
