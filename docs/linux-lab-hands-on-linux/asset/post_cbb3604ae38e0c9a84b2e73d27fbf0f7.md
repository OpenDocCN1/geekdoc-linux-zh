
3. Press the **CTRL+R** to insert another file in the current one. You are prompted to type the file name.

4. Type file name that you want to insert and press the **ENTER** key (Figure 14).

![](img/f3b9cff79e19317416c12eaf5ded7245_102_0.png)

5. Press the **CTRL+C** to find the position of cursor.

![](img/f3b9cff79e19317416c12eaf5ded7245_102_1.png)

The cursor position is displayed on the third line from the bottom (Figure 16).

6. Press **CTRL+X** to close file.

![](img/f3b9cff79e19317416c12eaf5ded7245_103_0.png)

7. You are prompted whether you want to save the file or not. Press `Y` for saving file and `n` for closing the file without saving (Figure 17).

![](img/f3b9cff79e19317416c12eaf5ded7245_103_1.png)

As soon as you press `n`, the file will be closed and you will be quit from the nano window. The Terminal window again appears, as shown in Figure 18:

![](img/f3b9cff79e19317416c12eaf5ded7245_104_0.png)

With this we come to the end of this lab.

Let's summarize the main points of the Lab.

## Summary

In this lab, you worked on two most popular Linux editors vi and nano. The different commands that are used for opening the file, editing, deleting, saving files and quitting the editor have been discussed for both the editors. An activity is performed to work on a file on vi and nano editors.

# NOTES

# 09
# LAB: Software Management

## OBJECTIVES

- Install and remove RPM packages
- Query packages and verify their state
- Manage packages using YUM
- Understand the relationship between YUM and RPM
- Rebuild and modify existing source RPMS

## REQUIREMENTS

P-IV class PC with FC6 or RHEL- 5, and Linux Distro CD/DVD.

## CONCEPT

Linux distributions use the popular Redhat Package Manager or RPM, system of adding or removing programs. Almost all Linux users will encounter the desire to add software to their computer. or remove a program that came with their version of Linux. You can also querying the package to know the status of the RPM. The query package systems offer many benefits. As a user, you can find what packages are installed on the system and their versions. While working with Linux you can develop a real taste for YUM (Yellow dog Updater Modified), an automatic update and package installer/remover for RPM systems.

### RPM Overview

RPM is a powerful command line driven package management system capable to install, uninstall, verify, query, and update computer software packages. Each software package consists of an archive of files along with information about the version and description of the package.

This lab uses rpm to deals with:

- Installing software
- Querying software
- Removing software

### Basic RPM Commands

The basic RPM commands are as follows:

- `U`: Lets you update or install the selected package. This can be done via http or ftp in addition to using local files.
- `i`: Allows you to install the selected package for multiple versions.
- `e`: Allows you to remove the packages you specify.
- `v`: Lets printout more information than usual. V stands for verbose.
- `F`: Works only if an earlier version of the package is already installed. F stands for freshen.
- `h`: Lets you improve the appearance of the RPM package when you install it and provides a progress bar. H stands for hash.
- `qa`: allows you to query for every package installed on the system.
  - You can limit the search by giving it a value like `rpm -qa php*`
- `ql`: Lets you display the lists of files associated with a package.
- `qg`: Lets you lists all installed packages in a specific group. For example, System Environment/Shells.
- `qil`: Lets you lists the spec file header for the given package. This is one of the things that make rpm useful for automation.
- `force`: Lets you quit the installation. DO NOT EVER DO THIS. This is a last resort command and should only be used by functionally impaired administrators.

You can use these options for the basic package management as they help to install, remove, and update packages on your system.
Let's learn about these in detail one by one.

## Installing Software

Red Hat Package Manager, also known as RPM, is a tool in Linux for software package management that is used to maintain software database and their files. In this section, you learn about:

- Red Hat Package Manager
- Installing Software through Command Line Interface

### Red Hat Package Manager

Following are the two main characteristics of RPM:

- RPM file: Comprised all the files essential to run a specific program, and the important scripts to carry out the installation on its own.
- RPM tool: Carries out common management of all the RPM packages, which are installed on a particular host.

### Installing Software through Command Line Interface

The following points should be kept in mind while installing software through command line interface:

- RPM packages are installed using the –i option to the rpm command.
  - For example, if the package, nano-3.3-18.src.rpm has to be installed then the following command can be given.
- Conventionally –i option is also used with –v option that makes rpm to be more verbose.
- The `-h` option makes rpm to display progress meters, which is as follows:
  - `# rpm -ivh evolution-2.0.4-6.src.rpm`

## Querying Software

Querying is the process to make enquiry on the software packages and check whether the RPMs are installed. This process in undertaken after the software is installed. So, we can say that querying performs two functions, which are as follows:

- Enquiring of the software packages
- Verifying the installed software packages

Let’s learn about these in detail one by one.

### Enquiring of the Software Packages

The enquiry of the installed software packages can be done using the following command:

```
[root@localhost ~]# rpm -q
```

If the details about the software packages, such as the name, version and release number of the installed software package has to be displayed, then the following command can be used:

```
[root@localhost ~]# rpm -q < package name>
```

### Verifying the Installed Software Package

Verification is done to check whether the software packages are installed successfully or not. The command used to verify a software package is as follows:

```
[root@localhost ~]# rpm -V
```

The command used to verify a software package having a specific file is as follows:

```
[root@localhost ~]# rpm -vf /usr/home/user1
```

The command used to verify all installed software packages is as follows:

```
[root@localhost ~]# rpm - va
```

## Removing Software

Software can be removed or uninstalled using RPM. The software, which is not in use currently, has to be removed so that the space occupied by it is saved for other programs. Software can be uninstalled using RPM on a command line and graphical interfaces.

### Uninstalling Software using RPM

Software applications can be uninstalled using the -e option to the rpm command, which is as follows:

```
[root@localhost ~]# rpm -e <package_name>
[root@localhost ~]# 
```

Only the name of the software package is used when the software has to be uninstalled.

### Advanced RPM Commands

The following functions are more useful, but dig a little deeper into rpm and other applications:

1. -V: Verifies packages on your system, and will inform you if a file has been altered, if the md5sum changes, if files are missing etc.
2. -K: Checks that the rpm was signed and verified either by gpg, gpg, or md5. This requires that you import the keys supplied by your rpm vendor.
3. --sign: Signs an RPM that you make, if you're so inclined.
4. --rollback: Allows you to roll back package upgrades for a specific time period. rpm --rollback 1 week ago is a good example of this.
5. --repackage: Recreates an rpm from files installed on your system. This is not a complete package, and must be rebuilt with rpmbuild --rebuild.

You can search the database to find the statistics about the RPMs on your system.

```
rpm -qa --qf "%(PLATFORM)\n. This example will show you how many rpms you have installed on your system, and for which architectures. You can do similar searches for NAME, VERSION, SIZE, and SOURCERPM.
```

## Installing Software using YUM

YUM is front-end to rpm: It performs the following functions:

- Designed to resolve package dependencies
- Used to locate packages across multiple repositories

## Using YUM

You can install, remove, and update software packages by using YUM.

The commands used to install, remove, and update software package are as follows:

```
[root @ netmon opt]# yum install nano
[root @ netmon opt]# yum remove nano
[root @ netmon opt]# yum update nano
```

## Searching packages /files

You can search packages and files by using YUM:
