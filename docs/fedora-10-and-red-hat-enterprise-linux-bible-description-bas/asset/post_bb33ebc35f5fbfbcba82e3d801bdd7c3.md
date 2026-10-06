
## Part II: Using Fedora and RHEL

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_283_0.png)

Figure 5-5: Set up your Windows applications in Linux from the Wine configuration window.

## Assigning drive letters

Before you begin installing Windows applications in WINE, you should become familiar with your WINE environment. Drive letters are assigned in the $HOME/.wine/dosdevices directory. Select the Drives tab on the Wine configuration window to see which drive letters are assigned. At least drive C: and drive Z: should be set.

To configure additional drive letters, you can select Add (to add an individual drive) or select Autodetect (to have WINE assign all your partitions to drive letters) in the configuration window.

Within the $HOME/.wine/drive_c directory (that is, your C: drive), you should see some things that are familiar to you if you are coming from an older Windows environment: Program Files and windows directories.

> NOTE: For details on configuring WINE, see the Wine User Guide. That guide (wineusr-guide.pdf) is stored in the /usr/share/doc/wine-docs* directory when you install the wine-docs RPM.

## Chapter 5: Accessing and Running Applications 237

## Installing applications in WINE

For Windows applications that are included on CD or DVD, you can try installing them by simply running the setup program on that medium with the wine command. So, with a CD containing the application you want to install inserted and mounted, you would run a command like the following:

```
# wine d:\Setup.exe
```

## Launching applications

Depending on how the application's installer set up the application, there are a couple of ways in which you might launch your Windows application in WINE, as follows:

- **Control Panel** — If the application set up an app for the Windows control panel, you can open a Windows control panel, and then select the app to launch the application from there. To start a Windows control panel, type the following:

```
$ wine control
```

- **WINE File System Browser** — If you installed the wine-tools package, you can launch the winefile window to see the WINE window. This displays a tree structure of the file system, as it relates to the drives you have configured for WINE. Select the drive letter containing the application you want to launch, browse to the application, and double-click to start.

Just as you launch the application's installer, as described earlier, you can also launch a Windows application installed on your file system from the command line. Again, you can use drive letters to indicate the location of the application you want to launch. However, to have the path to the application properly interpreted, you should typically surround it with quotes:

```
$ wine "C:\program files\appdir\app.exe"
```

As a Windows file path use backslashes (\) instead of slashes (/) to separate subdirectories. Instead of using double quotes, you can add an extra backslash before each space or slash.

Once you have a working wine command to run your Windows application, you can add a command to a launcher on your Fedora desktop. See Chapter 3 for information on adding application launchers to your panel, menus, or desktop area.

## Tuning and configuring WINE

Because the Windows applications you run with WINE expect to find Windows resources on a Linux system, those either have to be provided by WINE or need to be mapped into the existing Linux system. For example, an application may require a specific dll file that WINE doesn't include. Or, you may need to map your COM or LPT ports where WINE expects to find them.

Here are some tips to help you tune your WINE configuration:

- **Windows version** — Different versions of Windows provide different environments for applications to run in. WINE emulates Windows XP by default, but allows you to have WINE run as a dozen Windows versions for each application. From the WINE configuration window, select the Applications tab and choose the Addition button. Choose the Windows application you want from your file system then choose the Windows version you want to run it.

- **Changing registry entries** — When need to change WINE registry entries, WINE provides three files you can work with: system.reg, user.reg, and userdef.reg. All of these files are in the user's $HOME/.wine directory. You can use the wineprefix utility to update your registry, but normally you should no longer need to, as this should happen automatically.

- **Configuring ports** — As Windows drive letters, you can add links to serial and parallel ports to your $HOME/.wine/dosdevices directory. For add entries for your first parallel port (LPT1) and serial port (COM1), you could run the following commands from $HOME/.wine/dosdevices directory:

```
$ ln -s /dev/lp1 lpt1
$ ln -s /dev/ttyS0 com1
```

- **Adding DLLs** — WINE provides many of the basic libraries (DLL files) needed for a functioning Windows system. However, some DLLs that may be required for your application may not be included, or some that included may not work properly for your application. Using the Windows configuration window (Libraries tab), you can replace DLLs with WINE or other DLLs you have from applications you install.

- **Graphics settings** — You can change settings associated with your graphics display from the Graphics tab on the Windows configuration window. In particular, you can change how closely Windows applications can be managed on your Linux desktop.

- **Adding fonts** — To adds to your WINE installation, copy TrueType (.ttf files) to the C:\windows fonts directory on your WINE virtual drive.

For further information on configuring WINE to run your Windows applications in Linux, refer to the Wine User Guide (http://www.winehq.org/docs/en/wineuser-guide.html).

## Finding more Windows applications for WINE

For information on Windows applications that have been tested in WINE, refer to the Wine Application Database (http://appdb.winehq.org). CodeWeavers keeps its own database of applications that have been tested to run under WINE. Refer to the CodeWeavers Compatibility Center (http://www.codewavers.com/compatibility)

## Chapter 5: Accessing and Running Applications 239

for information on running Windows applications. From there, you can view CodeWeavers' own application database of more than 3300 Windows applications.

Another Web site for information about WINE applications is Frank's Corner http://www.frankscanner.org. The site is loaded with good tips for getting graphics, Internet, multimedia, office, games, and other applications running in WINE.

> CROSS REFERENCE: With Mac OS X based on a Linux-like operating system, and more cross-platform applications will be available for Linux and the Mac. Interoperating Mac OS X with systems is discussed in detail in Chapter 26.

## Running Applications in Virtual Environments

Virtualization has become a hot topic in Linux in recent years. Instead of being able to have just one operating system running on computer at a time, virtualization allows multiple operating systems to run on host. When acting as the host operating system, Fedora offers two approaches to virtualization: Xen and KVM.

The following sections introduce you to Xen and KVM virtualization software.

## Running applications virtually with Xen

Xen (http://www.xource.com) is virtualization software that is included in Fedora. (Xen is now owned by Citrix.) Using Xen, you can run multiple operating system instances within a Fedora system. These operating systems, referred to as virtual machines, can not only run applications specifically for those operating systems. They can also appear to the network as they are running on completely different machines.

To demonstrate Xen, the procedures in this section describe how to set up a virtual machine of Fedora that will run on an installed host Fedora system. Currently, to run other operating systems on Xen in Fedora, you need to supply an OS image, rather than build from scratch as in the procedure.

If you run into road blocks with Xen, there are places to get help. Ask questions about Xen, see the Fedora-Xen mailing list (http://www.redhat.com/mailman/listinfo /fedora-xen). Try the Xen Tools for links to further information on Xen in Fedora (http://fedaproject.org/wiki/Tools/Xen).
