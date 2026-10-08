
137644 -rw------- 1 root sys 161 Jul 11 12:16 softinit
137706 -rw-r--r-- 1 denise users 39 Sep 29 12:48 srvpr.exe
137682 -rw-r--r-- 1 denise users 38 Aug 15 12:14 steve.h
137685 -rw-r--r-- 1 denise users 14675 Aug 30 15:08 target.exe
137711 -rw-r--r-- 1 denise users 229630 Sep 29 12:54 tcp41a.exe
137700 -rw-r--r-- 1 denise users 1954453 Sep 29 12:26 tndsz.exe
137703 -rw-r--r-- 1 denise users 364270 Sep 23 09:50 upgrade.exe
137663 -rw-r--r-x 1 denise users 88 Aug 9 13:43 whoon
137678 -rw-r--r-- 1 denise users 191495 Aug 30 15:00 win95app.exe

The inode number contains: the location of files and directories on the disk; access permissions; owner and group IDs; file link count; time of last modification; time of last access; device identification number for special files; and a variety of other information. inode numbers are used extensively by the system as you change directories and perform various work.

![](img/75f39fc91296b889c0653851accdfd46_135_0.png)

## ls -p

Because you may have subdirectories within the directory you are listing, you may want to use the -p option to ls, which puts a "/" in after directory names, as shown in the following example:

```
$ ls -ap /home/denise
```

```
.xauthority
.cshrc
.cdt/
.dtprofile
.elm/
.exrc
.fmrc.orig
.glancerc
.gnupg
.history
.login
.lrm/
.mailrc
.netscape-bookmarks.html
.netscape-cache/
.netscape-cookies
.netscape-history
.netscape-newsgroups-news.spry.com
.netscape-newsgroups-newsserv.hp.com
.netscape-preferences
.newsrc-news.spry.com
.newsrc-newsserv.hp.com
.profile
.rhosts
.sh_history
.softbuildrc
.softinit.orig
.sw/
.xinitrc
.xsession
27247b.exe
410pt1.exe
410pt2.exe
41ndir.exe
41ndsl.exe
41ndsl4.exe
41nwd.exe
41rtr2.exe
HPDAl.EXE
Mail/
N32I2B6.EXE
SGS14S.EXE
clean
clean2
clean3
content.exe
dsanh.exe
eql
eq2
en03l6bz.exe
en03l6t6.exe
explore.exe
flexl_cd.exe
fred.h
hal.c
hpdll017.exe
hpdlinst.txt
hpux_patches
j25/7a.exe
j895up.exe
msie10.exe
n32el2n.exe
nfs197.exe
pass_sb
plusedemo.exe
ps4x03.exe
psq
quik_res.exe
rclock.exe
rkhelpe.exe
roni.mak
sb.txt
smsup2.exe
softinit.remotesoftcm
srvpr.exe
steve.h
target.exe
tcp41a.exe
tnds2.exe
upgrade.exe
whoam
win95app.exe
```

## ls -R

Because the subdirectories you are listing probably have files and subdirectories beneath them, you may want to recursively list these. The -R option to ls shown in the following example performs this recursive listing. This listing is truncated because it would be too long if it included all the subdirectories under /home/denise:

![](img/75f39fc91296b889c0653851accdfd46_136_0.png)

```
$ ls -aR /home/denise

.Xauthority
.cshrc
.dt
.dprofile
.exrc
.fmrc.orig
.glancerc
.pmphp
.history
.login
.lrom
.mailrc
.netscape-bookmarks.html
.netscape-cache
.netscape-cookies
.netscape-history
.netscape-newsgroups-news.spry.com
.netscape-newsgroups-newsserv.hp.com
.netscape-preferences
.newsrc-news.spry.com
.newsrc-newsserv.hp.com
.profile
.rhosts
.sh_history
.softwarebuildrc
.softinit.orig
.sw
.xinitrc
.xsession
27247b.exe
410pt1.exe
410pt2.exe
41ndir.exe
41ndsl.exe
41ndsd.exe
41nwa.exe
41ltr2.exe
HPDA1.EXE
Mail
N3212B6.EXE
SCSIAS.EXE
clean
clean2
clean3
content.exe
dsensh.exe
egl
e92
en0316bz.exe
en0316tb.exe
explore.exe
flexi_cd.exe
fred.h

.
.
.
(skip some of the listing)

/home/denise/.lrom:
LRAAAa27637.CC
LRBAAa27637.CC
LROM_AB
LROM_AB.OLD
LROM_AB.1kl
LROM.SET

/home/denise/.netscape-cache:
```

**(skip some of the listing)**

```
cache306C05510015292.gif
cache306C05560025292.gif
cache306C05560035292.gif

/home/denise/.sw:
sessions
```

**(skip remainder of the listing)**

## ls Summary

I have shown you what I believe to be the most important, and most often used, ls options. Because you may have future needs to list files and directories based on other criteria, I provide you with a list of most ls options. There is no substitute, however, for issuing the man ls command. Whatever I provide is only a summary. Viewing the man pages for ls gives you much more information. The following is a summary of the more commonly used ls options:

![](img/75f39fc91296b889c0653851accdfd46_138_0.png)

**ls - List the contents of a directory**

- **-a** List all entries.
- **-b** Print nongraphic characters.
- **-c** Use the time the file was last modified for producing order in which files are listed.
- **-d** List only the directory name, not its contents.
- **-f** Assume that each argument is a directory.
- **-g** Only the group is printed and not the owner.
- **-i** Print the inode number in the first column of the report.
- **-m** List the contents across the screen separated by commas.
- **-n** Numbers for UID and GID are printed instead of names.
- **-o** List the information in long form (-l), except that group is omitted.
- **-p** Put a slash (/) at the end of directory names.
- **-q** Nonprinting characters are represented by a "?".
- **-r** Reverse the order in which files are printed.
- **-s** Show the size in blocks instead of bytes.
- **-t** List in order of time saved, with most recent first.
- **-u** Use the time of last access instead of last modification for determining order in which files are printed.
- **-x** List files in multicolumn format as shown in examples.
- **-A** Same as -a, except that current and parent directories aren't listed.
- **-C** Multicolumn output produced.
- **-F** Directory followed by a "/", executable by an "*", symbolic link by an "@", and FIFO by a "|".
- **-L** List file or directory to which link points.
- **-R** Recursively list subdirectories.
- **-l** Output will be listed in single-column format.

Also, some shorthand command names are available for issuing ls with options. For instance, ll is equivalent to ls -l, and lsr is equivalent to ls -R in some UNIX variants. We will also cover creating an "alias," whereby you can define your own shorthand for any command in an upcoming chapter.

You can selectively list and perform other file-related commands with wild cards. The following section covers file name expansion and wild cards.

## File Name Expansion and Wild Cards

Before we cover additional file system related commands, it is worth taking a look at file name expansion. An overview of file name expansion is useful to ensure that you're comfortable with this topic before we cover additional commands.

Table 3-2 lists some common file name expansion and pattern matching.

### Table 3-2 File Name Expansion and Pattern Matching

| Character(s) | Example | Description |
|---|---|---|
| `*` | 1) `ls *.c` | Match zero or more characters |
| `?` | 2) `ls conf.?` | Match any single character |
| `[list]` | 3) `ls conf.[co]` | Match any character in list |
| `[lower-upper]` | 4) `ls libdd.9873[5-6].sl` | Match any character in range |
| `str{str1,str2,str3,...}` | 5) `ls ux*.{700,300}` | Expand str with contents of `{}` |
| `~` | 6) `ls -a ~` | Home directory |
| `~username` | 7) `ls -a ~gene` | Home directory of username |

The following descriptions of the examples shown in Table 3-2 are more detailed.

- 1) To list all files in a directory that end in ".c", you could do the following:

```bash
$ ls *.c
    conf. SAM.c conf.c
```

- 2) To find all the files in a directory named "conf" with an extension of one character, you could do the following:

```bash
$ ls conf.?
    conf.c conf.o conf.1
```

- 3) To list all the files in a directory named "conf" with only the extension "c" or "o", you could do the following:

```bash
$ ls conf.{co}
    conf.c conf.o
```

![](img/75f39fc91296b889c0653851accdfd46_140_0.png)

4) To list files with similar names but a field that covers a range, you could do the following:

```
$   ls libdd9873[5-6].sl
    libdd98735.sl libdd98736.sl
```

5) To list files that start with "ux" and have the extension "300" or "700," you could do the following:

```
$   ls ux*.{700,300}
    uxbootlf.700 uxinstrfs.300
```

6) To list the files in your home directory, you could use ~:

```
$   ls -a ~
    .   .cshrc.org .login  .shrc.org
    .. .exrc      .login.org .cshrc
        .history .profile
```

7) To list the files in the home directory of a user, you could do the following:

```
$   ls -a ~gene
    . .history splinedat under.des
    .. .login trail.txt xtra.part
    .cshrc .login.org ESP-File
    .cshrc.org .profile Mail
    .exrc .shrc.org opt
```

## pwd and cd

When we covered absolute and relative path names, we used the **cd** command to change directory. You can be at any point in the file sys-
