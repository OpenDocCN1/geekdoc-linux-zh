# **476**  **Chapter 12**  **COMPRESSION, BACKUP, AND SOFTWARE INSTALLATION**

```
rdesktop-$(VERSION)/doc/keymap-names.txt \\
rdesktop-$(VERSION)/doc/ipv6.txt \\
rdesktop-$(VERSION)/doc/rdesktop.l) \\
rm -rf /tmp/rdesktop-make-dist-dir
```

.SUFFIXES:

.SUFFIXES: .c .o

.c.o:

```
$($(CC)) $(CFLAGS) -o $@ <c
```

```
[root@server1 rdesktop-1.3.1]$ _
```

This Makefile contains most of the information and commands necessary to compile the program. Some program source code that you downloaded might contain commented lines that should be uncommented to enable certain features of the program or to allow the program to compile on your computer architecture. Instructions for these commented areas are documented in the Makefile itself; thus, it is good form to read the Makefile after you run the configure script. You can also edit the Makefile if you want to change the location to which the program is installed. For rdesktop, simply change the line `prefix=/usr/local` shown in the preceding output to reflect the new directory.

Next, you must compile the program according to the settings stored in the Makefile by typing the make command while in the source code directory. This uses the gcc program to compile the source code files, as shown in the following output:

```
[root@server1 rdesktop-1.3.1]$ **make**
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -02 -1/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RDPNSD -o rdesktop.o -c rdesktop.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -02 -1/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RDPNSD -o xwin.o -c xwin.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -02 -1/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RDPNSD -o xkeymap.o -c xkeymap.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -02 -1/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RDPNSD -o xkeymap.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -02 -1/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RDPNSD -o ewmhinit.o -c ewmhinit.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -02 -1/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RDPNSD -o xclip.o -c xclip.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -02 -1/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RDPNSD -o clipboard.o -c clipboard.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -02 -1/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RDPNSD -o rdpstd.o -c rdpstd.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -02 -1/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RDPNSD -o rdpstd.osc.o -c rdpstd.osc.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -02 -1/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RDPNSD -o tcp.o -c tcp.c
```