
CDs, you can also download this CD image separately from fedora.redhat.com/download.

It's a good idea to make a separate boot CD and store it for safekeeping. To create your Fedora Rescue CD from the image stored on the DVD, do the following:

1.  With Fedora installed and running, insert the Fedora DVD into the DVD drive.
2.  The Fedora DVD may mount automatically. If it does not, type something like the following (depending on the type of DVD drive you have) as root user from a shell:
    ```
    # mount /media/cdrom
    ```
3.  Copy the Rescue CD image to your hard disk:
    ```
    # cp /media/cdrom/images/rescuecd.iso /tmp/
    ```
4.  Unmount your DVD, eject it, and remove it:
    ```
    # umount /media/cdrom
    ```
5.  Insert a blank CD into your CD burner.
6.  Refer to the Red Hat Linux Getting Started Guide for procedures for writing iso images to CD (www.redhat.com/docs/manuals/linux/RHL-9-Manual/getting-started-guide/s1-disks-cdwr.html). Or, just try the following command:
    ```
    # cdrecord -v -pad speed=2 /dev/cdwr0 /tmp/rescuecd.iso
    ```

It's likely that you will be able to record at a higher speed than 2. If you like, you can just skip the speed=2 and let cdrecord determine how fast the drive can write. However, if you find that you are unable to boot the CD you create, you will find that a slower record speed will often fix the problem. Eject the CD when you are done and label it appropriately.

To use the Fedora Core 3 Rescue CD after you have created it, do the following:

1.  Insert the Rescue CD into the CD drive.
2.  Reboot your computer. You will see the Fedora Core 3 Rescue CD welcome screen with the boot: prompt at the bottom.
3.  Press Enter to begin rescue mode. (You could also type linux to begin a Fedora Core install with this CD, or press the F2 function key to see other options.) The rescue CD asks you to choose a language.
4.  Choose a language and select OK. You are asked to choose a keyboard type.
5.  Choose a keyboard type and select OK. You are asked if you want to start network interfaces.
6.  Choose Yes (to start a network interface, if you have a network interface card installed) or No (to continue booting without a network interface).
7.  If you said Yes, choose DHCP, or type in a static IP address and Netmask for your computer. Also, identify your gateway (the machine that connects you to the Internet) and one or more DNS servers you need for address resolution.
8.  When you enter the rescue environment, you need to choose whether or not to mount your Linux installation (under `/mnt/sysimage` directory) by selecting Continue, to mount it as read-only (select Read-Only), or to not mount it (select Skip).

If everything went well, you should receive the message: `Your system is mounted under the /mnt/sysimage directory. You will see a shell prompt.` Now you can:

-   Try to fix any errors in your Linux configuration, beginning at `/mnt/sysimage` to find your normal root (`/`) directory.
-   Backup or transfer files from your computer to other media or computers, if your system remains unbootable, so you can save any critical files.

When you are done, remove the CD and reboot your computer.

NOTE: Everything you do with the rescue CD you can also do with the Fedora DVD or first CD in your Fedora Core 3 installation CD set. The rescue CD is just more convenient in some cases because it is smaller to copy (only about 74MB as compared with over 4GB for the Fedora DVD) and quicker to boot up. It will also fit on a medium that is smaller than a full-size CD.

## Appendix B

### Fedora Core 3 RPMs

More than 1,600 RPM Package Manager (RPM) software packages make up the Linux distribution referred to as Fedora Core 3. This appendix contains an alphabetical listing and descriptions of those Fedora Core 3 software packages.

Packages are distributed on the DVD that comes with this book. Descriptions in this appendix help you determine the contents of those packages. You typically install the bulk of those packages when you install Fedora as described in Chapter 2. Later, you can add other packages using the Package Management window (Chapter 2) or the rpm command (Chapter 5).

### Comparing Fedora and Enterprise Packages

The Fedora Project was set up as a proving ground for developing technology that can be used by Red Hat, Inc. to include in its Red Hat Enterprise Linux products. You can look at Fedora Core 3 as a way of getting a jump on technology that is slated to be included in Red Hat Enterprise Linux and related Linux distributions.

Although the timing of the releases of Fedora Core 3 and the next release of Red Hat Enterprise Linux may make some version numbers different, there are hundreds of software packages that will probably be the same in the two distributions.

### Removed Packages

If you can’t seem to find a software package you relied on in previous Red Hat Linux or Fedora Core distributions, you might be interested in the following list. It shows packages from Fedora Core 2 that are not in the Fedora Core 3 distribution:

-   **ac-archives**: The Autoconf Macro Archive providing macros for the autoconf tool.
-   **anaconda-images**: Graphical images used in the anaconda installer.
-   **bleez-pan**: Bluetooth personal area networking tools.
-   **chromium**: An arcade-style shooting game.
-   **commons-\***: A set of packages for developing reusable JAVA components under the Apache Jakarta Commons project (http://jakarta.apache.org/commons).
-   **dev**: Commonly used Linux device files.
-   **devlabel**: Consistent storage device access facilitated by symlinking.
-   **dvdrecord**: A command-line CD/DVD recording program.
-   **fam**: Tracks file system changes through a daemon and API.
-   **fam-devel**: Libraries and header files for fam.
-   **glade**: Software for developing quick user interfaces for the GTK+ toolkit.
-   **gqvview**: Feature rich image viewer.
-   **Gtk-Perl**: Perl extensions for gtk+ that facilitate GUI creation using Perl.
-   **iiimf-client-lib**: Removed element of the Intranet/Internet Input Method Framework packages.
-   **iiimf-client-lib-devel**: Removed element of the Intranet/Internet Input Method Framework packages.
-   **iiimf-le-inpinyin**: Removed element of the Intranet/Internet Input Method Framework packages.
-   **imlib-cfgeditor**: Removed element of the Intranet/Internet Input Method Framework packages.
-   **iscsi**: The iSCSI daemon and utility programs.
-   **kde-i18n**: Korean and Lithuanian packages removed.
-   **kernel-source**: The source code files that are used to build the Red Hat Linux kernel.
-   **libfortran-ssa**: GCC Fortran support.
-   **libfortran-ssa-devel**: GCC Fortran support libraries.
-   **libgce-ssa**: GCC version 3.0 shared support library.
-   **libgcj-ssa**: Java runtime library for GCC.
-   **libgcj-ssa-devel**: Libraries for Java development using GCC version 3.
-   **libgcj34**: Java runtime library for GCC version 3.4.
-   **libgcj34-devel**: Libraries for java development using GCC.
-   **libgnomeprint**: GNOME printing library.
-   **libgnomeprint-devel**: Libraries for developing printing in GNOME applications.
-   **libgnomeprintui**: GUI support for libgnome print.
-   **libgnomeprintui-devel**: Libraries for compiling libgnomeprintui applications.
-   **libole2**: Structured storage OLE2 (Object Linking and Embedding) library.
-   **libole2-devel**: Header files to develop applications for OLE2-structured storage files.
-   **librep**: Tools and documentation associated with the librep Lisp dialect.
-   **librep-devel**: Header files and tools associated with the librep Lisp dialect.
-   **libstdc++-ssa**: GNU Standard C++ Library Version 3.
-   **libstdc++-ssa-devel**: Header files and libraries for C++ development.
-   **libstdc++34**: GNU Standard C++ Library version 3.4.
-   **libstdc++34-devel**: Header files and libraries for C++ development.
-   **licq**: The licq ICQ chat utility.
-   **licq-gnome**: A GNOME front-end for licq.
