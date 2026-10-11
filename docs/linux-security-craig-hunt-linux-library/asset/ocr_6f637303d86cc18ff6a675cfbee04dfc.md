Listing 2.1 shows how you should look for the existence of the /etc/shadow file. If it does not exist, simply create it with the pwconv command. Note the change in the /etc/passwd file after the conversion:

# Listing 2.1 Creating a shadow password file

```
[root]# ls -1 /etc/shadow
ls: /etc/shadow: No such file or directory
[root]# more /etc/passwd
root:PV/6t9I GetTjU:0:0:root:/root:/bin/bash
bin::1:1:bin:/bin:
daemon:x:2:2:daemon:/sbin:
adm::3:4:adm:/var/adm:
lp::4:7:lp:/var/spool/lpd:
sync::5:0:sync:/sbin:/bin/sync
shutdown::6:0:shutdown:/sbin:/sbin/shutdown
halt::7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:
operator::11:0:operator:/root:
ftp::14:50:FTP User:/home/ftp:
nobody:x:99:99:Nobody:/:
ramon:aa1g0.pAVxZuA:501:100:Ramon J.ontanon:/home/ramon:/bin/bash
[root]# pwconv
[root]# ls -1 /etc/shadow
- - - - - - - - - - - 1 root root 563 Sep 23 15:27 /etc/shadow
[root]# more /etc/passwd
root:x:0:0:root:/root/bin/bash
bin::1:1:bin:/bin:
daemon:x:2:2:daemon:/sbin:
adm::3:4:adm:/var/adm:
lp::4:7:lp:/var/spool/lpd:
sync::5:0:sync:/sbin:/bin/sync
shutdown::6:0:shutdown:/sbin:/sbin/shutdown
halt::7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:
operator::11:0:operator:/root:
ftp:x:14:50:FTP User:/home/ftp:
nobody:x:99:99:Nobody:/:
ramon::501:100:Ramon J.ontanone:/home/ramon:/bin/bash
[root]# more /etc/shadow
root:PV/6t9I GetTjU:11223:0:99999:7:::
bin::11223:0:99999:7:::
```