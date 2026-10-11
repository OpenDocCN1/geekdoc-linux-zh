
![](img/12d790664598bbf390261087fbe55bbc_369_0.png)

Figure 18.2: The HISTSIZE command.

- **Note**: Technically speaking, HISTSIZE is not a command per se. It is actually an environmental variable. However, for our purposes here it works like and can be used like other commands.
- **Note**: You must type in the shell commands exactly as you see them in this text or they will not work. For example, HISTSIZE=5 is all uppercase letters with no spaces. Typing it in any other way will not work. Most shell commands are all lowercase. These commands are case sensitive.

The history and HISTSIZE commands can be very useful. There may be occasions when you need to know what was done a few commands back. Another useful command is clear. Enter the word clear and press Return and it will clear the current view of the shell. This can be useful when you have to run several commands and the shell is appearing a bit cluttered.

While we will be working with the bash shell, you may be curious as to how you would go about invoking the other shells that we have mentioned. One obvious way is to set up that shell as the default shell for that user. However, there should be some way to change what shell you are using while the terminal is open. Fortunately, there is a way to do that very thing. You enter the abbreviation for that shell, and you will then be using that shell. For example, if you want to use the C shell, type in csh and then press Enter. You will not see any dramatic change in the appearance of the shell itself. In fact, you will see very little change. The cursor prompt will change slightly, indicating that you are using a different shell. In fact, that will be the only immediate indication that you have invoked a different shell. All the shell commands we will work with in this book will work in any shell. However, if you switch to C shell, you can do all the commands that are unique to that shell. When you are ready to switch back to bash, just enter bash. You can invoke the various other shells with just as much ease. Typing in ksh will invoke the Korn shell, and sh will invoke the Bourne shell. Changing between shells is a very easy thing to do.

There are two other very important shell commands you need to be aware of. Both of these will provide valuable information about other commands. The first is the man command, which was discussed briefly earlier in this book. Linux has a built-in manual. When you enter man followed by a particular command, you will display the manual page for that command.

For example, if you want to know about the ls command, enter man ls. You will immediately discover that most commands have several flags you can pass to them to make them behave differently. A flag is a character such as a letter that tells the command to modify its behavior in some way. You also will need to know how to exit the manual page when you are done reading it. That is simple; just enter the letter q, and you will quit the manual page.

Another useful command is help. If you enter a command followed by two dashes and the word help, you will see a brief list of flags you can pass to that command. help is sort of like an abbreviated manual page. An example of using help is shown here:

```
ls --help
```

## File and Directory Management

In *Chapter 3* you were briefly introduced to some file and directory management commands. You were shown how to create directories, copy files, list contents of a directory, and remove files and directories. Several of the commands explored in *Chapter 3*, and a few new ones that we will examine now, are shown in *Table 18.1*.

**Table 18.1: File and Directory Management Commands**

| Linux Command | Explanation and Example | Windows Command Prompt Equivalent |
| :--- | :--- | :--- |
| `ls` | This lists the contents of the current directory. **Example:** `ls` | The `dir` command is equivalent to the `ls` command. **Example:** `dir` |
| `cp` | This copies one file to another directory. **Example:** `cp filename.txt directoryname` | The `copy` command is equivalent to the `cp` command. **Example:** `copy filename.txt directoryname` |
| `mkdir` | The `mkdir` command creates a new directory. **Example:** `mkdir directoryname` | The `md` command is the equivalent of the `mkdir` command. Its syntax is identical to `mkdir`. **Example:** `md directoryname` |
| `cd` | The `cd` command is used to change directories. **Example:** `cd directory name` | The `cd` command is also used in Windows, and its syntax is identical. **Example:** `cd directoryname` |
| `rm` | The `rm` command is used to delete or remove a file. **Example:** `rm filename` | The `del` command is the equivalent to the `rm` command. **Example:** `del filename` |
| `rmdir` | The `rmdir` command is used to remove or delete entire directories. **Example:** `rmdir directoryname` | The `rd` command is the equivalent of the `rmdir` command. **Example:** `rd directoryname` |
| `mv` | This command is used to move a file. **Example:** `mv myfile.txt myfolder` | The equivalent command in Windows is `move`. **Example:** `move myfile.txt myfolder` |
| `diff` | This command performs a byte by byte comparison of two files and tells you what is different about them. **Example:** `diff myfile.txt myfile2.txt` | The `comp` command will perform a binary comparison of two files. |
| `cmp` | This command performs a textual comparison of two files and tells you the difference between the two. **Example:** `cmp myfile.txt myfile2.txt` | There is no equivalent command in Windows. |
| `spell` | This command performs a spell check on a target file and tells you if any words are misspelled. **Example:** `spell myfile.txt` | There is no equivalent command in Windows. |
| `head` | This command returns just the first few lines of a file. This is useful when searching for a particular file. Rather than opening the entire file, just view the first few lines to see if it is the one you want. Example: `head myfile.txt` | There is no Windows equivalent. |
| `cat` | This command will concatenate two files. The two files are put into one, one file being appended to the end of the other. Example: `cat myfile1.txt myfile2.txt` | There is no Windows equivalent. |
| `>` | This is the redirect command. Instead of displaying the output of a command such as `ls` to the screen, it redirects it to a file. Example: `ls > file1.txt` | This works in the Windows command prompt in much the same way. |

## diff and cmp

These two commands are used to compare two files and determine what differences the two files have. In order to demonstrate these commands, we will have to create two sample text files. For demonstration purposes you can open up any Linux text editor (Kate or KWrite, for example) and type in the following three lines:

```
Linux is very cool
I love Linux
It is awesome
```

Save that as `file1.txt`. Start a new text file and enter these three lines:

```
Linux is very cool
I love Linux
It is great
```

Save that as `file2.txt`. You should notice that, except for the last line, these two files are identical. This is intentional, as it gives us a chance to explore the `diff` and `cmp` commands and find the differences between these two files. Now we can use both the `diff` command and the `cmp` command and see what they tell us about these two files. Figure 18.3 shows the output from running the `cmp` command. Figure 18.4 shows the output from running the `diff` command.

![](img/12d790664598bbf390261087fbe55bbc_371_0.png)

**Figure 18.3:** The `cmp` command.

![](img/12d790664598bbf390261087fbe55bbc_372_0.png)

**Figure 18.4:** The `diff` command.

You are probably thinking that the `diff` command gives you more information than the `cmp` command, but that is not exactly accurate. The two commands give different output because they compare the files differently. The `cmp` command compares the files byte by byte in their binary format. Remember that ultimately everything in your computer is stored as ones or zeros (binary format). Therefore, it reports the specific bytes that are different. The `diff` command performs a textual comparison and returns what line or lines of text are different. Both of these commands can be quite useful. For example, if you have two versions of the same file and want to know exactly what is different between the two, either the `diff` or the `cmp` command can tell you.

## spell, head, cat, and redirect

The next four commands we will look at are very useful when you are working with text files. The first of these commands, the `spell` command, is used frequently by most Linux users. You use this command to find any misspelled words in a file. When you run the `spell` command, it will return all words in that file that are misspelled. The misspelled words will be listed vertically as they are in Figure 18.5.

![](img/12d790664598bbf390261087fbe55bbc_372_1.png)

**Figure 18.5:** The `spell` command.

The `head` command is very useful for searching through files. If you are seeking a particular file and do not recall what the filename is, in Windows you would have to open each file that you think might be it and scan it to see if it is indeed the file you are looking for. The `head` command will return just the first few lines of a file, and that is usually enough to determine if it is the file you are seeking. This is shown in Figure 18.6.
