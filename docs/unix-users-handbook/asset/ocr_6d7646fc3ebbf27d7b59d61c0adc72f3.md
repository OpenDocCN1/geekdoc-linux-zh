Using the **passwd.test** file, lets view this full file, and then view lines 16, 17, and 18 only using *p*.

```
# cat passwd.test
root:PGyQCKVH6ShY0:0:0:root:/root:/bin/bash
bin:4:1:bin:/bin:
daemon:4:2:2:daemon:/sbin:
adm:4:3:4:adm:/var/adm:
lp:4:4:7:lp:/var/spool/lpd:
sync:5:0:sync:/sbin:/bin/sync
shutdown:4:6:11:shutdown:/sbin:/sbin/shutdown
halt:4:7:0:halt:/sbin:/sbin/halt
mail:4:8:12:mail:/var/spool/mail:
news:4:9:13:news:/var/spool/news:
uucp:4:10:14:uucp:/var/spool/uucp:
operator:4:11:0:operator:/root:
games:4:12:100:games:/usr/games:
gopher:4:13:30:gopher:/usr/lib/gopher-data:
ftp:4:14:50:FTP User:/home/ftp:
man:4:15:15:Manualls Owner:/:/
nobody:4:65534:65534:Nobody:/:/bin/false
col:WhOyzfAV2qm2Y:100:100:Caldera OpenLinux User:/home/col/bin/bash
#
# sed 16,18p passwd.test
root:PGyQCKVH6ShY0:0:0:root:/root:/bin/bash
bin:4:1:1:bin:/bin:
daemon:4:2:2:daemon:/sbin:
adm:4:3:4:adm:/var/adm:
lp:4:4:7:lp:/var/spool/lpd:
sync:5:0:sync:/sbin:/bin/sync
shutdown:4:6:11:shutdown:/sbin:/sbin/shutdown
halt:4:7:0:halt:/sbin:/sbin/halt
mail:4:8:12:mail:/var/spool/mail:
news:4:9:13:news:/var/spool/news:
uucp:4:10:14:uucp:/var/spool/uucp:
operator:4:11:0:operator:/root:
games:4:12:100:games:/usr/games:
gopher:4:13:30:gopher:/usr/lib/gopher-data:
ftp:4:14:50:FTP User:/home/ftp:
man:4:15:15:Manualls Owner:/:/
nobody:4:65534:65534:Nobody:/:/bin/false
nobody:4:65534:65534:Nobody:/:/bin/false
col:WhOyzfAV2qm2Y:100:100:Caldera OpenLinux User:/home/col/bin/bash
col:WhOyzfAV2qm2Y:100:100:Caldera OpenLinux User:/home/col/bin/bash
#
# sed -n 16,18p passwd.test
man:4:15:15:Manualls Owner:/:/
nobody:4:65534:65534:Nobody:/:/bin/false
col:WhOyzfAV2qm2Y:100:100:Caldera OpenLinux User:/home/col/bin/bash
```

![](bbox=[0.89, 0.11, 0.97, 0.2])

![](bbox=[0.89, 0.35, 0.97, 0.44])

The first attempt to print only lines 16, 17, and 18 results in all of the lines in the file being printed and lines 16, 17, and 18 being printed twice. The reason is that sed reads each line of input and acts on each line. In order to specify the lines on which to act, we used the -n switch to suppress all lines from going to standard output. We then