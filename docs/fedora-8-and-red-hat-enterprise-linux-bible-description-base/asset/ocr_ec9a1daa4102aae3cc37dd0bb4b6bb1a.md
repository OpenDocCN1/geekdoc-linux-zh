the same hardware and configuration information. That makes this a great file for you to start creating your ks.cfg file from.

> NOTE: For further details about how to use kickstart, refer to the Red Hat Linux Configuration Guide. You can get this guide from any Red Hat mirror site. To use a more graphical tool for configuring kickstart, run the system-config-kickstart command.

To start, log in as the root user. Then make a copy of the anaconda-ks.cfg file to work on.

```
# cp anaconda-ks.cfg ks.cfg
```

Use any text editor to edit the ks.cfg file. Remember that required items should be in order and that any time you omit an item, the user will be prompted for an answer. Entries from a ks.cfg file that was created from a regular DVD installation of Fedora are used as a model for the descriptions below. You should start with your own anaconda-ks.cfg file, and as a result, your file will start out somewhat differently. Commented lines begin with a pound sign (#).

The first line in the ks.cfg file should indicate whether the installation is an upgrade or an install. The install option runs a new installation. You can use the upgrade keyword instead to upgrade an existing system. (For an upgrade, the only requirements are a language, an install method, an install device, a keyboard, and a boot loader.)

```
install
```

The method of installation is indicated on the next line. Possible locations for the installation media include: NFS (nfs --server=servername --dir=installdir), FTP (url --url ftp://user:passwd@server:dir/), HTTP (url --url http://server/dir/), or hard drive (harddrive --dir=/dir --partition=/dev/partition). For the default DVD or CD install, you will see:

```
cdrom
```

The required lang command sets the language (and to be more specific, the country as well) in which Fedora is installed. The value is U.S. English (en_US.UTF-8) by default:

```
lang en_US.UTF-8
```

You can install multiple languages to be supported in Fedora. Here is an example of the default being set to U.S. English:

```
langs support --default en_US.UTF-8 en_US.UTF-8
```

The required keyboard command identifies a United States (us) keyboard by default. More than 70 other keyboard types are supported. (Run system-config-keyboard to see a list of available keyboard types.)

```
keyboard us
```