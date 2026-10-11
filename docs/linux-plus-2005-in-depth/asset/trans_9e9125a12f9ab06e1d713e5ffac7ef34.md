

## **476**  **第 12 章**  **压缩、备份和软件安装**

```
VERSION                 = 1.3.1

KEYMAP_PATH           = $(datadir)/keymaps/
RDPOBJ                = tcp.o iso.o mcs.o secure.o licence.o rdp.o orders.o bitmap.o cache.o rdp5.o
            channels.o rdpdr.o serial.o printer.o
X11OBJ                = rdesktop.o xwin.o xkeymap.o ewmhints.o xclip.o cliprdr.o
VNCOBJ                = vnc/rdp2vnc.o vnc/vnc.o vnc/xkeymap.o vnc/x11stubs.o
CRYPTOBJ              = crypto/rc4_enc.o crypto/rc4_skey.o crypto/md5_dgst.o crypto/sha1dgst.o
            crypto/bn_exp.o crypto/bn_mul.o crypto/bn_div.o
            crypto/bn_sqr.o crypto/bn_add.o crypto/bn_shift.o crypto/bn_asm.o
            crypto/bn_ctx.o crypto/bn_lib.o
```

```
include Makeconf  # configure-generated

all: $(TARGETS)

rdesktop: $(X11OBJ) $(SOUNDOBJ) $(RDPOBJ) $(CRYPTOBJ)
    $(CC) $(CFLAGS) -o rdesktop $(X11OBJ) $(SOUNDOBJ) $(RDPOBJ)
    $(CRYPTOBJ) $(LDFLAGS) -lX11

rdp2vnc: $(VNCOBJ) $(SOUNDOBJ) $(RDPOBJ) $(CRYPTOBJ)
    $(CC) $(CFLAGS) -o rdp2vnc $(VNCOBJ) $(SOUNDOBJ) $(RDPOBJ) $(CRYPTOBJ)
    $(LDFLAGS) $(LDVNC)

vnc/rdp2vnc.o: rdesktop.c
    $(CC) $(CFLAGS) $(VNCINC) -DRDP2VNC -o vnc/rdp2vnc.o -c rdesktop.c

vnc/vnc.o: vnc/vnc.c
    $(CC) $(CFLAGS) $(VNCINC) -DRDP2VNC -o vnc/vnc.o -c vnc/vnc.c

vnc/xkeymap.o: xkeymap.c
    $(CC) $(CFLAGS) $(VNCINC) -DRDP2VNC -o vnc/xkeymap.o -c xkeymap.c

vnc/x11stubs.o: vnc/x11stubs.c
    $(CC) $(CFLAGS) $(VNCINC) -o vnc/x11stubs.o -c vnc/x11stubs.c

Makeconf:
    ./configure

install: installbin installkeymaps installman

installbin: rdesktop
    mkdir -p $(DESTDIR)/$(bindir)
    $(INSTALL) rdesktop $(DESTDIR)/$(bindir)
    strip $(DESTDIR)/$(bindir)/rdesktop
    chmod 755 $(DESTDIR)/$(bindir)/rdesktop

installman: doc/rdesktop.1
    mkdir -p "${DESTDIR}/${mandir}/man"
    cp doc/rdesktop.1 "${DESTDIR}/${mandir}/man1"
    chmod 644 "${DESTDIR}/${mandir}/man1/rdesktop.1"

installkeymaps:
    mkdir -p "${DESTDIR}/${KEYMAP_PATH}"
# Prevent copying the CVS directory
    cp keymaps/?\ keymaps/l?\-?\ ? "${DESTDIR}/${KEYMAP_PATH}"
    cp keymaps/common "${DESTDIR}/${KEYMAP_PATH}"
    cp keymaps/modifiers "${DESTDIR}/${KEYMAP_PATH}"
    chmod 644 "${DESTDIR}/${KEYMAP_PATH}"/*

proto:
    cproto -DMAKE_PROTO -DWITH_OPENSSL -o proto.h *.c

clean:
    rm -f *.o crypto/*.o *~ vnc/*.o vnc/*~ rdesktop rdp2vnc

dist:
    mkdir -p /tmp/rdesktop-make-dist-dir
    ln -sf /pwd /rdesktop-make-dist-dir/rdesktop-${VERSION}
    cd /tmp/rdesktop-make-dist-dir;
    tar zcfv /tmp/rdesktop-${VERSION}.tar.gz \
        rdesktop-${VERSION}/COPYING \
        rdesktop-${VERSION}/README \
        rdesktop-${VERSION}/configure \
        rdesktop-${VERSION}/Makefile \
        rdesktop-${VERSION}/rdesktop.spec \
        rdesktop-${VERSION}/*.c \
        rdesktop-${VERSION}/*.h \
        rdesktop-${VERSION}/crypto/README \
        rdesktop-${VERSION}/crypto/*.c \
        rdesktop-${VERSION}/crypto/*.h \
        rdesktop-${VERSION}/keymaps/?\ \
        rdesktop-${VERSION}/keymaps/l?\-?\ ? \
        rdesktop-${VERSION}/keymaps/common \
        rdesktop-${VERSION}/keymaps/modifiers \
        rdesktop-${VERSION}/keymaps/convert-map \
        rdesktop-${VERSION}/doc/HACKING \
        rdesktop-${VERSION}/doc/AUTHORS \
        rdesktop-${VERSION}/doc/TODO \
        rdesktop-${VERSION}/doc/ChangeLog \
        rdesktop-${VERSION}/doc/keymapping.txt \
        rdesktop-${VERSION}/doc/keymap-names.txt \\
        rdesktop-${VERSION}/doc/ipv6.txt \\
        rdesktop-${VERSION}/doc/rdesktop.l) \\
rm -rf /tmp/rdesktop-make-dist-dir

.SUFFIXES:

.SUFFIXES: .c .o

.c.o:

    $(CC) $(CFLAGS) -o $@ -c $<
```

```
[root@server1 rdesktop-1.3.1]$ _
```

该 Makefile 包含了编译程序所需的大部分信息和命令。您下载的一些程序源代码可能包含被注释掉的行，为了启用程序的某些功能或允许程序在您的计算机架构上编译，可能需要取消这些行的注释。关于这些注释区域的说明记录在 Makefile 本身中；因此，在运行 configure 脚本后阅读 Makefile 是一种良好的做法。如果您想更改程序安装的位置，也可以编辑 Makefile。对于 rdesktop，只需将前面输出中显示的 `prefix=/usr/local` 行更改为反映新目录即可。

接下来，您必须在源代码目录中输入 make 命令，根据存储在 Makefile 中的设置编译程序。这将使用 gcc 程序来编译源文件，如下面的输出所示：

```
[root@server1 rdesktop-1.3.1]$ make
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o rdesktop.o -c rdesktop.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o xwin.o -c xwin.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o xkeymap.o -c xkeymap.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o xkeymap.o -c xkeymap.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o ewmhinit.o -c ewmhinit.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o xclip.o -c xclip.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o clipboard.o -c clipboard.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o rdpstd.o -c rdpstd.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o rdpstd.osc.o -c rdpstd.osc.c
gcc -DKEYMAP_PATH="/usr/local/share/rdesktop/keymaps/\*" -Wall -O2 -I/usr/X11R6/include -
DWITH_OPENSSL -DWITH_RPSND -o tcp.o -c tcp.c

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

编译完成后，可以通过输入以下命令将这些二进制程序复制到文件系统中的正确位置：

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

