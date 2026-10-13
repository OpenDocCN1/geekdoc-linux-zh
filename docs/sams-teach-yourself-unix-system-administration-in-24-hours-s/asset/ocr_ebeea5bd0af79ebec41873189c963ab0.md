```
Using binary mode to transfer files.
ftp> cd /pub/freeware/intel/8/
250 CWD command successful.
ftp> dir sud*
200 PORT command successful.
150 Opening ASCII mode data connection for /bin/ls.
-rw-r--r-- 1 steve staff 93934 Nov 23 1999 sudo-1.5.9p4
  -> sudo-intel-local.gz
226 Transfer complete.
ftp> lcd /tmp
Local directory now /tmp
ftp> get sudo-1.5.9p4-sol8-intel-local.gz
200 PORT command successful.
150 Opening BINARY mode data connection for 'sudo-1.5.9p4
  -> sol8-intel-local.gz' (93934 bytes).
226 Transfer complete.
local: sudo-1.5.9p4-sol8-intel-local.gz remote: sudo-1.5.9p4
  -> sol8-intel-local.gz
93934 bytes received in 1.2 seconds (76.79 Kbytes/s)
ftp> quit
221 Goodbye.
```

Now the package is copied from the Net to /tmp, so it's time to install it on the Solaris system.

3. Installation of packages is done with pkgadd, but you need to take a simple intermediate step first: unzip the file. Fortunately, that's easy, as you learned last hour, with the command gunzip sudo*gz.

```
# gunzip sudo*gz
# pkgadd -d sudo-1.5.9p4-sol8-intel-local
```

```
The following packages are available:
1 SMCsudo        sudo
                   (i86pc) 1.5.9p4

Select package(s) you wish to process (or 'all' to process
all packages). (default: all) [?,??,q]: all

Processing package instance <SMCSudo> from </tmp/sudo-1.5.9p4-sol8-intel-local>

sudo .. (i86pc) 1.5.9p4 -- Todd Miller

The selected base directory </usr/local> must exist before
installation is attempted.

Do you want this directory created now [y,n,?,q] y
Using </usr/local> as the package base directory.
## Processing package information.
## Processing system information.
```