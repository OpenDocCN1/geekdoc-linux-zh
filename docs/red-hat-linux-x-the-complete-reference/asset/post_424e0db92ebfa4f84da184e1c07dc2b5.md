
# Software Repositories

You can download Linux software from many online sources. You can find sites for particular kinds of applications, such as GNOME and KDE, as well as for particular distributions, such as Red Hat. The Red Hat Network can automatically download and update software installed from RPM packages that make up the Red Hat distribution. Some sites are repositories for RPM packages, such as [rpmfind.net](http://rpmfind.net), and others like [freshmeat.net](http://freshmeat.net) refer you to original sites. A great many of the Open Source Linux projects can be found at [sourceforge.net](http://sourceforge.net). Here you will find detailed documentation and recent versions of software packages. For applications designed for the GNOME desktop, you can check [www.gnome.org](http://www.gnome.org), and you can find KDE applications at [apps.kde.com](http://apps.kde.com). For particular database and office applications, you can download software packages directly from the company's Web site, such as [www.oracle.com](http://www.oracle.com) for the Oracle database. Table 29-1 lists several popular Linux software sites.

## Table 29-1: Linux Software Sites

| FTP and Web Sites | Applications |
|---|---|
| ftp.redhat.com | Software packaged in RPM packages for Red Hat |
| freshmeat.net | Linux software, including RPMs |
| rpmfind.net | RPM package repository |
| freshrpms.net | Customized RPM packages |
| sourceforge.net | Linux Open Source software projects |
| www.gnome.org | GNOME software |
| apps.kde.com | KDE software |
| rpmseek.com | Linux software search site |
| www.filewatcher.org | Linux FTP site watcher |
| www.gnu.org | GNU archive |
| www.ximian.com | Ximian Desktop, office applications for GNOME |

# Software Package Types

The software packages on RPM sites like Red Hat and rpmfind.net will have the file extension .rpm. RPM packages that contain source code have an extension .src.rpm. Other packages, such as those in the form of source code that you need to compile, come in a variety of compressed archives. These commonly have the extensions .tar.gz, .tgz, or .tar.bz2. They are explained in detail later in the chapter. Table 29-2 lists several common file extensions that you will find for the great variety of Linux software packages available to you.

## Table 29-2: Linux Software Package File Extensions

| Extension | File |
|---|---|
| .rpm | Software package created with the Red Hat Software Package Manager, used on Red Hat, Caldera, Mandrake, and SuSE distributions. |
| .src.rpm | Software packages that are source code versions of applications, created with the Red Hat Software Package Manager. |
| .gz | gzip compressed file (use gunzip to decompress). |
| .bz2 | bzip2 compressed file (use bunzip2 to decompress, also use the j option with tar, as in xvjf). |
| .tar | A tar archive file, use tar with xvf to extract. |
| .tar.gz | gzip compressed tar archive file. Use gunzip to decompress and tar to extract. Use the z option with tar, as in xvzf to both decompress and extract in one step. |
| .tar.bz2 | bzip2 compressed tar archive file. Extract with tar -xvzj. |
| .Z | tar archive file compressed with the compress command. |
| .Z | File compressed with the compress command (use the decompress command to decompress). |
| .deb | Debian Linux package. |

# Red Hat Package Manager (RPM)

Several Linux distributions, including Red Hat, Mandrake, Caldera, and SuSE, use RPM to organize Linux software into packages you can automatically install, update, or remove. RPM is a command line-driven package management system that is capable of installing, uninstalling, querying, verifying, and updating software packages installed on Linux systems. An RPM software package operates as its own installation program for a software application. A Linux software application often consists of several files that need to be installed in different directories. The program itself is most likely placed in a directory called /usr/bin, online manual files like Man pages go in other directories, and library files in yet another directory. In addition, the installation may require modification of certain configuration files on your system. The RPM software package performs all these tasks for you. Also, if you later decide you don't want a specific application, you can uninstall packages to remove all the files and configuration information from your system. RPM works similarly to the Windows Install Wizard, automatically installing software, including configuration, documentation, image, sample, and program files, along with any other files an application may use. All are installed in their appropriate directories on your system. RPM maintains a database of installed software, keeping track of all the files installed. This enables you to use RPM also to uninstall software, automatically removing all files that are part of the application.

# RPM Tools

To install and uninstall RPM packages, you can use the rpm command directly from a shell prompt, or the Red Hat distribution software management tool, redhat-config-packages. The redhat-config-packages tool is a GUI front end for the rpm command. Although you should download RPM packages for your particular distribution, numerous RPM software packages are designed to run on any Linux system. You can learn more about RPM at its Web site at www.rpm.org. The site contains up-to-date versions for RPM, documentation, and RPM support programs, such as rpm2html and rpm2cpio. rpm2html takes a directory containing RPM packages and generates Web pages listing those packages as links that can be used to download them. rpm2cpio is a Perl script to extract RPMs. Also, the Red Hat Linux Customization Guide provides an excellent tutorial for both RPM and redhat-config-packages.

# RPM Packages

The naming conventions for RPM packages vary from one distribution to another. On Red Hat, the package name includes the package version along with its platform (i386 for Intel PCs) and the .rpm extension. An example of the Emacs editor's RPM package for Intel systems is shown here:

```
emacs-21.2-18.i386.rpm
```

The RPM packages on your DVD-ROM or distribution CD-ROM represent only a small portion of the software packages available for Linux. An extensive repository for RPM packages is also located at rpmfind.net. Packages here are indexed according to distribution, group, and name. The site includes packages for every distribution, including Red Hat.

- **Tip:** RPM packages with the term noarch are used for architecture-independent packages. This means that they are designed to install on any Linux system. Packages without noarch may be distribution- or architecture-dependent, designed to install on a particular type of machine.

You could place these packages in a directory on your system, and then use either rpm or a GUI RPM utility such as the redhat-config-packages tool to install it. Normally, you should always try to use the version of the RPM package set up for your Red Hat distribution; for instance, if you run Red Hat 9.0, it is best to download the software package designated for Red Hat 9.0 instead of downloading the same package for Red Hat 7.3. Packages for specific releases will be kept in the release directories. In many cases, attempting to install an RPM package meant for a different distribution may fail.

# Installing from the Desktop: redhat-config-packages

The redhat-config-packages tool provides an effective and easy-to-use interface for managing the Red Hat RPM packages provided by your Red Hat distribution, whether you installed from CD-ROMs, DVD-ROM, hard disk, or network. It runs on any window manager, including GNOME and KDE. You can access redhat-config-packages using the Packages icon in the System Settings window. This opens a Package Management window that initially displays a listing of package categories from which you can install packages. See Chapter 4 for more details.

- **Tip:** You can also install a particular RPM package directly. First display it with the file manager, and then double-click it. It invokes the redhat-config-packages tool, which installs the package. It also checks for dependent packages and installs those also. If you are using CD-ROMs instead of the DVD-ROM, you will be prompted to insert any other CD-ROMs as needed.

# Updating Software

You can update your Linux system automatically using a distribution update agent like the Red Hat Network. You can also manually download packages using an FTP client, Web browser, or the GNOME or KDE file managers, and then use the rpm command or the redhat-config-packages tool to install the software.

For redhat-config-packages, you can use your file manager to locate the RPM file and double-click the RPM package file. You can also, on GNOME, right-click it, and select Open With | Install Packages, or on KDE, select Install Package. redhat-config-packages starts up and checks for any dependent packages you may need. It then installs the RPM package for you.

If you are using the rpm command, you use the -U option to upgrade packages. In the following example, the rpm command with the -Uvh option installs an upgrade for Emacs:

```
# rpm -Uvh emacs-21.2-18.i386.rpm
```

# Command Line Installation: rpm

If you do not have access to the desktop, or you prefer to work from the command line interface, you can use the rpm command to manage and install software packages. rpm is the command that actually performs installation, removal, and queries of software packages. In fact, redhat-config-packages uses the rpm command to install and remove packages. An RPM package is an archive of software files that include information about how to install those files. The filenames for RPM packages end with .rpm, indicating software packages that can be installed by the Red Hat Package Manager.

# The rpm Command

With the rpm command, you can maintain packages, query them, build your own, and verify the ones you have. Maintaining packages involves installing new ones, upgrading to new versions, and uninstalling packages. The rpm command uses a set of options to determine what action to take. In addition, certain tasks, such as installing or querying packages, have their own options that further qualify the kind of action they take. For example, the -q option queries a package, but when combined with the -l option, it lists all the files in that package. Table 29-3 lists the set of rpm options. The syntax for the rpm command is as follows (rpm-package-name is the name of the software package you want to install):

```
rpm options rpm-package-name
```

## Table 29-3: Red Hat Package Manager (RPM) Options

| Mode of Operation | Effect |
|---|---|
| rpm -i options package-file | Installs a package; the complete name of the package file is required. |
| rpm -e options package-name | Uninstalls (erases) a package; you only need the name of the package, often one word. |
