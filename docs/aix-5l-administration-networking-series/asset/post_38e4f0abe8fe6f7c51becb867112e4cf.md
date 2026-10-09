
# CHAPTER 16
## Linux Affinity with AIX

IBM embraces the open source and GNU movement by adding the capability to run many Linux applications on the highly scalable AIX operating system. The AIX Toolbox for Linux Applications is a collection of software that will run on AIX 4.3.3 and AIX 5L systems installed on IBM pSeries and RS/6000 models. Linux application developers are comfortable working with the AIX Toolbox for Linux Applications. The tools are easy to install using the RPM format. With the addition of the software and development tools, IBM has introduced a bold affinity between Linux and AIX applications. In most cases, it is easy to rebuild your Linux applications on the AIX platform.

### RUNNING LINUX APPLICATIONS ON AIX 5L

IBM uses a two-phase approach for the implementation of Linux affinity into AIX. The first phase came with the release of the AIX Toolbox for Linux Applications, which was released with AIX 4.3.3 at maintenance level 8. The second phase is to provide additional application program interfaces (APIs) and header files with each subsequent AIX 5L release. These additional APIs allow you to bring your Linux source code over to your AIX 5L machine and recompile the program to create an AIX application. Each recompiled Linux application is treated as an AIX 5L application, which comes with the additional reliability, availability, and scalability that AIX provides.

You can get the latest installation procedure and download the latest version of the Toolbox packages at the following URL:

`http://www.ibm.com/servers/aix/products/aixos/linux/`

There is an excellent IBM Redbook called Running Linux Applications on AIX that goes into great detail about installing the Linux Toolbox and compiling and running Linux code on AIX. This Redbook can be downloaded for printing in either an HTML or PDF format at this URL:

`http://www.redbooks.ibm.com/redbooks/SG246033.html`

### Contents of the AIX Toolbox for Linux Applications

Not only can you compile Linux applications on AIX, but you can also install a large variety of Linux native applications from the AIX Toolbox for Linux. You can change the user interface to run GNOME and KDE, instead of CDE or the command line. The list of native Linux applications that reside on the CD-ROM is too large to cover here; a sample is given in Table 16-1.

The list in Table 16-1 displays a few of the tools and programs in the AIX Toolbox for Linux. In the next section, we cover installing the Toolbox on an AIX machine.

### Installing the AIX Toolbox for Linux Applications

Before you install the toolbox, you must ensure that you have enough disk space for the installation. Unlike when using SMIT or installp, you do not have the option when installing the Toolbox to automatically extend the filesystem on the fly. On AIX 5L, the Toolbox is installed in the `/opt` filesystem. Table 16-2 shows the space requirements for the various components of the Toolbox.

| Package | AIX Platform | Description |
| :--- | :--- | :--- |
| bison | Power/IA-64 | GNU parser generator |
| cdrecord | Power/IA-64 | Command-line CD/DVD recording program |
| cvs | Power/IA-64 | A version control system |
| emacs | Power | The emacs editor |
| enscript | Power/IA-64 | ASCII-to-PostScript converter |
| flex | Power/IA-64 | Tool to create scanners for pattern recognition |
| gcc | Power | GNU gcc C compiler |
| g++ | Power | GNU gcc C++ compiler |
| gbd | Power | GNU gcc debugging tool |
| ghostscript | Power | PostScript interpreter and renderer |
| gnome | Power | GNOME GUI desktop environment |
| gnuplot | Power/IA-64 | For plotting mathematical expressions and data |
| jabber | Power | Instant messaging system |
| kde | Power | K desktop environment |
| lsof | Power | Lists open files |
| php | Power/IA-64 | The PHP scripting language |
| python | Power/IA-64 | Interactive object-oriented programming language |
| rpm | Power/IA-64 | Red Hat package management tool |
| samba | Power/IA-64 | Samba client and server package |
| sudo | Power/IA-64 | Allows restricted root access for defined users |
| tk | Power/IA-64 | tk toolkit with the shared libraries |
| wget | Power/IA-64 | Retrieves files using FTP and HTTP protocols |
| xfig | Power | Tool for drawing vector graphics |
| zsh | Power | Shell based on ksh with enhancements |

Table 16-1. Short List of the Linux Toolbox for AIX

The space requirements listed in Table 16-2 may expand with new releases of the Toolbox. If you want to change your desktop to either GNOME or KDE, make sure that three additional AIX filesets are installed: X11.adt.lib, X11.apps.xdm, and X11.samples.apps.clients. The quickest method to check for these installed filesets is to use the `lslpp -L` command.

```
# lslpp -L X11.adt.lib X11.apps.xdm X11.samples.apps.clients
```

If any of the listed products are missing, you need to install the packages from the AIX installation media. Do not forget to reinstall the patch set for the current maintenance level in case modifications have been made. The maintenance-level code is installed by using the SMIT FastPath smitty update_all.

On the next screen, you are prompted for the location of the maintenance code; for example, if it is located on a CD-ROM inserted in /dev/cd0, then enter the device name. If the code is located in /usr/sys/inst.images, then enter the system path. If you do not want to commit the software updates, but instead install the patch set in an applied state, follow this procedure: in the SMIT panel set the COMMIT Software Updates? field to No, and set the SAVE Replaced Files? field to Yes. Then press the ENTER key twice to install the software.

### Red Hat Package Manager (RPM)

Before installing the whole AIX Toolbox for Linux, you must first install the Red Hat Package Manager (RPM). This fileset must be installed as a traditional AIX fileset using installp, SMIT, or WebSM. The quickest method is to use installp on the command line. First, change directory to the CD-ROM mount point, for example, /cdrom. In this case, you need to change directory to the installation directory /cdrom/INSTALLP/ppc. Use the following installp command:

```bash
# cd /cdrom/INSTALLP/ppc
# installp -qacXg -d . rpm.rte
```

or use the SMIT FastPath smitty install_latest

On the first SMIT screen, you are prompted for the location of the code to install. If your CD-ROM is mounted as /cdrom, use the path /cdrom/INSTALLP/ppc. You can leave the Software To Update field set to _update_all, since the RPM package is the only fileset in this directory.

This installation will take several minutes because the installation will query the system for information about currently installed shared libraries on the system. If you want to download the latest *rpm_rte* fileset, go to the following FTP site:

`ftp://ftp.software.ibm.com/aix/Freeware/aixtoolbox/INSTALL#ppc`

The user ID is *anonymous* if you need one; and, if a password is needed, it will be your e-mail address. The download method is binary. You can also get the latest versions of the prebuilt RPM packages from this web site.

The man page directory for the Toolbox is located in /opt/Freeware/man. To add this path to the MANPATH variable, use the following syntax:

```
# export MANPATH=$MANPATH:/opt/Freeware/man
```

Or, you can add this MANPATH to your $HOME/.profile or to the system profile located in /etc/profile.

### Installing the Toolbox Base Filesets

Now that RPM is in place, we can install the remaining packages. The first step is to see which packages are already installed on the system. The following RPM command will give you the installed package list:

```
# rpm -qa
```

At this point, you will probably see only three RPM packages. Before installing the rest of the packages, ensure that you have provided adequate disk space; space requirements are listed earlier in Table 16-2. To install all of the base RPM packages, perform the following steps:

```
# cd /cdrom/exinstall/ppc
# rpm -hiv */*
```

or

```
# rpm -hiv base/*/ deskop*/ kde*/ gnom*/
```

The preceding commands install all the RPM packages. The ezinstall packages include base, gnome.apps, kde2.all, kde2.opt, desktop.base, gnome.base, and kde2.base. If you are not planning to change your desktop to either KDE or GNOME, then you can save a lot of disk space by installing only the **base** ezinstall package.

### Installing the Toolbox Utilities and Programs

In the preceding section, we installed only the Toolbox base filesets. To install the rest of the Toolbox Linux utilities and programs, use one of the following commands:

```
# cd /cdrom/RPMS/ppc
```

For AIX 5L
