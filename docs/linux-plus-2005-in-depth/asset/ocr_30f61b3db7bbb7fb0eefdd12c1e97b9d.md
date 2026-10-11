```
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o iso.o -c iso.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o mcs.o -c mcs.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o secure.o -c secure.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o licence.o -c licence.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o rdp.o -c rdp.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o orders.o -c orders.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o bitmap.o -c bitmap.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o cache.o -c cache.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o rdp5.o -c rdp5.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o channels.o -c channels.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o rdpdr.o -c rdpdr.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o serial.o -c serial.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o printer.o -c printer.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o rdesktop rdesktop.o xwin.o xkeymap.o emm386.o xclip.o
cliprd.o rpsnd.o rpsnd_os5.o tcp.o iso.o mcs.o secure.o licence.o rdp.o orders.o
bitmap.o cache.o rdp5.o channels.o rdpdr.o serial.o printer.o -L/usr/X11R6/lib -lX11
```

After being compiled, these binary programs can then be copied to the correct location on the filesystem by typing the following command:

```
[root@server1 rdesktop-1.3.1]# make install
mkdir -p /usr/local/bin
install rdesktop /usr/local/bin
strip /usr/local/bin/rdesktop
chmod 755 /usr/local/bin/rdesktop
mkdir -p /usr/local/share/rdesktop/keymaps/
cp keymaps/? keymaps/?-?? /usr/local/share/rdesktop/keymaps/
cp keymaps/common /usr/local/share/rdesktop/keymaps/
cp keymaps/modifiers /usr/local/share/rdesktop/keymaps/
```