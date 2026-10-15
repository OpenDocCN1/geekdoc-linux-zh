will run unzip on every file in the current working directory whose name starts with hwk2_ and ends in ".gz" (in bash and sh and other Bourne-shell-like shells). You must be very careful when using file globs, especially with dangerous commands such as rm that are not reversible, because they may represent files that you did not think they did. One disastrous example would be

```
$ rm -r .*
```

which a naive user might think removes the "hidden" files in the given directory and their descendants. But the pattern .* matches .., which implies that the command will recursively remove everything in .., the parent directory. There are many other things to know about file globs; the complete description can be found in the man page in Volume 7:

```
$ man 7 glob
```

will display it.