
CentOS is derived from the distributions which are produced commercially.

- **Common set of tools:** The various distributions of Linux use different types of tools for performing various common tasks such as configuration of system or management of packages. Distributions like Ubuntu and Debian use APT for managing the .deb packages, OpenSUSE uses .rpm packages, and CentOS along with Fedora also use .rpm packages but manage all of them by using a tool known as yum. In most of the cases, the distribution you choose will end up being the one that comes with all the tools which you require and you are comfortable with.

The distributions are designed for performing in different situations. You are required to start with experimenting the distributions for finding out the one that fits you the best according to your need.

## Linux security

When you start using a system based on Linux OS, you become the owner of your system security. The internet is filled up with people who are waiting to use the computing power of your system for satisfying their own goals. Linux offers the users with various security options that help the users in securing their system and tuning the same according to their need.

## Finding your folders and files

Everything on a Linux system is in the form of a directory. In Linux, a folder is termed as a directory. Linux OS uses a well-balanced tree of various nested directories for keeping all the files in an organized manner. The directory of the highest level is known as the root directory. It comes designated with only one single slash. In Windows OS, you will come across various drives and disks. But this is not the case in Linux OS. There are several other sub-directories which lie under the root directory. Most of the systems based on Linux come with directories which are called as var and lib along with many others under the tree of the root directory. The directory of lib consists of the system libraries whereas the directory of var consists of all sorts of files which are available in the system which are most likely to change like the mail messages and logs. The directories of Linux OS can also go inside the other directories.

## Users and permissions

Linux OS uses a very powerful system for the users and its permissions for making sure that only the right people get access to the system files. As the owner of your Linux system, you can set the users and permissions for every directory. The file access system in Linux comprises of three categories.

- **Users:** A user account is assigned generally to a person or also to an application which requires access to the files in the system. You can provide user access to the system as many numbers you want.
- **Groups:** A group is the collection of one or more than one user. Groups are a great way of granting the same kind of access to various users at one time without the need for setting permissions for each individually. When you create an account of user, it gets assigned to a default group which comes with the same name as that of the name of the user. A user can be a part of as many groups as the user wants. Users who belong to a group get all the permissions which are granted for that specific group.
- **Everyone:** This category is for everyone other than the groups and users. When someone accesses the system files without even logging in the system as one specific user, they fall into the category of everyone.

The next important thing that comes right after users is permissions. Each and every directory and file in a Linux system comes with three probable levels of access.

- **Read:** All the files that come with the permission of read can be viewed.
- **Write:** All the files that come with the permission of write can be edited.
- **Execute:** All the files that come with the permission of execute can be executed or run just like an application. When you start a new script or program, you start executing it.

## Software installation in Linux

Like all the other things in the Linux system, software installation is also done by typing and then executing one specific form of text command. Most of the distributions in Linux come along with managers of package which makes it easier for installing or uninstalling any software in the system. Distributions such as Ubuntu and Debian use APT or the Advanced Packaging Tool package manager whereas CentOS and Fedora use YUM or Yellowdog Updater Modified manager of packages.

## Chapter 6: Basic Linux Commands

Linux is one of the most famous operating systems that can be found today. However, Linux is not one complete OS, it is the kernel of an OS. Linux is also regarded as a clone of UNIX. Some of the most common distributions of Linux are Linux Mint, Ubuntu Linux, Red Hat Enterprise Linux, Fedora and Debian. Linux is primarily used in the servers. It can also be regarded that almost 90% of the internet is being powered by the servers of Linux. This is mainly because Linux is secure, fast and free as a kernel. Windows servers can also be used for the internet but the main problem that comes basically with Windows is its costing. This problem of costing can be easily solved by the servers of Linux. In fact, the operating system Android which runs in a majority of the smartphones today has also been made from the Linux kernel.

### Linux shell

Linux shell is a form of program which receives the commands from the users of a system and transfers it to the operating system for the purpose of processing and then shows the result as well. The Linux shell is the main part of Linux OS. Its distributions come in graphical user interface or GUI but Linux basically comes with command line interface or CLI. For opening up the terminal of Linux shell, you need to press Ctrl+Alt+T in the Ubuntu distribution or you can also press Alt+F2, type in the gnome terminal and then hit enter.

### Linux Commands

Let’s start with some of the most basic commands of Linux.

#### pwd

When you open up the terminal first, you will be in the home directory of the user. For knowing exactly in which directory you are in, you can use the command pwd. It helps in giving out the exact path, the path which starts exactly from the root. The root is nothing but the base of the file system in Linux. It is generally denoted by using a forward slash (/). The directory of user generally looks like /home/username.

#### ls

By using the command ls, you can easily know what are the files within the directory in which you are in. You can also see each and every file which is hidden by using command ls -a.

#### cd

You can use the command cd for going to a directory. For example, if you are in the folder of home and you wish to go into the folder of downloads, you need to type cd Downloads and you will be in the downloads directory. You need to note that this command is very case sensitive. You are also required to type in the folder name exactly in the way it is in. However, this type of command comes with certain problems. For example, you are having a folder named as Raspberry Pi. In such case, when you enter the command as cd Raspberry Pi, the Linux shell will assume the second argument that comes with the command as a completely different entity and so what you will get in return is only an error message that will say that there is no such directory.

In such cases, you can use the backward slash which means use the command as cd Raspberry\Pi. The spaces are taken as : in Linux. If you type the command cd only and hit enter, you will get into the home directory again. In case you want to go back from a specific folder to a folder just before that, you need to use “cd..”. The two dots in the command represent the request of going back.

#### mkdir & rmdir

The mkdir command is being used for the purpose of creating a new folder or directory. For example, when you need to create a new directory such as DIY you need to enter command like mkdir DIY. Always remember that in case you want a directory named as DIY Hacking, you need to type it in as mkdir DIY\Hacking. You can use rmdir command for deleting the directory which you no longer need. However, always keep in mind that rmdir can only be used at the time of deleting a directory which is empty in nature. If you want to delete one directory which contains files, you need to use rm command.

#### rm

You can use the command rm for the purpose of deleting the directories and files. If you want to delete the directory only, you need to use rm -r command. When you use the rm command, it will delete the folder along with all the files in it.

#### touch

This command is used for creating new files. It can be anything, starting from a txt file which is empty to an empty form of a zip file. You can use the command like touch new.txt.

#### man & --help

If you want to know in details about a command and how you can use it, you can use the command man. It helps by showing all forms of manual pages of all the commands. For example, if you enter man cd, it will show all the manual pages of the command cd. When you type in the name of the command along with the argument --help, it will show in which way you can use the command.
