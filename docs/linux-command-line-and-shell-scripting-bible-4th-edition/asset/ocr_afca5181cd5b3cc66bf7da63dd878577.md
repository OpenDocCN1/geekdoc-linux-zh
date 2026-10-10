# **Creating a local temporary file**

By default, `mktemp` creates a file in the local directory. To create a temporary file in a local directory with the `mktemp` command, you just need to specify a filename template. The template consists of any text filename, plus six X's appended to the end of the filename:

```
```
$ mktemp testing.XXXXXX
$ ls -al testing*
-rw-------    1 rich    rich        0 Jun 20 21:30
    testing.UfIi13
$ 
```
```

The `mktemp` command replaces the six X's with a six-character code to ensure that the filename is unique in the directory. You can create multiple temporary files and be assured that each one is unique:

```
```
$ mktemp testing.XXXXXX
testing.1DRLuV
$ mktemp testing.XXXXXX
testing.lvBtkW
$ mktemp testing.XXXXXX
testing.PgqNKG
$ ls -l testing*
-rw-------    1 rich    rich        0 Jun 20 21:57
testing.1DRLuV
-rw-------    1 rich    rich        0 Jun 20 21:57
testing.PgqNKG
-rw-------    1 rich    rich        0 Jun 20 21:30
testing.UfIi13
-rw-------    1 rich    rich        0 Jun 20 21:57
testing.lvBtkW
$ 
```
```

As you can see, the output of the `mktemp` command is the name of the file that it creates. When you use the `mktemp` command in a script, you'll want to save that filename in a variable so that you can refer to it later on in the script:

```
```
$ cat test19
#!/bin/bash
# creating and using a temp file


    tempfile=$(mktemp test19.XXXXXX)


    exec 3>$tempfile
```
```