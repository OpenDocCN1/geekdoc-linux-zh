![](bbox=[0.05, 0.13, 0.9, 0.49])

What if the items being sorted had many more fields than our two-column disk usage example? Let's go back to the **passwd.test** file for a more complex sort. Let's `cat` **passwd.test** so that we can again see its contents:

```
# cat passwd.test
root:PgYQCkVH65hyQ:0:0:root:/root:/bin/bash
bin:::1:1:bin:/bin:
daemon:::2:2:daemon:/sbin:
adm:::3:4:adm:/var/adm:
lp::*:4:7:lp:/var/spool/lpd:
sync::*:5:0:sync:/sbin:/bin/sync
shutdown:::6:11:shutdown:/sbin:/sbin/shutdown
halt::*:7:0:halt:/sbin:/sbin/halt
mail::*:8:12:mail:/var/spool/mail:
news::*:9:13:news:/var/spool/news:
uucp::*:10:14:uucp:/var/spool/uucp:
operator::*:11:0:operator:/root:
games::*:12:100:games:/usr/games:
gopher::*:13:30:gopher:/usr/lib/gopher-data:
```