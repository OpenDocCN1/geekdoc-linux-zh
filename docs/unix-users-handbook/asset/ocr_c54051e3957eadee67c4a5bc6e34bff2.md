![](bbox=[0.1, 0.17, 0.85, 0.38])

You are progressing from root (/**), to **home**, to **denise**, and finally to the directory **.netscape-cache**. The change directory (cd) command you issue looks like the following:

```
$ cd /home/denise/.netscape-cache
```

This is an absolute path because it starts at root and progresses through the hierarchy. No matter what directory you are currently working in, even if it is **.netscape-cache**, you could use the absolute path name. In many cases, however, you may not need to issue an absolute path name. You may be so close to the file or directory you wish to access that the absolute path would be a waste of time for you. If, for instance, you are already in /home/denise, then you could change to .netscape-cache using a relative path name easily:

```
$ cd .netscape-cache
```