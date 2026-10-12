
why we have the command-line version, too. To run the graphical package management tool, go to the Red Hat menu, and from System Settings, select Packages. You can also go to a command line and run:

```
[rwhite@edford ~]$ redhat-config-packages
```

Either way you start the package manager, it will check to see if you are the root user. If you are not, it will open a window like the one shown, in which you can enter the root password to run the utility with root’s permissions.

![](img/ec2066d370d3af1a767664d36aa7ddfe_119_0.png)

Once you have successfully entered the root password, the package manager will check to see what packages are already installed on the system. You will be able to select packages for installation or removal in exactly the same way you did during the Red Hat Linux 8.0 installation. This is a welcome update to the look and feel of the package manager. As during installation, whole groups of packages can be selected (see Figure 4-1), or specific packages can be manipulated.

### **Project 4-2 Getting Apt**

The Debian distribution and a few others use a non-RPM package manager that adherents much prefer to RPM. The Debian package manager, apt, does a better job of handling dependencies automatically than RPM does. Some people like to use apt on their RPM-based systems, too, and so the folks at the Conectiva distribution made a version available that handles RPM installations. Now the same thing is available for Red Hat users. To install and use apt, you’ll have to build upon your RPM installation skills.

![](img/ec2066d370d3af1a767664d36aa7ddfe_120_0.png)

**Figure 4-1** The redhat-config-packages tool uses the same interface as the package selector used during Red Hat Linux 8.0 installation.

#### Step by Step

- 1. Go to http://psyche.freshrpms.net and find the apt package.
- 2. Download the apt package and install it (as root) using `rpm -ivh`.
- 3. Run `apt-get update` to download package information from the freshrpms.net site.
- 4. Run `apt-get -f install` to verify apt's installation integrity.
- 5. Download an apt GUI manager by running `apt-get install synaptic`.
- 6. Test the synaptic installation by running `synaptic`.

Many other packages can be installed from the command line using **apt-get install** and specifying the package name, or by using the synaptic GUI shown.

![](img/ec2066d370d3af1a767664d36aa7ddfe_121_0.png)

For some purposes, such as loading the many desktop-enhancing files available from freshrpms.net, these tools are even easier than RPM. Many server installations might not be good guinea pigs for using apt, however. Consider whether you want to be using non-Red Hat packages on a server you want to run mission-critical services. In the end, installing apt is not only a way of practicing use of RPMs, it’s also a way of starting to think about security policies, which I’ll address in more detail in Module 9.

## **4.2 Compiling Software Yourself**

One of the key benefits of open-source software is that you have the source code in your hands. If the developer chooses to stop working on it, you can continue. If you find a problem, you can fix it. In other words, you are in control of the situation and not at the mercy of a commercial developer you can’t control. But having the source code means you need to be able to compile it, too. Otherwise all you have is a bunch of text files that can’t do much. Although almost every piece of software in this book is available as an RPM, you should step through the process of compiling it yourself so that you can pick and choose compile-time options, which is something that you can’t do with RPMs. Thus, it’s a good idea to become comfortable with compiling packages yourself.

In this section, you will step through the process of compiling the KDirStat package, a graphical tool for viewing directory sizes. You can download KDirStat from http://kdirstat.sourceforge.net. KDirStat is a typical package; you’ll find that most other packages that you need to compile follow the same general pattern.

![](img/ec2066d370d3af1a767664d36aa7ddfe_122_0.png)

> KDirStat is not an essential package for managing your Red Hat Linux system; its functionality is similar to that of the **du** utility, which provides disk usage information for the directories you specify.

### Getting and Unpacking the Package

Software that comes in source form is often made available as a *tarball*—that is, it is archived into a single large file and then compressed. The tools used to do this are **tar** and **gzip** or **bzip2**; **tar** handles the process of combining many files into a single large file, and **gzip** or **bzip2** is responsible for the compression.

![](img/ec2066d370d3af1a767664d36aa7ddfe_122_1.png)

> Do not confuse **gzip** and **bzip2** with WinZip. They are different programs that use different methods of compression. It should be noted, though, that WinZip does know how to handle tarballs.

Typically, a single directory is selected in which to build and store tarballs. This allows the system administrator to keep the tarball of each package in a safe place in the event he or she needs to pull something out of it later. It also lets all the administrators know which packages are installed on the system in addition to the base system. A good directory for this is /usr/local/src, since software local to a site is generally installed in /usr/local. The downside of using the /usr/local/src directory to store source code is that the root user must be used to build the software there, not just install it. In most cases, software installed from tarballs *can* be built by a normal user and then installed by the root user, but because of the default directory permissions in /usr/local/src, normal users cannot build the software there.

When unpacked, most tarballs create a new directory for all of its files. The KDirStat tarball (*kdirstat-2.2.0.tgz*), for example, creates the subdirectory *kdirstat-2.2.0*. Most packages follow this standard. If you find a package that does not follow it, it is a good idea to create a subdirectory with a reasonable name and place all the unpacked source files there. This allows multiple builds to occur at the same time without the risk of the two builds conflicting.

![](img/ec2066d370d3af1a767664d36aa7ddfe_123_0.png)

> While tarballs often end in *.tar.gz* or *.tar.bz2*, you may also see files ending in *.tgz*. These are also tarballs; their file extension is a sort of contraction of *.tar* and *.gz*.

Begin by downloading the KDirStat source tarball. You can fetch it from its web site at http://kdirstat.sourceforge.net/

To unpack the KDirStat tarball, first become *root*, and then move the file into the /usr/local/src directory, like so:

```
[rwhite@tedford ~]$ su -
[root@tedford /root]# mv ~/kdirstat-2.2.0.tgz /usr/local/src
```

Once there, use the *cd* command to change directories to /usr/local/src, like so:

```
[root@tedford /root]# cd /usr/local/src
```

Then unpack the tarball with the following command:

```
[root@tedford src]# tar -xvzf kdirstat-2.2.0.tgz
```

The *z* parameter in the *tar* command invokes *gzip* to decompress the file before the untar process occurs. The *v* parameter tells *tar* to show the name of the file it is untarring as it goes through the process. This way, you'll know the name of the directory where all the sources are being unpacked. You should now have a directory called /usr/local/src/kdirstat-2.2.0. You can test this by using the cd command to move into it:

```
[root@tedford src]# cd /usr/local/src/kdirstat-2.2.0
```

### Looking for Documentation

Once you are inside the directory with all of the source code, begin looking for documentation. *Always read the documentation that comes with the source code!* If there are any special compile directions, notes, or warnings, they will most likely be mentioned here. You will save yourself a great deal of agony by reading the relevant files first.

So then, what are the relevant files? Typically there are two files in a distribution: README and INSTALL, both of which are located in the root of the source code directory. The README file generally includes a description of the package, references to additional documentation (including the installation documentation), and references to the author of the package. The INSTALL file typically has directions for compiling and installing the package.

These are not, of course, absolutes. Every package has its quirks. The best way to find out is to simply list the directory contents and look for obvious signs of additional documentation. In the case of KDirStat, there is a file named README, and another named INSTALL. Some packages use different capitalization: readme, README, ReadMe, and so on; some introduce variations on a theme: README.1ST or README.NOW, and so on.

Another common place for additional information is a subdirectory that is appropriately called “doc” or “documentation.” In the case of KDirStat, the doc directory contains source files for building the documentation.

To view a text file, use the more command:

```
[root@tedford kdirstat-2.2.0]# more README
```

To view the text file in an editor, use the pico command:

```
[root@tedford kdirstat-2.2.0]# pico README
```

![](img/ec2066d370d3af1a767664d36aa7ddfe_124_0.png)

To get a quick list of all the directories in a source tree, enter the command:

```
[root@tedford kdirstat-2.2.0]# ls -l | grep drwx
```
