The easiest way to install wine is to download a pre-built .rpm file, then install the program with the following code:

```
# rpm ivh wine*rpm
```

> Note
The commercial version of SuSE 6.2 Linux includes Wine, which may be installed using the YaST command. The resulting binary wine command will be found under the /usr/bin directory.

To build Wine from scratch, download the 3.1MB archive, then decompress the archive like this:

```
# tar xvzf Wine*gz
```

Change directory into the resulting wine directory, and use the configure command, like this:

```
# cd wine*
# ./configure
```

Finally, use the make command to build Wine like this:

```
# make depend && make
```

After the Wine build finishes, use the make command to install Wine (as root), like this:

```
# make install
```

This will copy the wine file into the /usr/local/bin directory. By default, debugging symbols are compiled into the binary, resulting in a 13MB file. You can reduce wine's size by using the strip command like this:

```
# strip /usr/local/bin/wine
```

This leaves wine as a much smaller file by nearly 10MB. As a final step, copy the file wine.ini from the Wine directory to the /usr/local/etc directory with the name wine.conf, like this (you must be root to do this):

```
# cp wine.ini /usr/local/etc/wine.conf
```

Open this file with your favorite text editor, and change the line designating the path to Drive C, which looks something like this:

```
[Drive C]
Path=/c
```