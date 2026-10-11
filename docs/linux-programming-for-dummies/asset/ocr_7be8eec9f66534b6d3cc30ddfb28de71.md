To set the `sort` utility to ignore the case distinction, use the `-f` option:

```
sort -f names
```

Another `sort` option (`-n`) tells the `sort` utility to order the file in numerical order. Still another `sort` option (`-m`) tells the `sort` utility to order by month. The `-m` `sort` option places `January` before `February`, `February` before `March`, and so on.

One drawback as you're using the `sort` utility is that the utility doesn't save the new, sorted list in the same file that contains the original, unsorted list. After you `sort` the `names` file, the results appear on-screen unless you use the redirection operator `>` to save the information to another file. (For a description of redirection operators, see `Chapter 5`.) If you want to save the results to a file, you must use the redirection operator.

What if you want to place the ordered information in the same file? The following example shows you how to do so:

```
sort -f names > newnames
mv newnames > names
```

The `sort` utility reorders the `names` file (ignoring the case distinction) and saves the sorted information in the `newnames` file. The last line renames the `newnames` file to the old file, `names`, by using the `move` (`mv`) command.

# ## Checking Differences Between Files: `diff`

After you begin programming in Linux, you inevitably come across the problem of having two files with practically the same name that contain your program. You may have this problem if you save a backup copy of your work, modify one copy, and then forget which copy you modified. How do you find the differences between the files?

You can compare each file line by line yourself, or you can have the `diff` utility do it for you. If you type the following line on the command line, you tell the `diff` utility to read `file1` and `file2`, compare the two files, and indicate the different lines in each file:

```
diff file1 file2
```

Say that you execute the `diff` utility from the command line. The following example shows what the `diff` utility may report back to you on-screen:

```
<Programming is fun.
>I hate computers.
```