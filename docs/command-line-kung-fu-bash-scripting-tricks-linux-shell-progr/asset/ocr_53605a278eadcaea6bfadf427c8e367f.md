```
`2014-04-09
$ sudo cp httpd.conf httpd.conf."d"
$ sudo cp httpd.conf httpd.conf.$(d)
$ sudo cp httpd.conf !#.$(d)
$ sudo cp httpd.conf{,.${d}}
$ ls -l httpd.conf*
httpd.conf
httpd.conf.2014-04-08`
```

# ## Overwrite the Contents of a File

```
`$ command > file`
```

You can redirect output from one command to a file using the greater-than symbol. A single greater-than symbol (> ) redirects standard output to a file, overwriting (truncating) any existing contents of the file. If no file exists, it creates one.

```
`$ grep bash /etc/passwd > users-that-use-bash
$ cat users-that-use-bash
root:x:0:0:root:/root:/bin/bash
jason:x:501:501:Jason:/home/jason:/bin/bash
oracle:x:1006:1006::/home/oracle:/bin/bash
bob:x:1000:1000:Bob Smith:/home/bob:/bin/bash
$`
```

# ## Empty a File That Is Being Written To

```
`$ > file
$ cat /dev/null > file`
```