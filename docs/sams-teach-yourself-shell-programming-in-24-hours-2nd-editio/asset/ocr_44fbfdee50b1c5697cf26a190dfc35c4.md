produces the following output on my system:

```
/home:
anna  ftp  httpd  ranga  vathsa

/usr/local:
X11  bin  gimp  jokes  sbin
ace  doc  include  lib  share
atalk  etc  info  man  turbo)-1.1.0
```

A blank line separates the contents of each directory.

# Listing Files

You can mix files and directories as arguments to ls:

```
$ ls .profile docs/ /usr/local /bin/sh
```

This produces a listing of the specified files and the contents of the directories. If you don't want the contents of a directory listed, you need to specify the -d option to ls.

This forces ls to display only the name of the directory, not its contents:

```
$ ls -d /home/ranga
/home/ranga
```

The -d option can be combined with any of the other ls options. An example of this is

```
$ ls -afd /usr/local /home/ranga /bin/sh
/bin/sh
/home/ranga/
/usr/local/
```

# Common Errors

If the file or directory you specify does not exist, ls reports an error. For example,

```
$ ls tomorrows_stock_prices.txt
tomorrows_stock_prices.txt: No such file or directory
```

If you specify several arguments instead of one, ls will report errors only for those files or directories that do not exist. It correctly lists the others. For example,

```
$ ls tomorrows_stock_prices.txt /usr/local .profile

produces an error message

tomorrows_stock_prices.txt: No such file or directory
/usr/local:
X11  bin  gimp  jokes  sbin
ace  doc  include  lib  share
atalk  etc  info  man  turbo)-1.1.0

.profile
```