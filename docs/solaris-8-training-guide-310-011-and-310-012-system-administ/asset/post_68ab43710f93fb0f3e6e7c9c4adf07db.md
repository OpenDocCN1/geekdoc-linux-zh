
## OBJECTIVES

The following is the test objective for this chapter:

### Understand the tools for managing software

Sun provides several standard tools for managing software on Solaris. This chapter describes all of these tools for performing the following tasks:

- Add and remove software packages
- List and verify installed software packages
- Install and remove software patches

One of the system administrator's primary responsibilities is to add and remove Solaris software packages, including software patches. A complete understanding of the methods and commands used to accomplish these tasks is critical.

## Software Package Administration

- Introduction 135
- Tools for Managing Software 135
- Adding and Removing Software Packages 136
- Using a Spool Directory 138
  - Adding Software Packages Using Admintool 139
  - Removing Software Packages Using Admintool 141
  - Solaris Product Registry 142
- Listing and Verifying Installed Packages 145
- Software Patches 146
  - Installing a Patch 147
  - Removing a Patch 151
  - General Guidelines 152
- Summary 153
- Apply Your Knowledge 154

The following strategies will help you study for the exam:

- When studying this chapter, I suggest that you practice the step-by-step examples that I've outlined on either a Sun system or an Intel-based system running the Solaris 8 operating system. Practice all of the step-by-step examples until you can perform them from memory.
- Become familiar with all the tools used to manage software on a Solaris system. Understand which tool is best for a particular circumstance.
- Understand the terms used in this chapter to describe how Sun packages their software. For your convenience, the important terms are listed at the end of this chapter. Many of these terms will be on the actual exam.
- Finally, make sure you understand the operating system patching process. Pay special attention to how to obtain patches, how to install them, and how to verify patches on your system.

## INTRODUCTION

The system administrator is responsible for managing all software installed on a system. Installing and removing software is a routine task that is performed frequently. Chapter 3, “Installing the Solaris 8 Software,” described the installation of the Solaris operating system. This chapter explains how to add and remove additional applications after the operating system has already been installed.

Sun and its third-party vendors deliver software products in a form called a software package. The term *package* refers to a method of distributing and installing software to systems where the products will be used. A package is a collection of files and directories in a defined format that conforms to the Application Binary Interface (ABI), a supplement to the System V Interface Definition. The Solaris operating environment provides a set of utilities that interpret the ABI format, and provides the means to install or remove a package or to verify its installation.

## TOOLS FOR MANAGING SOFTWARE

Solaris provides the tools for adding and removing software from a system. These are described in Table 4.1.

**TABLE 4.1**

**TOOLS FOR MANAGING SOFTWARE**

| Command | Description |
|---|---|
| *Managing Software from the Command Line* | |
| `pkgadd` | Adds software packages to the system |
| `pkgrm` | Removes software packages from the system |
| `pkgchk` | Checks the accuracy of a software package installation |
| `pkginfo` | Displays software package information |
| `pkgask` | Stores answers in a response file so that they can be supplied automatically during an installation |
| `pkgparam` | Displays package parameter values |

**TABLE 4.1 continued**

**Tools for Managing Software**

| Command | Description |
|---|---|
| *Managing Software from the Graphical User Interface* | |
| admintool | Invokes from within CDE or Openwindows |
| Solaris Product Registry | Manages all of your Solaris software. |

Use the pkgadd or pkgrm commands directly from the command line to load or remove software packages. The pkgadd and pkgrm commands can be incorporated into scripts to automate the software installation process. Many third-party vendors use pkgadd in scripts as a means of installing their software.

Admintool, on the other hand, provides an easy-to-use interface for installing and removing software packages. It is simply a graphical user interface to the pkgadd and pkgrm commands. Using the Admintool graphical interface is a convenient way to view software already installed on a system or to view the software that resides on the installation media. If you're unfamiliar with software-package naming conventions, if you are uncomfortable using command-line options, or if you're managing software on only one system at a time, you'll find Admintool an easy way to add and remove software packages.

New in Solaris 8 is the Solaris Product Registry, a system for maintaining records of the software products installed on a Solaris system. The Product Registry includes a GUI tool to make managing your Solaris software easier. The Product Registry allows you to install, list, or uninstall Solaris software packages or clusters.

## ADDING AND REMOVING SOFTWARE PACKAGES

When you add a software package, the pkgadd command decompresses and copies files from the installation media, such as the CD-ROM, to a local system's disk. When you use packages, files are delivered in package format, and are unusable as they are delivered.

The pkgadd command interprets the software package's control files and then decompresses the product files and installs them on the system's local disk.

You should know the following things before installing additional application software:

- Sun packages always begin with the prefix SUNW, as in SUNWvolr, SUNWadmap, and SUNWab2m. Third-party packages usually begin with a prefix that corresponds to the company's stock symbol.
- You can use the pkginfo command or Admintool to view software already installed on a system.
- Clients might have software that resides partially on a server and partially on the client. If this is the case, adding software for the client requires adding packages to both the server and the client.
- You need to know where the software will be installed, and you need to make sure you have a file system that has enough disk space to store the application software. If you know the name of the software package, you can use the pkgparam command to determine where the package will be loaded. For example, to find out information about the SUNWvolr package, type the following:

```
pkgparam -d /cdrom/cdrom0/s0/Solaris_2.8/Product SUNWvolr SUNW_PKGTYPE
```

SUNW_PKGTYPE is a special parameter that reports where a Solaris software package will be installed. If the package does not have the SUNW_PKGTYPE parameter set, the pkgparam command returns an empty string. For Sun packages, this usually means that the package will be installed in /opt.

The system responds with the location where the application will be stored:

```
root
```

> NOTE It's not always clear what the pkgid is for a particular software package or application until it is actually installed. Sometimes the release documentation that came with the package will tell you the name of the pkgid. Other times you might need to call the vendor to get the pkgid information.

CAUTION
When you remove a package, the pkgrm command deletes all the files associated with that package unless those files are also shared with other packages. If the files are shared with another package, a system message will warn you that other packages use these files, and you will be prompted if you want to remove them anyway. Be sure you do not delete application software without using pkgrm. For example, some system administrators delete an application simply by removing the directory containing the application software. With this method, files belonging to the application that might reside in other directories are missed. With pkgrm, you'll be assured of removing all files associated with the application.

NOTE
Copying packages to a spool directory is not the same as installing the packages on a system.

Although the pkgadd and pkgrm commands do not log their output to a standard location, they do keep track of the product installed or removed. The pkgadd and pkgrm commands store information in a software product database about a package that has been installed or removed. By updating this database, the pkgadd and pkgrm commands keep a record of all software products installed on the system.

## USING A SPOOL DIRECTORY

For convenience, you can copy frequently installed packages to a spool directory. If you copy packages to the default spool directory, /var/spool/pkg, you do not need to specify the source location of the package when using the pkgadd command. The pkgadd command, by default, will look in the /var/spool/pkg directory for any packages specified on the command line.

## STEP BY STEP

### 4.1 Adding a Package to the Spool Directory

To add a package to the spool directory named /var/spool/pkg, follow these steps:

1. Log in as root.
2. Make sure the spool directory exists.
3. Add a software package to a spool directory using the pkgadd command as follows:

```
pkgadd -d <device-name> -s <spool directory> <pkgid>
```

in which

- `-d <device-name>` specifies the absolute path to the software package. `<device-name>` can be the path to a device, a directory, or a spool directory.
- `-s <spool dir>`. Specifies the name of the spool directory where the software package will be spooled. You must specify a `<spool dir>`, a directory where the software will be put.
