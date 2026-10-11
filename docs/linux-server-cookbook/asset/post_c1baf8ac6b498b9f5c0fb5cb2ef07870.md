
## Commands grep

- Check the content of the file and filter starting with the letter r, followed by a letter o or several, and ending with a letter t:

```
agonzalez@ubuntu:~$ grep -E ro*t text
rt
rot
root
```

Figure 5.37: Example using the command grep

- Check the content of the file and filter starting with the letter r, followed by a letter o or several, and ending with a letter t:

```
agonzalez@ubuntu:~$ grep -E ro+t text
rot
root
```

Figure 5.38: Example using the command grep

- Check the content of the file and filter starting with the letter r, followed by an o (optional) and ending with a letter t:

```
agonzalez@ubuntu:~$ grep -E ro?t text
rt
rot
```

Figure 5.39: Example using the command grep

- Check the content of the file and filter starting with the letter r, followed by two letters o, and ending with the letter t. Filter to starting with letter p, followed by 1 or 2 letters e and ending with letter n:

![](img/863afa537de4eed7deb11978bfbfa90e_170_0.png)

Figure 5.40: Example using the command grep

- Check for the word agonzalez and root in two different ways:

![](img/863afa537de4eed7deb11978bfbfa90e_170_1.png)

Figure 5.41: Example using the command grep

## Commands awk

AWK is a pattern scanning and processing language. The tool awk uses regular expressions to match lines, and it allows to print some parts. This command has many options and possibilities for complex operations; only some real use cases are shown in figures 5.42 and 5.43:

- Print the username of the users using shell bash:

![](img/863afa537de4eed7deb11978bfbfa90e_170_2.png)

Figure 5.42: Example using the command awk

- Search the string /home and print the columns for the username, the home, and the shell:

![](img/863afa537de4eed7deb11978bfbfa90e_170_3.png)

Figure 5.43: Example using the command awk with the output of the command cat

## Formatting the output

Linux provides several tools to format the content of a file or the output of another command. These commands are part of the package coreutils, which is installed by default on the Linux distributions. Table 5.18 shows some of the popular commands and their description:

| Command | Description |
| :--- | :--- |
| nl | Number lines of files |
| sort | Sort lines of a text file |
| tac | Shows the files specified in reverse |
| tr | Translate or delete characters |
| sed | Filters and transforms text |
| rev | Reverse lines character wise |
| wc | Word and line count |
| fmt | Simple optimal text formatter |
| uniq | Omit or report repeated lines |
| join | Join lines of two files on a common field |
| paste | Merge lines of files |
| shuf | Generate random permutations |

Table 5.18: Popular commands for formatting output

Figures 5.44 to 5.55 show one example for each of the commands:

- Using nl to numerate the lines of one file:

```
agonzalez@ubuntu:~$ nl /etc/legal
1 The programs included with the Ubuntu system are free software;
2 the exact distribution terms for each program are described in the
3 individual files in /usr/share/doc/*/copyright.
4
5 Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by applicable law.
```

Figure 5.44: Output example for the command nl

- Using sort for alphabetical sort:

```
agonzalez@ubuntu:~$ awk -F":" ' /bash$/{print $1}' /etc/passwd | sort
agonzalez
root
testuser
```

Figure 5.45: Output example for the command sort.

- Using tac to visualize a file in a reverse way:

```
agonzalez@ubuntu:~$ tac /etc/legal
applicable law.
Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
individual files in /usr/share/doc/*/copyright.
the exact distribution terms for each program are described in the
The programs included with the Ubuntu system are free software;
```

Figure 5.46: Output example for the command tac

- Using tr to convert characters from the text:

```
agonzalez@ubuntu:~$ echo "UXXER CASE LINE" | tr '[A-Z]' '[a-z]' | tr 'x' 'p'
upper case line
```

Figure 5.47: Output example for the command tr

- Using sed to convert expressions from the text:

```
agonzalez@ubuntu:~$ cat /etc/hostname
ubuntu.example.com

agonzalez@ubuntu:~$ cat /etc/hostname | sed 's/example.com/localdomain/'
ubuntu.localdomain
```

Figure 5.48: Output example for the command sed

- Using rev to reverse line character-wise:

```
agonzalez@ubuntu:~$ echo "Hello world" | rev
dlrow olleH
```

Figure 5.49: Output example for the command rev

- Using wc to count lines, words, and characters of one file:

```
agonzalez@ubuntu:~$ wc /etc/legal
8  38 267 /etc/legal
```

Figure 5.50: Output example for the command wc

- Using fmt to format the output reformatting paragraphs to use 60 characters width:

```
agonzalez@ubuntu:~$ fmt -w 60 /etc/legal
The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in
the individual files in /usr/share/doc/*/copyright.
Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted
by applicable law.
```

Figure 5.51: Output example for the command fmt

- Using uniq to remove from the output the duplicated lines. Duplicated lines need to be adjacent:

```
agonzalez@ubuntu:~$ cat uniq.txt
one
two
three
two
one
agonzalez@ubuntu:~$ cat uniq.txt | sort | uniq
one
three
two
```

Figure 5.52: Output example for the command uniq

- Using join to combine two files with a common field:

```
agonzalez@ubuntu:~$ cat names.txt
1 Alberto
2 John
3 Linus
agonzalez@ubuntu:~$ cat lastname.txt
1 Gonzalez
3 Torvalds
agonzalez@ubuntu:~$ join names.txt lastname.txt
1 Alberto Gonzalez
3 Linus Torvalds
```

![](img/863afa537de4eed7deb11978bfbfa90e_174_0.png)

- Using paste to merge two files line by line:

```
agonzalez@ubuntu:~$ cat names1.txt
Alberto
Linus
John

agonzalez@ubuntu:~$ cat lastname1.txt
Gonzalez
Torvalds

agonzalez@ubuntu:~$ paste names1.txt lastname1.txt
Alberto Gonzalez
Linus Torvalds
John
```

![](img/863afa537de4eed7deb11978bfbfa90e_174_1.png)

- Using shuf to randomly sort the lines:

```
agonzalez@ubuntu:~$ shuf /etc/passwd | head -1
apt:x:100:65534::/nonexistent:/usr/sbin/nologin
agonzalez@ubuntu:~$ shuf /etc/passwd | head -1
systemd-resolve:x:102:103:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
```

![](img/863afa537de4eed7deb11978bfbfa90e_174_2.png)

## File editors and file managers

Editing files is one of the common tasks when we operate with a Linux system. Edit configuration, developing scripts or applications, creating content such as documentation, or any other task related to files are usual tasks. For this purpose, there are available visual editors (GEdit, Visual Studio, and Kate as some examples) and text-based editors, which are more popular due to are usually already on the systems to administrate, either local or remote servers. The most popular editors are as follows:

- **nano:** a small and friendly editor. It allows editing a file in a quick way, with the possibility to open several files, have syntax highlight, and line numbering, among other features.

- **vi and vim:** vi is one of the most popular editors in Linux. Despite of its complexity, it is used by most Linux users, which requires advanced features during editing files. **vim** (VI Improved) enhances the traditional **vi** adding features such as multiple windows, syntax highlighting, and visual selection, among other features.

- **emacs:** This editor, like VI, is a complex one but used by many users. The biggest advance of this editor is the extensibility, not used only as a file editor but as a suite of tools such integrated browser, file manager, e-mail read, git integration, and much more functionalities.

This section will cover the basics for each of them. The editor **nano** is shown in figure 5.56 after running it with the argument **names.txt**:

![](img/863afa537de4eed7deb11978bfbfa90e_175_0.png)

In the bottom part of the screen, it indicates the actions available, and these actions are accessible using Ctrl+Key. For example, to write the changes is need to press Ctrl+O. For exiting the editing, the combination is Ctrl+X. Figure 5.57 shows the editor vim. The editor VIM has three modes:

- **Normal mode:** in this mode is possible to write the changes, exit the application, copy lines, paste lines, and perform other operations related to
