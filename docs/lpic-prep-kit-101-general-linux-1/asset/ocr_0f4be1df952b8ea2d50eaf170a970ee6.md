The expression most commonly used with `find` is `-name`, which specifies the filename it is to find. This filename can contain wildcards, as listed in Table 6.10, or parentheses. However, they must be enclosed in quotes to prevent the shell from interpreting them. So, if you would like to find a file named `mydogma` but do not know where you saved it or exactly what you named it, but you are sure the name contains the letters `dog`, you could search for it by typing

```
```bash
find /home/hadden -name '*dog*' -print
```
```

The `-print` expression causes `find` to print all files that meet the criteria. It is the default action and therefore can be omitted. If, however, you had typed

```
```bash
find -print /home/hadden -name '*dog*'
```
```

`find` would have printed all the files contained in the directory `/home/hadden` and all its subdirectories whether or not they met the criteria. `find` sees the `-print` expression and assumes that there is no criteria. If you use the `-print` expression, make sure it is the last one on your command line.

`find` also can be used to find a file based on when it was accessed last.

```
```bash
find /home/hadden -atime zn [-print]
```
```

where `n` is the number of days relative to today. When you use this, `find` changes the access time of every directory it searches. In addition, you can use `find` to locate a file based on when it was last modified.

```
```bash
find /home/hadden -mtime zn [-print]
```
```

When using multiple criteria, a space is considered to mean `and`. The `-a` can be used instead of a space. Use either `-or` or `!` to mean `or`. Use the `!` in front of an expression to designate not. The following examples search the `pwd`.

```
```bash
find . -name '*dog*' -a '*cat*'
```
```

The previous code finds all files that contain both “`dog`” *and* “`cat`” in their names.

```
```bash
find . -name '*dog*' -o '*cat*'
```
```

The preceding code finds all files that contain either “`dog`” *or* “`cat`” in their names.

```
```bash
find . -name !'*dog*'
```
```

The previous code finds all files that do *not* contain “`dog`” in their names.