![](bbox=[0.14, 0.07, 0.85, 0.61])

```
$ cat tempfile<Enter>
admin
Desktop
mbox
 tempfile
 tempwork
$ rm tempfile<Enter>
```

# Filter Commands

Here, we will show you how the various elements of a pipe execute in parallel.

A command is referred to as a *filter* if it can read its input from standard input, alter it in some way, and write the output to standard output. A filter can thus be used as an intermediate command between pipes. When