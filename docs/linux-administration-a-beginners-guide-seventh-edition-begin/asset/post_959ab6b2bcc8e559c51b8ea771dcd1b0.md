
## CHAPTER 4 Managing Software

NOTE A slight caveat applies here. As with Windows install/uninstall tools, the wonderful things that RPM can do are also dependent on the software package. For example, if a software application was badly packaged and its removal scripts were not properly formatted, you might still end up with bits of the package on your system, even after installing. This is one of the reasons why you should always get software only from trusted sources.

Removing software with RPM is easy and can be done in a single step. For example, to remove the lynx package that we installed earlier, we simply need to use the -e option, like

```
[root@fedora-server #] rpm -e lynx
```

This command will usually not give you any feedback if everything went well. To get a verbose output for the uninstallation process, add the -vvv option to the command.

A handy feature of RPM is that it will also protect you from removing packages that are needed by other packages. For example, if we try to remove the kernel-headers package (recall that the gcc package depends on it), we'd see the:

```
[root@fedora-server -#] rpm -e kernel-headers
error: Failed dependencies:
kernel-headers -> * is needed by (installed) glibc-headers->
```

> NOTE Remember that the glibc-headers* package required the kernel-headers package, too. And so RPM will do its best in helping you maintain a stable software environment. If you are about shooting yourself in the foot, RPM will also allow you to do that (perhaps because you know what you are doing).

If, for example, you wanted to perform the uninstallation of the kernel-headers package, you would add the --nodeps option to the uninstallation command, like:

```
[root@fedora-server -#] rpm --nodeps -e kernel-headers
```

## Other Things RPM Can Do

In addition to basic installation and uninstallation of packages with RPM, you can do numerous other things with it. In this section, we walk through some of these other functions.

## Verifying Packages

One of the most useful functionalities provided by the RPM tool is to verify a package by looking up the package information in its database, which is assumed to be good. It then compares information with the binaries and files that are on your system.

# 100 Linux Administration: A Beginner's Guide

In today's Internet world, where being hacked is a real possibility, this kind of test should tell you instantly if anyone has tampered with the software installed on your system. For example, to verify that the Bash package is as it should be, you type the following:

```
root@fedora-server # rpm -V bash
```

The absence of any output is a good sign. You can verify specific files on the file system that a particular package installed. For example, to verify that the /bin/ls command is valid, you would type this:

```
root@fedora-server # rpm -Vf /bin/ls
```

Again, the lack of output is a good sign. If something was amiss—example, by a different version—the verify output might be similar to this:

```
root@fedora-server # rpm -Vf /bin/ls
SM5....T. /usr/bin/ls
```

If something is wrong, in RPM will inform you of what test failed. Some examples are the MD5 checksum test, file size, and modification times. The moral of the story is that RPM is an ally in finding what is wrong with your system. Table 4-1 provides a summary of the various error codes and their meanings. You can use the following command to verify all the packages installed on your system:

```
root@fedora-server # rpm -Va
```

This command verifies all the packages installed on your system. That's a lot of files, so you might have to give it some time to complete.

| Code | Meaning |
|---|---|
| S | File size differs |
| M | Mode differs (includes permissions and file type) |
| 5 | MD5 sum differs |
| D | Device/minor number mismatch |
| L | readLink-path mismatch |
| U | User ownership differs |
| G | Group ownership differs |
| T | Modification Time (mtime) differs |

Table 4-1 RPM Verification Error Attributes

## CHAPTER 4 Managing Software

# 101

## Package Validation

Another feature of RPM is that it allows the packages to be digitally signed. This provides a type of built-in authentication mechanism that allows a user to ascertain whether the package in his her possession was truly packaged by the expected (trusted) party and also that the package has not been tampered with. This explains why you might see some warnings when trying to install a package (such as this message: lynx.rpm: Header V3:SHA256 Signature, KEY ID: NOKEY). To prevent this warning, you should import Fedora's digital key into your system (replace <VERSION> with your version of Fedora):

```
[root@fedora-server ~]# rpm --import \
/etc/pki/rpm-gpg/fedora
```

You might also have to import other vendors' keys into the keyring. To be certain that local key you have is not a duplicate, you can import the key directly from the vendor's web site. For instance, to import from Fedora's project site, you would replace <KEY_FILE> in the next command with the correct value:

```
[root@fedora-server ~]# rpm --import \
https://fedora.org/static/<KEY_FILE>
```

You will find a listing of the current keys on the Fedora project site here: https://fedora.org/keys/. For example, for Fedora version 23, the full syntax for the rpm command is:

```
[root@fedora-server ~]# rpm --import \
https://fedora.org/static/RPM-G.txt
```

Table 4-2 shows a list of frequently used rpm options and is provided here for quick reference.

| Command-Line Option | Description |
|---|---|
| --install | Installs a new package. |
| --upgrade | Upgrades or installs the package currently installed to a newer version. |
| --erase | Removes or erases an installed package. |
| --query | Used for querying or retrieving information about installed (or uninstalled) packages. |

Table 4-2 Common RPM Options

# Linux Administration: A Beginner's Guide

| Command-Line Option | Description |
|---|---|
| --force | Tells RPM to forego sanity checks and just do it, even if you're trying to fit a square peg into a round hole. Be careful with it is the sledgehammer of installation. Typically you use it when you're knowingly installing an odd or unusual configuration. |
| -h | Prints hash marks to indicate progress during an installation. Use with the -v option for a pretty display. |
| --percent | Prints the percentage completed to indicate progress. It's handy if you're running RPM from another program, such as a Perl script, and you want to know the status of the installation. |
| -nodeps | Causes RPM to not perform any dependency checks if RPM is complaining about missing files, but you want the installation to happen anyway. |
| -q | Queries the RPM system for information. |
| --test | Checks to see whether an installation would succeed without performing an actual installation. If it anticipates problems, it displays what they will be. |
| -V | Verifies RPMs or files on the system. |
| -v | Tells RPM to be verbose about its actions. |

Table 4-2 Common RPM Options (Continued)

## Yum

Yum is one of the more popular packaging/updating tools for managing software on Linux systems. It is basically a wrapper program for RPM, with great enhancements. It has been around for a while and is now quite mature. Yum has changed and enhanced the traditional approach to package management on RPM-based systems. Popular large sites that serve as repositories for open source software have had to retool slightly to accommodate “Yumified” repositories.

## CHAPTER 4 Managing Software 103

According to the Yum project's web page (http://yum.base.org/):

“Yum is an automatic updater and package installer/remover for rpm systems. It automatically computes dependencies and figures out what things should occur to install packages. It makes it easier to maintain groups of machines without having to manually update each one using rpm.

This summary is an understatement. Yum can do a lot. Several Linux distributions rely heavily on the capabilities provided by Yum.

Using Yum is simple on supported systems. You mostly need a single configuration file (/etc/yum.conf). Other configuration files can be stored under the /etc/yum.repos.d/ directory that points to other Yum-enabled (Yumified) software repositories. Fortunately, several Linux distributions have Yum already installed and preconfigured. Fedora is one such distro.

To use Yum on a Fedora system (or any other Red Hat-like distro) to install a package gcc, for example, you would follow the following at the command line:

```
root@fedora-server # yum install gcc
```

Yum will automatically take care of any dependencies that the package might need and install the package for you. (The first time it runs, it will build its local cache.) Yum also has extensive capabilities that will help you find a package, even if you don't know its correct name. All you need to know is part of the name. For example, if you want to search for all packages that have the word “headers” in the name, you can try a Yum option like this:

```
root@fedora-server # yum search headers
```

This will return a list of matches. You can look through the list and pick the package you want.

> NOTE By default, Yum tries to access repositories that are located somewhere on the Internet. Your system needs to be able to access the Internet to use Yum in its default state. You can create your own local software repository on the local file system or on your local area network (LAN) and Yumify it. Simply copy the entire contents of the distribution media (DVD/CD) and run the creerepo command against the directory location.

## DNF

DNF is the new package manager slated to replace Yum on Red Hat-type distros. It is feature compatible with Yum and supports virtually all the options that Yum supports, Users of Yum should be able to literally replace the word yum with the word dnf for all package management needs when using the program from the command line.
