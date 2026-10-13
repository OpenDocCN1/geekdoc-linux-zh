# Dealing with Arguments

To illustrate the use of options, let's change the nytar script to use its first argument, $1, as the mode argument and $2 as the tar file to read or create. You can implement this change as follows:

```
USAGE="usage: $0 [-c|-t] [file|directory]"
case "$1" in
  -t) TARGS="-tvf $2" ;;
  -c) TARGS="-cvf $2 $2" ;;
  *) echo "$USAGE"
     exit 0
     ;;
esac
```

The three main changes are as follows:

+   - All references to $1 have been changed to $2 because the second argument is now the filename.
+   - listtar has been replaced by -t.
+   - maketar has been replaced by -c.

Now running nytar produces the following output:

Usage: ./nytar [-c|-t] [file|directory]

To create a tar file of the directory fruits with this version, use the command

```
$ ./nytar -c fruits
```

To list the contents of the resulting tar file, fruits.tar, use the command

```
$ ./nytar -t fruits
```

# Using basename

Currently, the usage statement of nytar outputs the entire path with which the script was invoked. What it should really output is just the name of the script. You can correct this by using the basename command.

The basename command takes an absolute or relative pathname to a file or directory and returns just the file or directory name from that path. The basic syntax is as follows:

```
basename file
```

For example,

```
$ basename /usr/bin/sh
```

prints the following:

```
sh
```