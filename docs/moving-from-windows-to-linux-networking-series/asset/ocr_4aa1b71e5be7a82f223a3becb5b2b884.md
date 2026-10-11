| head | This command returns just the first few lines of a file. This is useful when searching for a particular file. Rather than opening the entire file, just view the first few lines to see if it is the one you want. Example: `head myfile.txt` | There is no Windows equivalent. |
| --- | --- | --- |
| cat | This command will concatenate two files. The two files are put into one, one file being appended to the end of the other. Example: `cat myfile1.txt myfile2.txt` | There is no Windows equivalent. |
| > | This is the redirect command. Instead of displaying the output of a command such as `ls` to the screen, it redirects it to a file. Example: `ls > file1.txt` | This works in the Windows command prompt in much the same way. |

# diff and cmp

These two commands are used to compare two files and determine what differences the two files have. In order to demonstrate these commands, we will have to create two sample text files. For demonstration purposes you can open up any Linux text editor (Kate or KWrite, for example) and type in the following three lines:

```
```
Linux is very cool
I love Linux
It is awesone
```
```

Save that as `file1.txt`. Start a new text file and enter these three lines:

```
```
Linux is very cool
I love Linux
It is great
```
```

Save that as `file2.txt`. You should notice that, except for the last line, these two files are identical. This is intentional, as it gives us a chance to explore the `diff` and `cmp` commands and find the differences between these two files. Now we can use both the `diff` command and the `cmp` command and see what they tell us about these two files. Figure 18.3 shows the output from running the `cmp` command. Figure 18.4 shows the output from running the `diff` command.

![](bbox=[0.06, 0.67, 0.51, 0.92])

**Figure 18.3:** The `cmp` command.