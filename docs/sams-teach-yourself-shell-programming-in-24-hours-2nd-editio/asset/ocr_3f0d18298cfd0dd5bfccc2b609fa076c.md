file, but often you need more control over lines that are displayed. The head and tail commands provide some of this control.

# The head Command

The head command is used to display the first few lines of a file. Its basic syntax is

```
head [-n lines] files
```

Here files is the list of the files you want the head command to process. Without the -n lines option, the head command shows the first 10 lines of its standard input. When this option is specified, head shows the number of lines specified by lines instead.

![](bbox=[0.28, 0.52, 0.35, 0.6])

> On some versions of Linux the output from the -n lines option might include one line less than the number of lines you specified. For example, the command:
> 
> $ head -n 5 file
> 
> may produce only four lines of output rather than the expected five.

Although this command is useful for viewing the tops of large README files, its real power happens in daily applications. Consider the following problem: you need to generate a list of the five most recently accessed files in a directory. You can devise a solution to this problem by breaking the problem down. First, you can generate a list of the files in the directory using the ls -l command. For example, if you are interested in the files in the directory /home/ranga/public_html, you can use the following command:

```
$ ls -l /home/ranga/public_html
```

In this case, the following list of files and directories is generated:

+   - rcs
+   - cgi-bin
+   - downloads
+   - humor
+   - images
+   - index.html
+   - misc
+   - projects
+   - school

Next, you need to sort the list by the date of the last access. This can be accomplished by specifying the -ut (sort by last accessed time) option of the ls command:

```
$ ls -lut /home/ranga/public_html
```