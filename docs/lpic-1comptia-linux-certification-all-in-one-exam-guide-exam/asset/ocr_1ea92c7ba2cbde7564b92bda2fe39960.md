example, the command **touch my\_file.txt** was issued from within the home directory of the rtracy user:

```
```
rtracy@fs2:~> touch my_file.txt
rtracy@fs2:~> ls -l my*
-rw-r--r-- 1 rtracy users 0 2011-02-01 11:36 my_file.txt
rtracy@fs2:~>
```
```

After entering touch, the ls command was entered. You can see that a 0-byte file was created named my\_file.txt in /home/rtracy. If you wanted to create the file elsewhere in the file system, you would use an absolute path with the filename.

# ## Viewing File Contents

As we discussed earlier, your Linux system and the services that run on it are configured using simple text files stored in (usually) the /etc directory in the file system. In addition, many of your system log files are saved as text files. Because Linux uses text files to configure and manage just about everything, you will frequently need to view the contents of files.

In the preceding chapter, you learned how to use text editors to open a file for viewing and editing. This works very well. However, there will be many occasions when you simply want to quickly view a text file on screen and don't need or want to load up a text editor. Linux provides you with a variety of command-line tools that you can use to do this. These include the following:

+   - **cat** The **cat filename** command will display the specified text file on screen. For example, if you needed to view the /etc/xinetd.conf configuration file, you would enter **cat /etc/xinetd.conf** at the shell prompt.

> TIP The cat command doesn't pause the output, so if you use it to view a long file you may need to pipe it to the more program (| more) to pause the output a page a time.

+   - **less** The **less filename** command can also be used to display the specified text file on screen, much like cat. However, the less command automatically pauses a long text file one page at a time. You can use the SPACEBAR, PAGE UP, PAGE DOWN, and ARROW keys to navigate around the output.

+   - **head** The **head filename** command is used to display the first couple of lines of a text file on the screen.

+   - **tail** The **tail filename** command is used to display the last couple of lines of a text file on screen. The tail command is particularly useful when displaying a log file on screen. When viewing a log file, you usually only need to see the end of the file. You probably don't care about log entries made several days or weeks ago. You can use tail to see just the last few log entries added to the end of the file.