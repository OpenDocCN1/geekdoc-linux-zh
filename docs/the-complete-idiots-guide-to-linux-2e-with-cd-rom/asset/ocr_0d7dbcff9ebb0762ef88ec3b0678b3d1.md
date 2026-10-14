the shell will have some side effect you didn’t intend.

To enable noclobber, type the following on your bash shell:

```
noclobber=1
```

If you are using a different shell, like the C shell, you might want to try this:

```
set noclobber=1
```

To test if the command took, type the following:

```
[alberto@digital alberto]$ noclobber=1
[alberto@digital alberto]$ touch file
[alberto@digital alberto]$ date > file
bash: file: Cannot clobber existing file
```

If you get the same error, noclobber is set properly. I tried to redirect the output of a command called date to file. Because file already existed, such redirection would have caused the contents of file to be replaced by whatever date printed. Such action is not allowed when you have noclobber defined in your environment. (The date command is covered in Chapter 17, "Command Toolbox: Useful Shell Commands and Shortcuts.")

Now that you know about redirection, let me show you a neat trick: Let’s use the cat command as a minimal text editor. We can do this by issuing the cat command and then redirecting the output to a file, like this:

```
[alberto@digital alberto]$ cat > /tmp/message.txt
This is a test. Until I type a Ctrl+D, I can type all that I want.
I can even enter new lines.

-- Alberto
[alberto@digital alberto]$ cat /tmp/message.txt
This is a test. Until I type a Ctrl+d, I can type all that I want.
I can even enter new lines.

-- Alberto
[alberto@digital alberto]$
```

With redirection, you can use cat as a simple editor. You can edit the current line you are working on, as the shell won’t grab the characters until you hit Enter. To finish entering text, just press Ctrl+D.

# Appending a File: >>

Redirecting is very useful, but sometimes you don’t want to replace the file’s previous contents. Instead, you might want to add information to the end of a file. Maybe you want to maintain a list of all your favorite Web sites. In such a case, adding a new entry should not replace the entire file but augment it.

Instead of using a single >, you use a >> to tell the shell to append new output instead of overwriting. If the file doesn’t exist, it is created, like this:

```
[alberto@digital alberto]$ cat > /tmp/websites
www.caldera.com
www.redhat.com
[alberto@digital alberto]$ cat >> /tmp/websites
www.mcp.com
[alberto@digital alberto]$ cat /tmp/websites
www.caldera.com
```