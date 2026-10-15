
If other dependent packages must be installed first, RPM cancels the installation and lists those packages. You can install those packages and then repeat the installation of the application. To determine if a package is already installed, use the -qi option with rpm. The -q stands for query. To obtain a list of all the files the package has installed, as well as the directories it installed to, use the -ql option. To query package files, add the p option. The -qpi option displays information about a package, and -qpl lists the files in it. The following example lists all the files in the freeciv package:

```
$ rpm -qpl freeciv-1.14.0-2.i386.rpm
```

To remove a software package from your system, first use rpm -qi to make sure it is actually installed, and then use the -e option to uninstall it. As with the -qi option, you needn’t use the full name of the installed file. You only need the name of the application. In the next example, the user removes the freeciv game from the system:

```
$ rpm -e freeciv
```

## Package Security Check

If you download an RPM package, you may want to check its integrity and authentication, making sure the package was not tampered with and that it was obtained from a valid source. To just check a package’s integrity you can use the rpm command with the -K and the --nogpg options. A value called the MD5 digest measures the contents of a package. If the value is incorrect, the package has been tampered with. See Chapter 16 for more details on integrity checks and MD5 digests. Some packages, like Webmin, provide just digest values, allowing only integrity checks. In the next example, the user checks whether the freeciv package has been tampered with. The --nogpg option says not to perform authentication, doing the integrity check only.

```
$ rpm -K --nogpg freeciv-1.14.0-2.i386.rpm
```

To authenticate a package, you check its digital signature. Packages are signed with encrypted digital keys that can be decrypted using the public key provided by the author of the package. This public key has to first be downloaded and installed on the encryption tool used on your system. Red Hat, along with most Linux systems, uses the GNU Privacy Guard (GPG) encryption tool. GPG and authentication methods along with public keys are discussed in detail in Chapter 16. To use a public key to authenticate an RPM package, you first have to download the public key and install it in the RPM key database. For all Red Hat RPM packages that are part of the Red Hat distribution, you can use the Red Hat public key, placed during installation in the /usr/share/rhn/RPM-GPG-KEY file. You need to manually import the key to the RPM database before you can check Red Hat RPM packages, as shown here.

```
rpm --import /usr/share/rhn/RPM-GPG-KEY
```

```
$ rpm -K freeciv-1.14.0-2.i386.rpm
```

To see a list of all the keys that have been imported, you can use the -qa option and match on the gpg-pubkey* pattern. Using rpm with the -qi option and the public key, you can display detailed information about the key. The following example shows the Red Hat public key:

```
$ rpm -qa gpg-pubkey*
gpg-pubkey-db42a60e-37ea5348
```

## Installing Source Code Applications

Many programs are available for Linux in source code format. These programs are stored in a compressed archive that you need to decompress and then extract. The resulting source code can then be configured, compiled, and installed on your system. The process has been simplified to the extent that it involves not much more than installing an RPM package. The following example shows the common method to extract, compile, and install software, in this case the KonCD program, a CD writer and ripper. Always check the included README and INSTALL files that come with the source code to check the appropriate method for creating and installing that software.

> Tip Be sure that you have installed all development packages onto your system. Development packages contain the key components such as the compiler, GNOME and KDE headers and libraries, and preprocessors. You cannot compile source code software without them.

First you locate the software—in this case, from apps.kde.com—and then you download it to your system. KonCD is downloaded in a file named koncd-1.0rc2.tar.gz. Then decompress and extract the file using the tar command with the xvzf options, as shown here:

```
tar xvfz koncd-1.0rc2.tar.gz
```

This will create a directory with the name of the software, in this case koncd-1.0rc2. Change to this directory with the cd command:

```
cd koncd-1.0rc2
```

Issue the command ./configure. This generates a compiler configuration for your particular system.

```
./configure
```

Compile the software with the make command:

```
make
```

Then install the program with the make install command:

```
make install
```

Most KDE and GNOME software will also place an entry for the program in the appropriate menus—for example, a KonCD entry will be placed in the KDE Applications menu. You can
