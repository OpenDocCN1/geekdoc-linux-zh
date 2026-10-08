a**yo.freshrpms.net**. Click on the Fedora link to list the **freshrpms-release** packages for Fedora. The package you want is something like `freshrpms-release-1.1-1.fc.noarch.rpm`

```
freshrpms-release-1.1-1.fc.noarch.rpm
```

With your Web browser you can choose to download and install at once. The install procedure will warn that there is no key for the packages, but install anyway. The key is included with the **freshrpms-release** package and will be automatically installed. Alternatively, you could download the package first, and then install it either from GNOME or using the **rpm** command. With GNOME, just right-click and select Open With “Software Installer.” With the **rpm** command, download the package first, and then just use the following:

```
rpm -ivh freshrpms-release-1.1-1.fc.noarch.rpm
```

This will install the **freshrpms.repo** configuration file in the `/etc/yum.repos.d` directory, as well as download the Freshrpms GPG key. You can then install the GPG manually or just wait until you first install a package from Freshrpms, in which case Yum will install it for you, after prompting for your approval. The following will import the Freshrpms key manually:

```
rpm --import http://freshrpms.net/RPM-GPG-KEY-freshrpms
```

# Installing Some Popular Packages

Once configured, installation is a simple matter of opening a terminal window and entering the command **yum** along with the **install** option followed by the name of the software package you want to install.

If you are installing a package from Fedora repository, you are set to go. You can use Pirut or the **yum** command. Be sure to use the Search or List views of Pirut to access all packages. For example, to install Abiword from a command line, you just enter

```
yum install abiword
```

Yum does the rest, first locating the package, then downloading it, and then performing the installation. It will also be careful to select the package for your architecture, like x86_64 for 64 bit or i686 for 32 bit. Yum will first ask for confirmation before installing, listing any dependent packages that will also have to be installed. You can also use Yum to remove and update packages. Check the **yum** Man page for options. Some detailed examples are shown here for some of the more popular packages such as MPlayer and Xine, as well as GStreamer and MP3 support.

Before installing multimedia packages, you will first need to install the Yum configuration file for a repository that carries them. You could use **freshrpms.net**, which carries a collection of multimedia packages, including GStreamer and MPlayer. If you have installed the Yum configuration file for Livna, be sure to disable the repository if you have not already done so.

# GStreamer Support: Multimedia Plug-ins

Many GNOME multimedia applications such as Totem use GStreamer to provide multimedia support. To use such features as DVD video and MP3, you have to install additional GStreamer