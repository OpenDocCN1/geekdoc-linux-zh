
you). The “provides” list is quite powerful because it allows several different packages to provide a given resource. For example, a MySQL database-based program requires MySQL to be installed, but isn’t fussy whether you install MySQL 4.1 or MySQL 5.0. In this situation, the Debian packages for MySQL 4.1 and MySQL 5.0 will both have “mysql-server-4.1” in the provides list, meaning that they offer the functionality provided by MySQL 4.1. As a result, you can install either version to satisfy the MySQL-based application.

## Compiling Software from Source

Compiling applications from source is not that difficult. Most source code is available as compressed source tarballs—that is, tar files that have been compressed using gzip or bzip. The compressed files typically uncompress into a directory containing several files. It is always a good idea to compile source code as a regular user to limit any damage that broken or malicious code might inflict, so create a directory named source in your home directory.

From wherever you downloaded the source tarball, uncompress it into the ~/source directory using the -C option to tar:

```
tar zxvf packagename.tgz -C ~/source
```

```
tar zxvf packagename.tar.gz -C ~/source
```

```
tar jxvf packagename.bz -C ~/source
```

```
tar jxvf packagename.tar.bz2 -C ~/source
```

If you are not certain what file compression method was used, use the file command to figure it out:

```
file packagename
```

Now, change directories to ~/source/packagename and look for a file named README, INSTALL, or a similar name. Print out the file if necessary because it contains specific instructions on how to compile and install the software. Typically, the procedure to compile source code is as follows:

```
./configure
```

This runs a script to check whether all dependencies are met and the build environment is correct. If you are missing dependencies, the configure script normally tells you exactly which ones it needs. If you have the Universe and Multiverse repositories enabled in Synaptic, chances are you will find the missing software (usually libraries) in there.

When your configure script succeeds, run

```
make
```

to compile the software. And finally, run

```
sudo make install
```

If the compile fails, check the error messages for the reason and run

```
make clean
```

before you start again. You can also run

```
sudo make uninstall
```

to remove the software if you do not like it.

## Relevant Ubuntu and Linux Commands

You will use these commands while managing your Ubuntu system resources and software packages:

- `apt-get`—The default command-line package-management tool (see Chapter 33 for more on APT)
- `gnome-app-install`—The Ubuntu GUI Package Manager
- `synaptic`—Advanced tool for software manipulation and repository editing
- `update-manager`—The primary source of Ubuntu package updates

## Reference

http://www.debian.org/doc/manuals/project-history/ch-detailed.en.html—History of the Debian Linux package system.

http://www.nongnu.org/synaptic/—Home of the Synaptic package manager.

http://www.ubuntu.com/usn—The official list of Ubuntu security notices.

## CHAPTER 8

## On the Internet: Surfing the Web, Writing Email, and Reading the News

## IN THIS CHAPTER

- Choosing a Web Browser
- Choosing an Email Client
- An Overview of Network News
- Selecting a Newsreader
- Internet Relay Chat
- Internet Messaging with GAIM
- Videoconferencing with Ekiga
- Reference

The Internet has revolutionized our modern civilization within a short time. Not long ago, it was unheard of to be communicating through the Internet, and computer networks were viewed with some suspicion thanks to various Hollywood blockbusters such as WarGames and The Terminator; nowadays you are deemed backward if you do not have an email account or an instant messenger "nick." This chapter introduces you to some of the more popular software that you can use to access the Internet, send and receive email, read network news, collaborate with others using an online collaboration tool, and talk in real time using instant messaging and even videoconferencing. You will find out how to set up each piece of software to access the resources you need.

## Choosing a Web Browser

The Internet has forever changed how we access and share information. The ways in which we view the Internet have also changed and are continually improving to give better and richer experiences. In this section, we look at some of the popular open-source web browsers available for Ubuntu.

## A Brief Introduction to the Internet

The Internet itself was first brought to life by the U.S. Department of Defense in 1969. It was called ARPAnet after the Department of Defense's Advanced Research Projects Agency. Designed to build a network that would withstand major catastrophe (this
