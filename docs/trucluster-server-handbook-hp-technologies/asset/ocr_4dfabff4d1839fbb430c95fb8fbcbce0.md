NOTE: although we have created a CDSL that points to somewhere, that somewhere points to nowhere.

```
```sh
# wc -l myFirstCDSL
wc: myFirstCDSL : No such file or directory
```
```

This is not an error, but rather the nature of a symbolic link. You can remedy this situation by simply copying a file to /myFirstCDSL.

```
```sh
# cp .profile myFirstCDSL && wc -l myFirstCDSL
       74 myFirstCDSL
```
```

Next, let’s create a directory under root (/) to illustrate the mkcdsl command with the “-c” option. The “-c” option copies the file (or in this case, the directory) from its location to a member-specific location while leaving a CDSL in the file’s location.

```
```sh
# CcdlDir && mkdir $C && mkcdsl -c $C && fin $C
cluDir -> cluster/members/(memb)/cluDir
```
```

You can see what the mkcdsl would do (without actually doing it) using the “-n” option.

```
```sh
# mkcdsl -n anotherCDSL
mkcdsl would: ln -s cluster/members/(memb)/anotherCDSL /anotherCDSL
```
```

# 6.4.2   Maintaining CDSLs

There are two commands that can be used to maintain CDSLs on a system:

+   - `cdslinvchk(8)`
+   - `mkcdsl(8)`

# 6.4.2.1   Using the cdslinvchk (8) command

The cdslinvchk command verifies that all the CDSLs installed on the system exist by searching the subset inventory files located in /usr/.smdb/ (the *.inv files) and the /var/adm/cdsl_admin.inv file. If the command detects any errors, it writes them in the cdsl_check_list file located in /var/adm. The cdslinvchk command checks only for missing CDSLs; it does not recreate missing links. To recreate a missing CDSL, use the mkcdsl command.

```
```sh
# cdslinvchk
Successful CDSL inventory check
```
```