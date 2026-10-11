name of an ordinary file (not a directory or other type of file) in the working directory. The `test` builtin with the `-f` option and the first command-line argument (`$1`) check the file:

```
```
$ cat is_ordfile
if test $# -eq 0
  then
       echo "You must supply at least one argument."
       exit 1
  fi
  if test -f "$1"
  then
       echo "$1 is an ordinary file in the working directory"
  else
       echo "$1 is NOT an ordinary file in the working directory"
  fi
```
```

You can test many other characteristics of a file with `test` and various options. Table 27-1 lists some of these options.

**Table 27-1 Options to the test builtin**

| Option | Tests file to see if it |
| :------- | :----------------------------------------------------- |
| `-d` | Exists and is a directory file |
| `-e` | Exists |
| `-f` | Exists and is an ordinary file (not a directory) |
| `-r` | Exists and is readable |
| `-s` | Exists and has a size greater than 0 bytes |
| `-w` | Exists and is writable |
| `-x` | Exists and is executable |


Other `test` options provide ways to test relationships between two files, such as whether one file is newer than another. Refer to later examples in this chapter for more detailed information.

# ## Always test the arguments

> tip To keep the examples in this book short and focused on specific concepts, the code to verify arguments is often omitted or abbreviated. It is a good practice to test arguments in shell programs that other people will use. Doing so results in scripts that are easier to run and debug.

The following example—another version of `chkargs`—checks for arguments in a way that is more traditional for Linux shell scripts. The example uses the bracket (`[ ]`) synonym for `test`. Rather than using the word `test` in scripts, you can surround the arguments to `test` with brackets. The brackets must be surrounded by whitespace (SPACES or TABs).