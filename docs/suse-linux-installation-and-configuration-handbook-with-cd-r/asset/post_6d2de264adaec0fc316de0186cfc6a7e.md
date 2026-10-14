
## Using cpio to Back Up Your Files

YaST isn't the only utility you can use to perform the backup operations described in the previous section "Back Up Using YaST." SuSE Linux offers another important tool with a large degree of scalability: cpio.

cpio is famous for its ease of use and archiving capabilities. It supports archiving and extracting large numbers of archive formats. cpio is short for Copy In/Out, which describes the program behavior. In fact, cpio can be used to copy pass data, which is typically the same as mirroring a directory tree from one path to another.

### Out Mode

When you back up your data, you need to use cpio's out mode. Think of cpio as a pipe you use to pipe your data in so that it goes out the other side as an archive. Consider the following example:

```
bash# ls | cpio -ov > backup.cpio
```

In this example, you pipe the directory listing to cpio, which reads the files, generates an archive, and redirects the output to a backup.cpio file. The -o option tells cpio to generate an archive of the listing sent to it. The -v option tells cpio to be verbose when adding files.

The way files are passed to cpio might seem odd to you, but, after you've used it a while, you will realize the power it gives you. In fact, with some knowledge of shell scripting, you can create a selective archive using cpio. Consider the following command:

```
bash# cd /home; find . -print -depth | cpio -ov > home.cpio
```

This command will back up the /home directory into home.cpio.

### In Mode

To restore the data you back up using cpio, you should use cpio's in mode. The -i option tells cpio to restore the data out of the archive and in the location specified. For example, to restore the home.cpio file, enter the following command:

```
bash# cpio -idvu < home.cpio
```

The -d option tells cpio to create subdirectories when required. The -u option tells cpio to overwrite files in the directory if files with the same name exist. You should use this option with caution.

### Other Backup Software

If SuSE Linux is running important databases based on advanced products such as Oracle or Informix databases, you might want to increase the security of your backups by using advanced backup packages.

One of the most famous packages SuSE recommends to use in mission-critical systems is Time Navigator by Quadratec (http://www.quadratec-software.com). Time Navigator is an advanced package that can be used to integrate and back up giant databases on SuSE Linux. Visit their Web site for more information on the availability of the package. ●

## System Upgrade

### In this chapter

- Upgrading Your Linux 132
- Precautions Prior to Package Installations 132
- Upgrading SuSE Linux 133
- Upgrading Your X Window System 136
- Upgrading Your KDE 140
- Upgrading GNOME 145
- Upgrading an Existing Library 152
- Upgrading Your GCC 154
- Troubleshooting 155

## Upgrading Your Linux

SuSE Linux comes with so many packages and applications, one may never need to look elsewhere. The question here is, are you going to need to upgrade any of its components? Well, that depends on how you use your SuSE Linux. If you use it as a server for a small network or small number of users, you might never need to touch it after it's up and running. If you are using it as a server for a large network, you might need to upgrade a few packages to fix security or performance bugs, or to get new features. If you are using it on a desktop computer, then you might want to upgrade a lot of your applications as newer versions are released. The key is to only upgrade when you need to.

## Precautions Prior to Package Installations

If you are running SuSE Linux as a server that handles users, then you have to be very careful when upgrading packages—both in the decision to upgrade and the actual process of upgrading. Before you decide to upgrade a package, you have to read about all the changes that this new version will bring and make sure that it does not break any existing data files. If, for example, you are upgrading your mail reader and the new version is not compatible with the old version's configuration files, then your users will be very upset when they find out that they have to reconfigure their software. But, if you have to upgrade to this version, for instance for security reasons, then at least inform your users of this upcoming change beforehand.

Another consideration is the actual upgrade process. You don't want to upgrade a package of applications when you have users connected. A user might be using that application now, and this might conflict with your upgrade process. Some applications you can upgrade with users logged on, for example, applications that are used only by root.

So, how can you make sure that you do not have users logged on while you are upgrading your packages? Unplugging the network cable is one way; but there are less physical methods of achieving the same goal. You can switch Linux to single-user mode or just turn off the network.

Turning off the network will stop any users from being able to log on the machine. To do this, simply go to /sbin/init.d/ and execute the following commands:

```
# cd /sbin/init.d/
# ./network stop
```

Now the network is down. Just make sure that you inform your users beforehand that the server will be down for a while. After you are done with your upgrades, you can bring the network back up:

```
# ./network start
```

Now that the network is back up, users can start to log on to the system again. For major system upgrades, you might want to switch Linux to single-user mode. To do this, run the following command:

```
# telinit 5
```

This command will switch Linux to single-user mode. To get back to a multiuser system with the network, enter the following command:

```
# telinit 2
```

Or if you want to go back to multiuser mode with the network and xdm/kdm, enter this command:

```
# telinit 3
```

More information on telinit can be found in Chapter 9, "Configuring the System Boot Up Sequence."

## Upgrading SuSE Linux

SuSE constantly upgrades its packages as new versions are released. The new packages might contain important bug and security fixes. SuSE prepares those new releases in RPM packages that install flawlessly on your system. They also provide the source RPMs if you want to compile the packages yourself. Source RPMs are good because SuSE fine-tunes them to work best on their distribution.

So, how do you know if there is a new set of updated packages for your system? Well, you can find this out in many ways. You can start by checking the SuSE Web site at http://www.suse.com. Follow these steps:

- 1. Start your browser at this address.
- 2. Click Updates. You will be taken to a page that organizes the available updates by distribution version.
- 3. Click your version. You will be taken to another page that lists all the available new updates for your distribution along with a fairly detailed description of each one. The packages are listed by series.

### Installing New Packages from Your Hard Disk

Now that you know there are new updated packages, you can start to install them right away. This is easy; just follow these steps:

- 1. Click the packages' names (while holding down the Shift key if you are using Netscape Navigator) to start downloading them to your hard disk.
- 2. When you have all the packages you want on your hard disk, you can install them using one of two methods—YaST or manually. Both are easy to perform. Let's start with the manual method.

### Installing Packages Manually

To install the packages manually, all you have to do is issue the rpm command. For example, let's say you downloaded all the packages in a directory called /tmp/updates. Follow these steps:

- 1. Log in as root.
- 2. Turn off the network if you do not want to have users logged on while you perform the upgrade.
- 3. Change the current path to the directory that has the RPMs you want to install:
- 4. Then, use the following rpm command to install them all in one run:

```
# cd /tmp/updates
```

```
# rpm -Uvh *
```

If rpm finds an old version of one of the packages, it will upgrade it; if not, it will install the new package. rpm will go through all the new packages and install them.

### Installing Packages Using YaST

If you do not want to use the manual method, you can always use YaST to install the new packages. Follow these steps:

- 1. Run YaST, choosing Choose/Install Packages.
- 2. Now that you are in the Installation Menu, choose Install packages, as in Figure 7.1.

FIGURE 7.1
YaST installation menu.

![](img/659f91d9da7b29976c0625e2e9628511_159_0.png)

3. Tell SuSE where to get your packages. At the Source: (None) field, press Enter to get a list of the installation sources YaST can use, as shown in Figure 7.2.

FIGURE 7.2
Installation sources YaST can use.

![](img/659f91d9da7b29976c0625e2e9628511_159_1.png)
