
After you have the file, grab a cup of coffee or something. This is going to take some time:

- 1. Create a directory to use for the process, making sure that you have enough disk space for this. The unpacked files take up 70+MB, and when compiled, might need 100MB more. For this example, create a directory called /compile.
- 2. Unpack the file with the following command:
```
# tar xvfz X335src-1.tgz -C /compile
```
When done, you should have a directory called xc under /compile. This is where all the files are stored. Now you are ready to start the process.
- 3. Everything you need to know about how to do this is in the file called INSTALL.TXT—read this file! The file has full instructions on how to compile X Windows. Explaining how to compile X Windows in detail is out of the scope of this book. We will, however, explain a quick method to do this. We are assuming that if you are about to compile X Windows to fine tune it, you have enough knowledge to understand the INSTALL.TXT file.
- 4. After you read the INSTALL.TXT file and configure X Windows, you are ready to start compiling it. To do this, run a make command in /compile/X/xc:
```
# make World >& world.log
```
This will start the compilation process and will save all the messages coming from make to the file world.log.

> **CAUTION**
> 
> Unlike most compilations, make will not stop compiling if an error is encountered. You have to check the file world.log when make is done to ensure that you actually got everything to compile. To check, just look for any error messages in the file; if you find none, then you have everything. Now you need to install X Windows. A note of caution here—after you install the compiled version, it will replace a lot of the configuration files for your current X Windows, so you might want to back them up first. Just to be safe, you really should backup your /usr/X11R6 directory. Just copy all of its contents to another temporary directory. This way, if things don't work right for you, you can copy it back.

- 5. To install X Windows, run a make install in /compile/X/xc with this command:
```
# make install
```
- 6. Install the man pages with the following command:
```
# make install.man
```

That's it—you are done. You have compiled your X Window System.

## Upgrading Your KDE

The K Desktop Environment (KDE) is the main graphical desktop environment for SuSE Linux. It offers a very powerful and integrated desktop using a vast set of applications and utilities. KDE is currently at version 1.1.2 (code name Kolor). New versions of KDE are released every few months depending on how stable they are. The upcoming version is KDE 2.0, which promises to be very powerful and complete, with a whole new set of components and applications. Upgrading your KDE is a simple process once you know what you have to do.

### Checking Your KDE Version

Before you start checking for a new version of KDE, you will probably need to check the version of the one you have installed now. If you have SuSE 6.2, then you have KDE 1.1.1. You can check the version number by running the KDE Control Center. Simply launch an xterm and type kcontrol. The first window that appears should contain your current KDE version. Figure 7.5 shows the start screen of the KDE Control Center and the current KDE version.

FIGURE 7.5
KDE Control Center start screen.

![](img/659f91d9da7b29976c0625e2e9628511_165_0.png)

### Checking for a New Version of KDE

Now that you know which version you have, you should check if there is a newer version. One way is to check the SuSE update page as described previously. SuSE has built a great site that offers the latest RPMs of KDE and KDE applications compiled for your SuSE. This is the first place you will want to check for any new KDE packages at http://www.suse.de/en/support/download/LinuxKS/index.html. Figure 7.6 shows you the site. You can download

the packages that are appropriate for your distribution version and install them in the same way you updated your SuSE Linux in the previous section.

### FIGURE 7.6
SuSE KDE packages
Web site.

![](img/659f91d9da7b29976c0625e2e9628511_166_0.png)

Sometimes KDE releases are so new that SuSE doesn't synchronize with them. In that case you will want to check the home of KDE itself for the latest releases. Start your browser at http://www.kde.org—new versions of KDE are announced on the front page, as shown in Figure 7.7. Here you can see that the latest version is KDE 1.1.2. If you find out that a newer version of KDE is available, but is not yet packaged by SuSE, you have two options. You can either get it from KDE or wait for SuSE to package it and post it on its site. If you decide to wait, which we must say will not be a long wait, download the latest RPMs and install them using the same method described in the previous section “Upgrading Your Linux.” If you decide you just can’t wait, read on to find out how you can get the latest version yourself.

### CAUTION

You have to remember that SuSE does not compile KDE out of the box. In most cases, the SuSE team adds or modifies the KDE source code before compiling it. In some cases the modified code does not work with some of the current KDE applications. In that situation you might want to get the original KDE code and compile it.

### FIGURE 7.7

The KDE Web site's announcement section.

![](img/659f91d9da7b29976c0625e2e9628511_167_0.png)

### Getting the Latest KDE from kde.org

The main FTP site for KDE is ftp://ftp.kde.org. When new versions are released, this site usually has a lot of traffic and might not be easy to access. In that case, you will want to use a mirror site. A list of all the mirror sites is at http://www.kde.org/mirrors.html. Choose the mirror site that is geographically closest to you for maximum transfer speed. In our case, we will choose ftp.kde.org. Follow these steps:

- 1. Using your favorite ftp program, connect to ftp.kde.org. KDE packages are usually found in a directory called /kde/stable/latest/distribution.
- 2. Inside that directory you will see four directories, deb (for Debian Linux), pkg (for Solaris Unix), RPM (for Red Hat and SuSE), and tar (generic format). The first thing you will want to check is the RPM directory in case you find RPMs for SuSE. At the time of this writing, RPMs for SuSE were already built and are found in the RPM directory. All you have to do is download and install them using either YaST or RPM directly.

But what happens if you do not find RPMs for SuSE? In that case you might need to build KDE from source. This is a simple process, but it does take some time. The sources for KDE

are found in /pub/kde/stable/1.1.2/distribution/tar/generic/source/bz2. This directory contains a lot of files, and some of them you might not really need. The following table lists all those files and tells you whether you really need this package or not.

| Package Name | Package Description | Required/Optional |
|---|---|---|
| kdeadmin-1.1.2.tar.bz2 | System Administration programs | Optional |
| kdebase-1.1.2.tar.bz2 | Part of the KDE core | Required |
| kdegames-1.1.2.tar.bz2 | Games for KDE | Optional |
| kdegraphics-1.1.2.tar.bz2 | Graphics programs for KDE | Optional |
| kdelibs-1.1.2.tar.bz2 | KDE libraries, part of KDE core | Required |
| kdemultimedia-1.1.2.tar.bz2 | KDE multimedia applications | Optional |
| kdenetwork-1.1.2.tar.bz2 | KDE network applications (mail, news readers, and so on) | Optional |
| kdesupport-1.1.2.tar.bz2 | Libraries required to compile and run KDE | Required |
| kdetoys-1.1.2.tar.bz2 | KDE toy applications | Optional |
| kdeutils-1.1.2.tar.bz2 | KDE utility applications | Optional |
| korganizer-1.1.2.tar.bz2 | Organizer/scheduler for KDE | Optional |
| qt-1.44.tar.bz2 | GUI toolkit used to build KDE | Required |

As you can see from the previous table, there are only four packages that are required to upgrade your KDE. If you are just upgrading, you can download kdebase, kdelibs, kdesupport, and qt. These are the files that include the bulk of the updates; the rest of the applications do not change drastically. In your case, you will compile all the packages.
