
The `apt-get` utility works by obtaining information on available packages from the sources listed in `/etc/apt/sources.list` and then using that information to upgrade or install packages. One particularly common use of this utility is to keep your system up-to-date with any new packages. The following two commands will accomplish this goal, if `/etc/apt/sources.list` includes pointers to up-to-date file archive FTP sites:

```
# `apt-get` update
# `apt-get` `dist-upgrade`
```

In addition to system updates, you can perform package installations (`apt-get` `install` `package name`) and more—consult the `man` page for `apt-get` for details. APT still relies on `dpkg` to do its “dirty work,” though, and sometimes using `dpkg` is necessary. For instance, if you want to install a package that you’ve obtained from a source other than a Debian repository, you must use `dpkg` or some other derivative tool.

One potential problem with APT is that it downloads packages to your hard disk and then installs them but it doesn’t automatically delete packages. To ensure that your hard disk doesn’t fill up with package files you no longer need, type `apt-get` `clean` from time to time. This command removes the package files on a one-time basis.

## Criteria for Completion

To complete this task, you should have performed four types of package maintenance tasks with `dpkg`: removing packages, upgrading packages, installing packages, and querying packages. You should also have used APT to check for package updates from an APT repository and optionally to update some or all of your system’s packages.

## Task 3.3: Install Programs from Source

Although most Linux distributions provide handy binary package systems, such as RPM and Debian packages, truly “street-smart” Linux administrators are just as comfortable compiling and installing programs from source code as they are installing binary packages. The reasons for this are varied. All open-source programs are, by definition, available in source code form, so the ability to handle source code frees you from any omissions that might be made by your distribution maintainer. Compiling and installing source code guarantees that you’re using *pristine code*—that is, code as delivered by the developers rather than modified (and perhaps made buggier) by distribution maintainers. Installing from source code also enables you to tweak the code yourself, either by making changes to the code or by just altering compile-time options to better suit your system’s needs. On the downside, compiling programs from source code is time-consuming, distribution maintainers often make improvements to better integrate packages with their systems, and bypassing the package system means that you lose features such as dependency tracking and easy software deletion.

Gentoo Linux is unusual in that it employs a source-based package system, known as Portage. When you install a package in Gentoo, the package system downloads the source code, applies patches, and compiles the code automatically. This gives you some, but not all, of the advantages of installing from source code on other platforms along with the advantages of easy deletes and upgrades of binary package systems. The RPM and Debian package systems also both offer source packages, which can be useful—you can compile the source package to overcome weird dependency problems, use software on a platform that’s not supported by its developers, and so on.

## Scenario

Your distribution lacks **ftpd** (http://www.time-travellers.org/oftpd/), which is an anonymous-only File Transfer Protocol (FTP) server program. You want to install this program for use on an Internet server that’s intended to deliver files to the public at large, so you plan to install it by compiling the source code from the server’s Web page.

## Scope of Task

Compiling software from source code requires obtaining the package, unpacking the package, configuring the compile scripts, compiling the software, and installing the software. Unfortunately, each of these tasks can be performed in various different ways, depending upon the package in question. Therefore, I can only present an overview that’s likely to apply to most packages. Ultimately, you should read the documentation that comes with any software to learn about its own unique quirks and requirements.

## Duration

This task should take about half an hour or an hour to complete. Compiling software from source code can take anywhere from a minute or two to many hours, depending on the complexity of the software and whether you run into any problems, such as missing development libraries.

## Setup

You need a working Linux computer and **root** access to that computer to complete this task. You can complete most of the task as an ordinary user, but you must be **root** to install the software.

## Caveats

The tasks you perform before acquiring **root** privileges are fairly safe. Once you take on the superuser identity to install the software, the usual caveats apply. In addition, installing software runs the risk of overwriting other software files—perhaps even files from other packages, if an unfortunate naming conflict exists.

## Procedure

Installing software from source requires several steps: obtaining and unpacking the software, preparing to compile the software, compiling the software, installing the software, and testing the software.

### Obtaining and Unpacking the Software

The easiest way to obtain software is usually to check the program’s main Web site. In the case of **oftpd**, download links appear on the main page. The latest version as I write is **0.3.7**.

Most packages ship as tarballs that are compressed with **gzip** (with a `.gz` or `.tgz` filename extension) or **bzip2** (with a `.bz2` or `.tbz` filename extension). To unpack the software, you should change into a directory in which you want to extract the source code and use **tar**:

```
`$ tar xvzf ~/oftpd-0.3.7.tar.gz`
```

For **bzip2**-compressed packages, change **xvzf** to **xvfj**. You should also, of course, provide a correct path to the location of the tarball. If all goes well, the source code will be uncompressed, with **tar** displaying the files’ names as they’re extracted from the archive. Most, but not all, packages place their files in a subdirectory named after the package, such as **oftpd-0.3.7** for the **oftpd** package. Change into that subdirectory.

### Preparing the Software for Compilation

Before compiling the software, most non-trivial programs give you the chance to configure them for your system, and many require such configuration. Precisely how you do this varies from one package to another, and this is the step that really requires you to read the package’s documentation. Look for a file called **README**, **INSTALL**, **FAQ**, or something similar and read it. (Many packages provide several such documentation files.)

Although not universal, many packages provide a script called **configure**. To configure the software for your system, run that script:

```
`$ ./configure`
```

A few packages provide a configure script that’s run in another way, via the **make** utility:

```
`$ make config`
```

The **README**, **INSTALL**, or other documentation file should describe how to configure the package if it’s done differently than one of these methods. In addition, you can sometimes pass options to the configuration script. These compile-time *options* can permanently enable or disable certain program features, change program defaults, or otherwise customize the software for your system. For instance, some programs enable you to tweak compiler options for a particular CPU, add or remove support for particular GUI libraries (particularly for X-based programs), change the installation directories, and so on. The **oftpd** package is simple enough that it doesn’t support many such options. (You can change the installation directory by passing the `--prefix=dir` option, but you’re unlikely to need to do even that much.)
