# FOR EXAMPLE

You could use the following function to test whether a parameter is the name of a regular file that is also readable:

```
# f723 -- Test if parameter 1 is a readable regular file
function f723 {
  [[ -f "$1" && -r "$1" ]] && {
    print "$1 is a readable regular file."
    return
  }
  print "\$1" is not a readable regular file.
}
```

In this example, the && operator is used twice. Inside the double brackets, it performs a logical "and" between the -f and -r tests; the second time it is used in the way you have already seen (Lab 3.2, "Command Groups") to perform a logical "and" between the double bracket and the print/return command group inside the braces.

The two uses work just about the same way, with the shell using true/false values to decide how much work to do. The double bracket command has a true exit code if both the -f and -r tests are.

As with && used for command grouping, the shell evaluates the right-hand side of a && only if the left-hand side's result is true.

> If you are not familiar with the ideas of file modification times or the permission bits that UNIX systems associate with files (read, write, execute), you should consult your documentation. Likewise, if you are running KornShell on a non-UNIX system that does not have similar file system capabilities, the tests used in this exercise may not work for you. For example, U/WIN running a FAT file system cannot mimic all these features, although U/WIN does fine with an NTFS file system.

![](bbox=[0.025, 0.613, 0.115, 0.693])

Put f723 in your fun directory, and run the following commands:

```
f723 ~/.kshrc
f723 ~/bin
f723 "A figment of your imagination"
```