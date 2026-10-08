You can specify the field separator with the *-F* option followed by a separator, which is a colon(:) in **passwd.test**. The following example specifies the field separator and then evaluates the first field to determine whether it equals "root," and if so, prints out the entire line:

![](bbox=[0.04, 0.21, 0.14, 0.34])

```
```
# awk -F: '$1 == "root" {print}' passwd.test
root:PgYQCkVH65hyQ:0:0:root:/root:/bin/bash
```
```

The following example specifies the field separator and then evaluates the fourth field to determine whether it equals "0," which means the user is a member of the same group as root, and if so, prints out the entire line:

```
```
# awk -F: '$4 == "0" {print}' passwd.test
root:PgYQCkVH65hyQ:0:0:root:/root:/bin/bash
sync:*:5:0:sync:/sbin/bin/sync
halt:*:7:0:halt:/sbin/sbin/halt
operator:*:11:0:operator:/root:
```
```

You can perform many types of comparisons besides **==** using **awk**. The following examples show the use of several comparison operators on our trusty **passwd.test** file. The first example prints all users who are in a group with a value less than 14:

```
```
# awk -F: '$4 < 14 {print}' passwd.test
root:PgYQCkVH65hyQ:0:0:root:/root:/bin/bash
bin:*:1:1:bin:/bin:
daemon:*:2:2:daemon:/sbin:
adm:*:3:4:adm:/var/adm:
lp:*:4:7:lp:/var/spool/lpd:
sync:*:5:0:sync:/sbin/bin/sync
shutdown:*:6:11:shutdown:/sbin:/sbin/shutdown
halt:*:7:0:halt:/sbin/sbin/halt
mail:*:8:12:mail:/var/spool/mail:
news:*:9:13:news:/var/spool/news:
operator:*:11:0:operator:/root:
```
```

The next example prints all users who are in a group with a value less than or equal to 14: