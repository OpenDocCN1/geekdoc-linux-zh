```
```text
% grep '^taylor[a-z]' /etc/passwd
taylorj:? :1048:1375:James Taylor:/users/taylorj:/bin/csh
taylorjr:? :203:1022:James Taylor:/users/taylorjr:/bin/csh
taylorjj:? :668:1042:Robert Taylor:/users/taylorjj:/bin/csh
taylormx:? :869:1508:Melanie Taylor:/users/taylormx:/bin/csh
```
```

4. Let’s look at some other examples. Here I use `head` to view the first five lines of the password file:

```
```text
% head -5 /etc/passwd
root:? :0:0:/:/bin/csh
news:? :6:11:USENET News:/usr/spool/news:/bin/ksh
ingres:*? :7:519:INGRES Manager:/usr/ingres:/bin/csh
usrlimit:? :8:800:(1000 user system):/mnt:/bin/false
vanilla:*? :20:805:Vanilla Account:/mnt:/bin/sh
```
```

Now I’ll specify a pattern that tells grep to search for all lines that contain zero or more occurrences of the letter z:

```
```text
% grep 'z*' /etc/passwd | head -5
root:? :0:0:/:/bin/csh
news:? :6:11:USENET News:/usr/spool/news:/bin/ksh
ingres:*? :7:519:INGRES Manager:/usr/ingres:/bin/csh
usrlimit:? :8:800:(1000 user system):/mnt:/bin/false
vanilla:*? :20:805:Vanilla Account:/mnt:/bin/sh
```
```

The result is identical to the result of the preceding command, but that shouldn’t be a surprise. Specifying a pattern that matches zero or more occurrences will match every line! Specifying only the lines that have one or more z’s is accomplished with this odd-looking pattern:

```
```text
% grep 'z*z*' /etc/passwd | head -5
marg:? :724:1233:Guyzee:/users/marg:/bin/ksh
ayy:? :1272:1224:martine:/users/ayy:/bin/csh
wizardz:? :1560:1375:Cz:/users/wizardz:/bin/ksh
zhq:? :2377:1318:Zihong:/users/zhq:/bin/csh
mmm:? :1527:133:Michael Kenzel:/users/mmm:/bin/ksh
```
```

5. Earlier I found that a couple of lines in the `/etc/passwd` file were for accounts that didn’t specify a login shell. Each line in the password file must have a certain number of colons, and the last character on the line for these accounts will be a colon, which is an easy grep pattern when you remember that as the last character in a pattern, a `$` represents the end of line. And don’t forget that `^` as the very first character in a pattern represents the beginning of the line (versus within a set notation, where it indicates a “not,” or reverse, of the pattern subsequently specified).

Here’s how the `$` notation might look in this context:

```
```text
% grep ':$' /etc/passwd
charon:? :21:807:The Ferryman:/users/tomb:
lp:*? :70:10:System V LP Administration:/var/spool/lp:
```
```