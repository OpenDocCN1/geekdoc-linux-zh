You can use test to ask a question about the status of a file argument or the relationship between two file arguments. After verifying that at least one argument has been given on the command line, the following scripts test whether the argument is the name of a regular file (not a directory or other type of file) in the working directory. The test builtin with the -f option and the first command line argument ($1) check the file:

```
$ cat is_regregfile
if test $# -eq 0
then
    echo "You must supply at least one argument."
    exit 1
fi
if test -f "$1"
then
    echo "$1 is a regular file in the working directory"
else
    echo "$1 is NOT a regular file in the working directory"
fi
```

You can test many other characteristics of a file with test and various options. Some of the options are listed in Table 13-1

| Option | Test Performed on File | || table 13-1 |
|---|---|---|
| -d | Exists and is a directory file | |
| -e | Exists | |
| -f | Exists and is a regular file | |
| -r | Exists and is readable | |
| -s | Exists and has a length greater than 0 | |
| -W | Exists and is writable | |
| -X | Exists and is executable | |

Other test options provide a way to test for a relationship between two files, such as whether one file is newer than another. Refer to later examples in this chapter, as well as to test in Part III for more detailed information. (Although test is a builtin in bash and zsh, the test utility described in Part III on page 1352 functions similarly.)