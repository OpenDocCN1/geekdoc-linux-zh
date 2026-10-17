
### 编译命令

```bash
gcc -DKEYMAP_PATH="/usr/local/share/keymaps/" -Wall -O2 -I/usr/X11R6/include -DWITH_OPENSSL -DWITH_RDPSND -o channels.o -cc channels.c

gcc -DKEYMAP_PATH="/usr/local/share/keymaps/" -Wall -O2 -I/usr/X11R6/include -DWITH_OPENSSL -DWITH_RDPSND -o rdpdr.o -cc rdpdr.c

gcc -DKEYMAP_PATH="/usr/local/share/keymaps/" -Wall -O2 -I/usr/X11R6/include -DWITH_OPENSSL -DWITH_RDPSND -o serial.o -cc serial.c

gcc -DKEYMAP_PATH="/usr/local/share/keymaps/" -Wall -O2 -I/usr/X11R6/include -DWITH_OPENSSL -DWITH_RDPSND -o printer.o -cc printer.c

gcc -DKEYMAP_PATH="/usr/local/share/keymaps/" -Wall -O2 -I/usr/X11R6/include -DWITH_OPENSSL -DWITH_RDPSND -o rdesktop.o xw.in xkeymaps.o ewmhints.o xclip.clprdr.o rdp5nd.o rdp5nd_osc.tcp iso.o mcs.secure.licence.o rdp5.o bitmap.o rdpdr.o printer.o -L/usr/X11R6/lib -lcrypto -lX11
```

`[root@server1 rdesktop-1.3.1]#`

编译完成后，可以通过输入以下命令将这些二进制程序复制到文件系统中的正确位置：

```bash
[root@server1 rdesktop-1.3.1]# make install

mkdir -p /usr/local/bin

install rdesktop /usr/local/bin
```

## 软件安装 551

```bash
strip /usr/local/bin/rdesktop

chmod 755 /usr/local/bin/rdesktop/keymaps/

mkdir -p /usr/local/share/rdesktop/keymaps/

cp keymaps/* /usr/local/share/rdesktop/keymaps/

cp keymaps common /usr/local/share/rdesktop/keymaps/

cp keymaps modifiers /usr/local/share/rdesktop/keymaps/

chmod 644 /usr/local/share/rdesktop/keymaps/*

mkdir -p /usr/local/man/man1

cp doc.rdesktop.1 /usr/local/man/man1

chmod 644 /usr/local/man/man1/rdesktop.1
```

在编译并复制到相应的目录（`README` 文件包含了程序的所在位置）之后，你可以删除源代码和压缩包，并找到程序的主二进制文件，如下例所示：

```bash
[root@server1] # cd .

[root@server1] # rm -rf rdesktop-1.3.1

[root@server1] # rm -f rdesktop-1.3.1.tar.gz

[root@server1] # which rdesktop

/usr/local/bin/rdesktop
```

随后，你可以查看该程序的帮助页，如图 12 所示，通过 `rdesktop` 命令来查看。

## 使用 RPM

Red Hat 包管理器通过互联网分发软件包。要安装软件包，可以使用 `-i` 参数：

```bash
[root@server1]# rpm -ivh rdesktop-1.3.1-i386.rpm
```

## 软件安装

```
package bluefish is not installed

[root@server1 root]# _
```
