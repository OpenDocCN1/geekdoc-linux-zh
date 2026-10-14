
When you download a new script, you either can install it so that everyone on the system can use it, or you can install it locally in your home. To install a script for global usage, you need to copy the script file in /usr/share/gimp/scripts (if you installed GIMP from an RPM). If you compiled GIMP using its defaults, then the directory to copy the file to is /usr/local/share/gimp/scripts. Copy the script file there with the following:

```
# cp script /usr/share/gimp/scripts
```

To install it locally in your home, you need to place it in .gimp-1.1/scripts (please note the dot preceding .gimp-1.1). So, if your username is john, you would place it in /home/john/.gimp-1.1/scripts/, as shown in the following:

```
$ cp script ~/.gimp-1.1/scripts
```

The ~/ is replaced by /home/john. The script is now installed—restart GIMP and check it out.

## Troubleshooting

### I can't compile the GIMP

Are you sure that you have all the required libraries installed? Make sure that you have the GTK+ Development library installed.

### GIMP doesn't run correctly after I upgraded.

Did you remove the .gimprc in your home directory? If not, then do so using the procedure that was described earlier. The reason you should do this is that GIMP attempts to read the current configuration file, which was built by another version.

### I can't open some of the common image formats, why?

GIMP supports all the image formats as long as the corresponding image library is found. For example, for GIMP to support JPEG images, you should have libjpeg installed. Make sure that you have the required library for the image you are trying to open.

### I just installed a new plug-in/script-fu but it is not working.

Did you restart the GIMP? For script-fus, are you sure you placed the script in the correct place? Put it inside your home directory first to make sure that it's working.

### Script-fu is not working correctly, and displays an error message. This happens especially with the logos.

If you are using GIMP 1.0 series, and a script-fu fails with an error message, this usually means that the font you are trying to use cannot be found. Change the name of the font. Otherwise, make sure that the script you are running is compatible with your GIMP version.

## Installing and Configuring Netscape Communicator

### In this chapter

- A Briefing on Netscape 548
- Netscape and Linux 548
- Software Requirements 548
- Obtaining the Latest Netscape Version 549
- Installing the Latest Netscape Version 550
- Configuring Netscape's Appearance (Netscape Navigator) 550
- Configuring Netscape Browser (Netscape Navigator) 551
- Configuring Netscape Messenger (Email Client and News Reader) 553
- Configuring Composer (HTML Editor) 555
- Configuring Netscape's Advanced Options 556
- Netscape Tips and Tricks 557
- Troubleshooting Netscape Communicator 558

## A Briefing on Netscape

Soon after it was founded in 1994, Netscape released what was to become the most famous Internet graphical browser—Netscape Navigator. When Navigator was first released in 1995, its ease-of-use and powerful capabilities made it one of the major breakthroughs of the Information Age. It wasn't long before subsequent releases of Netscape products started to incorporate the new HTML technologies.

## Netscape and Linux

It wasn't long before Netscape was ported to Linux. As a matter of fact, when Netscape was ported to Linux, it wasn't only used in Internet navigation. Some of the various uses were in printing! Some users would write their documents in HTML, use Netscape Navigator to view them, and then print them out! This is in the past, of course. Thanks to StarOffice, WordPerfect, and some other word processing suites, we don't need Netscape Navigator for this purpose now. Netscape continued providing the Linux community with new versions of Netscape Communicator, thus making Internet navigation as simple as possible through interactive menus, a clear interface, and helpful tools. Netscape's browser comes in two flavors: the stand-alone Navigator and Netscape Communicator. The difference in size is not large, but the capabilities differ between each flavor.

## Software Requirements

Package Requirements:

- Series xap:
  - Netscape
  - plugger
- Series snd:
  - xMP
  - sidplay
- Series gra:
  - xanim
- Series pay:
  - acroread
  - MpegTv

## Obtaining the Latest Netscape Version

The simplest way to get the latest Netscape version is getting the package through the Netscape FTP. But, before you get the latest version of Netscape, you have to decide which flavor you want.

### Choosing Which Netscape Package to Get

As mentioned before, Netscape comes in Navigator stand-alone and Communicator packages. By getting the Navigator stand-alone version, you get only the Web browser. The Communicator package has Netscape Messenger and Netscape Composer in addition to the Netscape Navigator.

### Connecting to the Netscape FTP Site

Due to the load on the Netscape FTP site, Netscape made some mirrors from which users can get free Netscape products. The mirrors start from ftp.netscape.com to ftp20.netscape.com. You can start the download process with the following:

```
bash#ftp
ftp>open ftp20.netscape.com
```

You will be asked for a username and password. Use anonymous as the username and your email address as the password. If you don't have an email address, enter any string. After you are connected, you can get to the package you want. In this chapter, you should be getting the Communicator package. Therefore, issue the following command:

```
ftp>cd /pub/communicator/
```

In this directory you will find the Communicator package in several different languages. In this example you will be getting the English version of Communicator, with the following command:

```
ftp>cd english
```

Now the time has come to see what is the latest version of Netscape. List the available directories on the FTP:

```
ftp> ls
200 PORT command successful.
150 Opening ASCII mode data connection for /bin/ls
total
drwxr-xr-x 4 888 999 34 Sep 28 14:14 .
drwxr-xr-x 14 888 999 4096 Jun 15 16:26 ..
drwxr-xr-x 5 888 999 50 Jun 14 16:01 4.61
drwxr-xr-x 5 888 999 50 Sep 28 17:31 4.7
226 Transfer complete.
```

The listing shows that 4.7 is the latest version. It's easy to figure out because 4.7 is greater than 4.61. Enter the following command to get version 4.7:

```
ftp>cd 4.7
```

Then, to get the Linux version of Netscape, change to the following directory where the Linux binaries of Netscape are found:

```
ftp>cd unix/unsupported/linux22/
```

This directory has a listing of complete_install and navigator_standalone. Netscape Communicator is located in the complete_install directory, while Navigator is located in the navigator_standalone directory. To get to the complete_install directory, enter the following:

```
ftp>cd complete_install/
ftp>cd /tmp
ftp>bin
ftp>get communicator-v47-export.x86-unknown-linux2.2.tar.gz
```

The preceding ftp commands download Netscape Communicator into the /tmp directory. After the download is complete (12+ MB), proceed to the installation process.

## Installing the Latest Netscape Version

Now that you have downloaded the latest version of Netscape off its FTP site, you can start installing it. The installation process is done by first removing the old version of Netscape and then installing the new version.

The following command will uninstall the Netscape package that comes with SuSE:

```
bash#rpm -e netscape
```

You then start unpacking the Netscape version that you just downloaded and start the installation program:

```
bash#cd /tmp
bash#tar xzvf communicator-v47-export.x86-unknown-linux2.2.tar.gz
bash#cd communicator-v47-export.x86-unknown-linux2.2
bash#./ns-install
```

The installation program starts and asks you for the location of the installation. The default is /opt/netscape. Press Enter to accept the default or enter a new path to install the Netscape files to. The last step is to delete the old files from the previous installation, if they exist.

## Configuring Netscape's Appearance
(Netscape Navigator)

Because Netscape is customizable through menu-driven commands, it's not strange that customization is easy in Netscape. Open the Edit menu and choose Preferences. The Preferences window appears and you can start configuring the appearance of Netscape. Netscape has built a hierarchy tree of the preferences that can be set. By clicking the arrow next to the section name, you can expand or collapse the tree. In the Appearance section, you can choose the module that should be launched first when you start Netscape and the button interface. Figure 28.1 shows the Netscape preferences tree with appearance settings selected.
