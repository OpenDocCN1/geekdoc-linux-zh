First you locate the software-in this case, from apps.kde.com and then you download it to your system.

KonCD is downloaded in a file named koncd-1.0rc2.tar.gz. Then decompress and extract the file using the tar command with the xvzf options, as shown here:

```
tar xvfz koncd-1.0rc2.tar.gz
```

This will create a directory with the name of the software, in this case kreatcd-1.0rc2. Change to this directory with the cd command:

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

Most KDE and GNOME software will also place an entry for the program in the appropriate menus-for example, a KonCD entry will be placed in the KDE Applications menu. You can then run KonCD from the menu entry. You could also open a terminal window and enter the program's name.