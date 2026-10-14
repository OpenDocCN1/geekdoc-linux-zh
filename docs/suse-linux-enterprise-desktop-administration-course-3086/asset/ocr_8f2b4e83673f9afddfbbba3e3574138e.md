For user root, the output is different:

```
```text
dalo:~ # ls -l /usr/share/doc/packages/yast2-users/
total 79
drwxr-xr-x   3 root root  248 Feb 2 15:42 .
drwxr-xr-x 492 root root 13976 Feb 2 16:02 ..
-rw-r--r--   1 root root 17992 Jan 27 00:34 COPYING
-rw-r--r--   1 root root 17992 Jan 27 00:34 COPYRIGHT.english
-rw-r--r--   1 root root    75 Jan 27 00:34 README
-rw-r--r--   1 root root   193 Sep 8 02:36 TODO.txt
drwxr-xr-x   2 root root 1352 Feb 2 15:42 autodocs
-rw-r--r--   1 root root 2013 Sep 8 02:36 crack.html
-rw-r--r--   1 root root 9583 Sep 8 02:36 users.html
dalo:~ #
```
```

The first file in the list of the normal user is autodocs. The first file in the list of user root is COPYING.

In the POSIX encoding table, all the lowercase characters are listed after all uppercase characters. In UTF-8, the lowercase “a” follows the uppercase “A” immediately.

In POSIX, the only character between “A” and “C” is “B.” But in UTF-8, “a,” “B,” and “b” come between “A” and “C.”

![](bbox=[0.105, 0.461, 0.293, 0.531])

To change the locale variables permanently, you have to edit the file /etc/sysconfig/language. The functionalities of the other variables are described in that file. Further information can be found in the man page of locale (man locale).

# Name Expansion Using Search Patterns

Occasionally, you might want to perform operations on a series of files without having to name all the files. In this case, you could make use of the search patterns shown in Table 8-1.

| Search Pattern | Description |
|---|---|
| `?` | Any single character (except `/`). |
| `*` | Any string length, including zero characters (except `/` at the beginning of a filename and `/`). |
| `[0-9]` | Any of the characters enclosed (here: numbers from 0 to 9). |
| `[a-ek-s]` | Any character from the ranges a-e and k-s. |
| `[abcdefg]` | Any of these characters. |
| `[!abc]` | None of these characters. |

Table 8-1