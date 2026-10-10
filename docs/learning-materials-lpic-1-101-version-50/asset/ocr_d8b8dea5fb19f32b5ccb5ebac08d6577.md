```
$ which -a mkfs.ext3
/usr/sbin/mkfs.ext3
/sbin/mkfs.ext3
```

**TIP** To find which directories are in the PATH use the `echo $PATH` command. This will print (echo) the contents of the variable PATH ($PATH) to your terminal.

type is a similar command which will show information about a binary, including where it is located and its type. Just use type followed by the command name:

```
$ type locate
locate is /usr/bin/locate
```

The -a parameter works in the same way as in which, showing all pathnames that match the executable. Like so:

```
$ type -a locate
locate is /usr/bin/locate
locate is /bin/locate
```

And the -t parameter will show the file type of the command which can be alias, keyword, function, builtin or file. For example:

```
$ type -t locate
file

$ type -t ll
alias

$ type -t type
type is a built-in shell command
```

The command whereis is more versatile and besides binaries can also be used to show the location of man pages or even source code for a program (if available in your system). Just type whereis followed by the binary name:

```
$ whereis locate
locate: /usr/bin/locate /usr/share/man/man1/locate.1.gz
```