
partition on the disk. The command to boot from this partition would be typed at the boot prompt like this:

```
boot ro root=/dev/hda1
```

This tells LILO to find the kernel to boot from on that partition. You should use the proper partition name, of course, and a Linux kernel must be there to read.

After you have booted the system from floppy, run LILO to set up the boot sequence the way you want it.

## Using dmesg

If you have devices that are not recognized properly after booting, you should check the boot messages your system generates. You can see all the messages by typing the command dmesg at the shell prompt. If a device is not recognized properly, you will see one or more lines in the dmesg output about that device. For example, if your network card is not properly detected you may see messages like this:

```
loading device 'eth0'... 
ne.c:v1.10 9/23/94 Donald Becker (becker@cesdis.gsfc.nasa.gov)
NE*000 ethercard probe at 0x300: 00 00 6e 24 1e 3e
eth0: NE2000 not found at 0x300
eth0 not loaded
```

As was mentioned, this error almost always occurs because you provided the wrong configuration information. In the case of the network card above, the IO address on the card was 330H not 300H. Running the setup utility again lets you change these parameters.

## Changing Disk Partitions

Whether your system had Windows or DOS on before Linux, or maybe just has Linux now, in the future you may want to modify the layout of the disk drivers to allow other operating systems to be loaded. If you want to modify your partitions' sizes, there are several commercial products (such as PartitionMagic from PowerQuest Corporation) that can do the job, but there's also a tool we've looked at in earlier chapters that works just fine under DOS and Windows—FIPS. FIPS lets you size existing partitions without requiring a full backup-reformat-restore operation.

You've already seen how to run FIPS from the DOS or Windows prompt. Prior to running FIPS, you should defragment your file system using one of the utilities included with DOS or Windows for that task, and then run FIPS to create new partitions or remove existing ones.

![](img/e8e6b47ac20475e23d48b4c476f5d891_128_0.png)

If you've installed Linux, you're not out of luck: You can boot off a floppy disk and use the Linux CD-ROM to run FIPS, or copy FIPS to your boot floppy when in Linux. You can use this technique to convert an all-Linux disk to a shared Linux-Windows disk. You should not run FIPS from the Linux directory, even under an emulator software package such as Wabi because the results are not predictable.

### Installing Additional Software

So your Linux system is up and running, but you want more software? There are several sources of additional software you can load on your system, including CD-ROMs, WWW pages, and FTP sites. You can also purchase software from vendors. In some cases, software includes an installation utility that needs to be run to install the package properly. Commercial software is usually like this, as you will see in Part VIII of this book when we look at some commercial applications.

For other applications, especially those that come in the disk sets that most CD-ROM versions of Linux include, you must use a package tool such as *installpkg*, *pkgtool*, or *pkgadd*. The name of the tool differs considerably, depending on your version and release of Linux, so you should check the documentation that came with your system for the exact name and actions necessary to add software. As an example of the process, we can look at two different tools. The first is RPM (Red Hat Package Manager), and the second is *installpkg* (which is available with many versions of Linux).

#### RPM

RPM is not restricted to Red Hat Linux; it has appeared in several different versions of Linux. RPM is a character-based system that allows you to build, install, query, verify, update, and uninstall software packages. (A software package in Linux terms consists of an archive of files and information about that package, such as the package name, version number, and a brief description.) RPM has ten modes of operation, each with a different set of options. This can make RPM a little confusing to work with, although most of the uses are straightforward. RPM's modes and their purposes are shown in Table 5.1.

**TABLE 5.1. RPM'S MODES AND WHAT THEY ARE USED FOR.**

| Mode name | Command line | Used for |
|---|---|---|
| Build | `rpm -[bit]0` | Build a package |
| Fix permissions | `rpm --setperms` | Fix the permissions on a package |
| Install | `rpm -i` | Adding new software |
| Query | `rpm -q` | Check to see what packages and files are installed |
| Rebuild Database | `rpm --rebuilddb` | Rebuild the package database |
| Set owners and groups | `rpm --setugids` | Set the owner and group of a package |
| Show RC | `rpm --showrc` | |
| Signature check | `rpm --checksig` | Check the package to ensure there are no errors |
| Uninstall | `rpm -e` | Remove a package |
| Verify | `rpm -Vl-yi` / `--verify` | Verify that a package is installed properly (all files installed) |

We won't bother with a lot of detail about all these options because most are self-explanatory and covered in the documentation, but a few common-usage examples will help you become more familiar with RPM. To install software with RPM, you need to specify the package name that you want to install. The syntax of the install command is as follows:

```
`rpm -i [install-options] <package_filename>`
```

There are dozens of installation options possible, most of which don't do very much except modify the behavior of RPM slightly. A few of the more useful installation options for RPM are:

- **allfiles.** Installs or upgrades all the files in the package.
- **force.** The same as using *replacepkgs*, *replacefiles*, and *oldpackage* together.
- **h** or **--hash.** Displays 50 hash marks as the package archive is unpacked to show the system is working (use with the `-v` option for a nicely formatted status display).
- **includedocs.** Installs documentation files (usually done by default).
- **ignores.** Forces installation or upgrading if the operating systems of the RPM and the host are not the same.
- **keep-temps.** Keeps temporary files created during the installation process, useful for debugging installation problems.
- **percent.** Displays progress percentages as files are unpacked (intended to make RPM easy to run from scripts).
- **quiet.** Displays a minimal set of messages (but all error messages).
- **replacefiles.** Installs the package even if new files replace files from already installed packages.
- **replacepkgs.** Installs the package(s) even if they are already installed.
- **test.** Does not install but checks for conflicts.

Check the man page for a full list of options. The package name to be added is usually given as a complete path, although a URL is also possible with many versions of RPM. To install a package called Xgames, the command would be given like this:

```
`rpm -i /mnt/cdrom/col/install/Xgames.rpm`
```

In this case, the package is called Xgames.rpm, and the full path to the package is given (this one is on a CD-ROM in the col—collections—directory).

The verify mode of the RPM command is handy for making certain that all portions of a package have been installed and still exist on your system. This is sometimes necessary after installing other packages that may overwrite part of an existing package. When you verify a package, RPM compares information about the installed files in the package with information about the files taken from the original package and stored in the RPM database. Among other things, verifying compares the filename, size, check sum, permissions, type, owner, and group of each file. Any discrepancies in the comparison are displayed on the screen.

To use the verify mode of RPM, use the command with the -w option and the package name. RPM will use one of these eight characters to show a failure of one of the tests:

- 5: MD5 sum (checksum)
- S: File size incorrect
- L: Symbolic link incorrect
- T: Time incorrect
- D: Device incorrect
- U: User owner incorrect
- G: Group owner incorrect
- M: Mode incorrect (includes permissions and file types)

If you find errors in a package, it is usually easiest to reinstall the package.
