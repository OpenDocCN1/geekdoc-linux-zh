
```
root@lnxone:~/Stunnel/stunnel.22
文件 编辑 设置 帮助
[root@lnxone:~/Stunnel]# # ./
[root@lnxone:~/Stunnel]# # ./
[root@lnxone:~/Stunnel]# #configure
checking build system... i586-pc-linux-gnu
checking for gcc... gcc
checking for C output... aout
checking whether the compiler works... yes
checking whether we are cross compiling... no
checking for executable suffix... a
checking for object suffix... o
checking whether we are using the GNU compiler... yes
checking whether gcc accepts -g... yes
checking for BSD compatible install... /usr/install -c
checking for SSL directory... /usr
checking whether enable SSL defaults... no
checking to disable RSA support... no
checking to enable DM support... no
checking for dipopen in -ldl... yes
checking for gethostname in -lnsl... yes
checking for socket in -lp
checking for pthread_
```

图 4-30 `./configure` 命令为 Stunnel 创建一个 make 脚本。

52 Linux 与 OpenVMS 互操作性

```
root@lnxone:~/Stunnel/stunnel.22
文件 编辑 设置 帮助
checking for pthread_sigmask... yes
checking for ANSI C header files... yes
checking for sys/types.h... yes
checking for sys/stat.h... yes
checking for stdlib.h... yes
checking for memory.h... yes
checking for string.h... yes
checking for intptes.h... yes
checking for strint.h... yes
checking for unistd.h (cached)
checking for unsigned char... yes
checking size of unsigned char... 1
checking for unsigned short... yes
checking size of unsigned short... 2
checking for unsigned int... yes
checking size of unsigned int... 4
checking for unsigned long... yes
checking size of unsigned long... 6
checking size of unsigned long... 8
configure: creating /config.status
config: creating Makefile
```

图 4-31 等待 `make` 命令完成且 `/configure` 完成。

```
root@lnxone:~/Stunnel/stunnel.22
文件 编辑 设置 帮助
checking for unsigned long... yes
checking size of unsigned long... 8
configure: creating /config.status
```

``` Makefile
root@lnxone:~/Stunnel/stunnel.22
文件 编辑 设置 帮助
[root@lnxone:~/Stunnel/stunnel.22]# # ./
[root@lnxone:~/Stunnel/stunnel.22]# # make
[root@lnxone:~/Stunnel/stunnel.22]# # make
```

图 4-32 执行 `make` 来构建 Stunnel 程序（你必须在 Linux 系统中安装了 c）。

第 4 章 – OpenVPN 和 Linux 的安全工具 53

```
root@lnox:~/stunnel/stunnel-3.22
文件 编辑 设置 帮助
你即将被要求输入一些信息，这些信息将整合到你的证书请求中。
你即将输入的内容被称为属性名称（Distinguished Name，简称 DN）。
有很多字段，但你可以留一些字段为空。
某些字段将有一个默认值，
如果你输入 "..."，该字段将留空。
国家，名称（字母代码） [PL]
州或省份（全称） [State-State]:Texas
地名名称（英文，城市） []
组织名称（英文，公司） [Developers Ltd]:Defcon-VMS
组织单元名称（可选） [dfslug]
通用名称（服务器的完全域名 FQDN） [localhost]
test - eq 1 - f "/dev/urandom" && /dev/urandom 512 >> stunnel.pem
test - eq 1 - f "/dev/urandom" && /dev/urandom 512 >> stunnel.pem
/usr/bin/openssl x509 -dates -fingerprint -notout
-in stunnel.pem
subject=C=US/ST=Texas/L=Defcon-VMS/OU=dfwlug/CN=localhost
Before=Aug 27 01:51:24 2022 GMT
After=Aug 27 01:51:24 2032 GMT
MD5 fingerprint=E1:F9:B1:67:A9:C5:7E:D0:32:12:60:F:54:A2:E6
[root@lnox:~/stunnel/stunnel-3.22]# _
```

图 4-3 这些问题的答案，以便能够为 Linux 系统创建一个 stunnel 文件。

```
root@lnox:~/stunnel/stunnel-3.22
文件 编辑 设置 帮助
/usr/bin/openssl ghend -rand "/dev/urandom" 512 >> stunnel.pem
test - eq 1 - f "/dev/urandom" || \
/usr/bin/openssl ghend 512 >> stunnel.pem
/usr/bin/openssl x509 -dates -fingerprint -notout
-in stunnel.pem
subject=C=US/ST=Texas/L=Defcon-VMS/OU=dfwlug/CN=localhost
Before=Aug 27 01:51:24 2022 GMT
After=Aug 27 01:51:24 2032 GMT
MD5 fingerprint=E1:F9:B1:67:A9:C5:7E:D0:32:12:60:F:54:A2:E6
[root@lnox:~/stunnel/stunnel-3.22]#
[root@lnox:~/stunnel/stunnel-3.22]#
[root@lnox:~/stunnel/stunnel-3.22]#
[root@lnox:~/stunnel/stunnel-3.22]#
[root@lnox:~/stunnel/stunnel-3.22]#
[root@lnox:~/stunnel/stunnel-3.22]# make install
/bin/make install /usr/local/bin /usr/local /usr/local/man/man8 /usr/local/
var/stunnel/
chmod anew /usr/local/var/stunnel/
/usr/bin/install -c 711 stunnel /usr/local/lib
test -z stunnel.so || /usr/bin/install -c 755 stunnel.so /usr/local/lib
test -z /usr/bin/install -c 600 stunnel.pem
[root@lnox:~/stunnel/stunnel-3.22]# _
```

图 4-4 执行 `make` 以完成 Stunnel 程序/库到生产系统中的安装。

54 Linux 与 OpenVMS 互操作性
