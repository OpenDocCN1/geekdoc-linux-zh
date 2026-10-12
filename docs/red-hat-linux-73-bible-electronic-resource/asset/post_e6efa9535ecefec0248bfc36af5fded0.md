
## Understanding WINE

For WINE to let you run Windows applications, it needs to have an environment set up that looks like a Windows system. When you install the wine package in Red Hat Linux, the package creates /etc/wine.reg and /etc/wine.systemreg files that, like the Windows registry, identify the locations of components an application would need in a Windows operating system.

The location of the basic Windows operating-system directories for WINE is the /usr/share/wine-c directory (in other words, drive C:) by default. Table 5-6 shows how C: and other Windows drive letters are mapped into Linux directories and devices.

### Table 5-6: Windows Drive Letters in WINE

| Description | Drive Letter or Name | Linux Directory or Output Location | Linux Device Name (If Applicable) |
|---|---|---|---|
| Floppy drive | A: | /mnt/floppy | /dev/fd0 |
| Hard disk #1 | C: | /usr/share/wine-c | |
| CD-ROM | D: | /mnt/cdrom | /dev/cdrom |
| Temp directory | E: | /tmp | |
| User's home directory | F: | $HOME (user's home directory) | |
| Root directory | Z: | / | |
| Serial ports | COM1, COM2, COM3, COM4 | | /dev/ttyS0, /dev/ttyS1, /dev/ttyS2, /dev/ttyS3 |
| Parallel ports | LPT1 | | /dev/lp0 |
| Print spooler | LPT1 | Pipes printer jobs to the lpr command (\| lpr) | |
| WineLook | Win98 (how the system appears to apps: Win31, Win95, or the default Win98) | | |

Within the `/usr/share/wine-c` directory (that is, your C: drive), you should see some things that are familiar to you if you are coming from a Windows environment: `autoexec.bat` and `config.sys` files (empty to start with), and My Documents, Program Files, and windows directories.

Assuming that the basic directory structure is okay with you, you may still want to consider changing a few items. For example, you may want to change the command to print documents (set in the `/etc/wine.reg` file) to something other than the `"| lpr"` command to use a particular printer or add some Linux printing options.

## Setting up Windows applications

The best way to understand how to set up and run a Windows application is to step through the process of getting a simple Windows accessory to run in WINE. To do this procedure, you will need the following:

- The wine package installed in Red Hat Linux.
- Access to MS Windows components, including the executable program you want to run and the DLL files the executable needs to run.

If you have a dual-boot system (Red Hat Linux and Windows), the best way to do this procedure is to have Linux running with the Windows partition mounted somewhere so that you can copy the files you need. Otherwise, you should skip the first step and copy the files you need from a floppy or CD, or over the network.

In this example, we want to be able to run the Microsoft Paint program (`mspaint.exe`) from Windows in Linux using WINE. Here is an example of how to go about it.

1. If you have a dual-boot system you can start by mounting the Windows partition. Here's how:

    - As the root user, from a Terminal window, type

    ```
    # fdisk -l
    ```

    This lists your hard-disk partitions. Look for a partition that is listed as something like WIN95 FAT32.

    - Make a directory on which to mount your Windows partition. For example, to use the /mnt/win directory, type

    ```
    # mkdir /mnt/win
    ```

    - Assuming that the Windows partition is on the first partition of the first IDE hard disk (/dev/hda1), type the following to mount the Windows partition:

    ```
    # mount -t vfat /dev/hda1 /mnt/win
    ```

    At this point you should have a mounted Windows partition available from /mnt/win.

2. To make that partition permanently available to you from Linux, add the following line to your `/etc/fstab` file:

    ```
    /dev/hda1 /mnt/win vfat defaults 0 0
    ```

    The preceding entry causes the Windows partition to mount automatically on /mnt/win each time your Red Hat Linux system boots up.

    > **NOTE:** For the purposes of the rest of this procedure, I assume that you have a Windows system accessible from /mnt/win. If this is not the case, you need to find a way to copy files from your Windows system on another computer to the locations described in this procedure.

3. Copy the mspaint.exe program to a location accessible from your Linux computer. For example, with a mounted Windows partition as previously described, you could type

    ```
    # cp /mnt/win/Program\ files/Accessories/mspaint.exe /bin
    ```

4. Run the wine command with mspaint.exe as an argument to see if it can run or if it needs some added DLL files.

    ```
    # wine /bin/mspaint.exe
    err: module:PE_fixup_imports Module (file) MFC42.DLL (which is needed by Z:\a\mspaint.exe) not found
    ```

    This says that you need the mfc42.dll file to be able to run mspaint.exe.

5. Next, copy the necessary DLL file from the Windows partition. For example:

    ```
    # cd /usr/share/wine-c/windows/system
    # cp /mnt/win/windows/system/mfc42.dll mfc42.dll
    ```

6. With the proper DLL files installed, type `wine /bin/mspaint.exe` again and the MS Paint window opens. An example of the Paint window running in Red Hat Linux is shown in Figure 5-6.

![](img/1744bde8c889adfab3fc911e1687fecf_234_0.png)

Figure 5-6: Running Paint in Red Hat Linux using WINE.

In Figure 5-6, Paint is displaying a bitmap image that I opened from the Red Hat Linux file system. Choose File → Open. In the Open dialog box, you can see how the application views the locations available to it. The C:, D:, E:, F:, and Z: drives all represent the locations shown in Table 5-6. (The computer in the example didn’t have a floppy, or you would see an A: as well.)

## Finding Windows applications for WINE

Applications that have been tested to run under WINE are maintained at the Wine Application Database (http://appdb.codeweavers.com). The database is divided into the following categories:

- Games
- Learning Software and Computer-Based Training
- Multimedia
- Networking and Communications
- Productivity
- Programming/Software Engineering
- Reference, Documentation, and Information
- Scientific, Technical, and Mathematical
- Special Purpose

Hundreds of applications have been submitted for the database. Most of the packages that have been tested are games. In most cases, the person listing the application describes the platform he or she tested on and any experiences he or she had getting it to run. The host of the list, codeweavers.com, asks that you create a login to access the database.

## Running Macintosh applications with ARDI Executor

Besides enabling you to run many popular Macintosh applications on the PC, ARDI Executor (www.ardi.com) from ARDI, Inc. lets you work with Mac-formatted floppies and a variety of Mac drives. You can download RPMs of ARDI Executor from www.ardi.com/updates.php.

ARDI also maintains a listing of compatible Mac software in its Compatibility Database. There are literally hundreds of Mac applications listed. Each application is color coded (green, yellow, orange, red, or black) to indicate how well the software runs under ARDI. Green and yellow are fully usable and largely usable, respectively. Orange is mostly unusable. Red means the application won’t run at all, and black means it won’t run because it requires features that aren’t implemented in ARDI. At a glance, about two-thirds of the applications listed were either green or yellow.

## Summary

Between applications written directly for Linux and other UNIX systems, those that have been ported to Linux, and those that can run in emulation, there are hundreds of applications available that can be used with Red Hat Linux. There are dozens of locations on the Internet for downloading Linux applications, and many more that can be purchased on CD.

To simplify the process of installing and managing your Linux applications, Red Hat developed the Red Hat Package Manager (RPM). Using tools developed for RPM, such as the `rpm` command, you can easily install, remove, and do a variety of queries on Linux packages that are in RPM format.

Of the types of applications that can run in Linux, those created for the X Window System provide the greatest level of compatibility and flexibility when used in Linux. However, using emulation software, it is possible to run applications intended for DOS, Windows 95/98, and Macintosh operating systems.
