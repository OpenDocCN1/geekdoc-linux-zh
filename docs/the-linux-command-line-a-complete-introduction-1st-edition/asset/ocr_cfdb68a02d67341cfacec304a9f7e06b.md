In addition, we will introduce a couple of commands to assist us in our explorations:

+   - touch—Change file times.
+   - stat—Display file or filesystem status.

# locate—Find Files the Easy Way

The locate program performs a rapid database search of pathnames and then outputs every name that matches a given substring. Say, for example, we want to find all the programs with names that begin with zip. Since we are looking for programs, we can assume that the name of the directory containing the programs would end with bin/. Therefore, we could try to use locate this way to find our files:

```
[me@linuxbox ~]$ locate bin/zip
```

locate will search its database of pathnames and output any that contain the string bin/zip:

```
/usr/bin/zip
/usr/bin/zipcloak
/usr/bin/zipgrep
/usr/bin/zipinfo
/usr/bin/zipnote
/usr/bin/zipsplit
```

If the search requirement is not so simple, locate can be combined with other tools, such as grep, to design more interesting searches:

```
[me@linuxbox ~]$ locate zip | grep bin
```

```
/bin/bunzip2
/bin/bzip2
/bin/bzip2recover
/bin/gunzip
/bin/gzip
/usr/bin/funzip
/usr/bin/gpg-zip
/usr/bin/preunzip
/usr/bin/prezip
/usr/bin/prezip-bin
/usr/bin/unzip
/usr/bin/unzipSfx
/usr/bin/zip
/usr/bin/zipcloak
/usr/bin/zipgrep
/usr/bin/zipinfo
/usr/bin/zipnote
/usr/bin/zipsplit
```

The locate program has been around for a number of years, and several different variants are in common use. The two most common ones found in modern Linux distributions are slocate and mlocate, though they are usually