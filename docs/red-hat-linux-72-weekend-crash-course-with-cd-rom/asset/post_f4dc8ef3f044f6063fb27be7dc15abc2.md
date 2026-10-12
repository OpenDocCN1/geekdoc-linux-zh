
## SESSION 9: Learning More Linux and Bash Commands

- **Session Checklist**
  - Changing the Bash prompt
  - Formatting text files
  - Changing text in files
  - Compressing and uncompressing files

This session helps you to become more familiar with Linux and Bash commands. First, you learn how to customize the Bash prompt. Then, because many Linux activities involve text files, you will learn how to format them using a few simple commands, and how to make bulk changes to text files. This session’s last topic teaches you how to work with compressed files.

### Changing the Bash Prompt

One of the most enjoyable features of Red Hat Linux is the degree to which you can customize and personalize it. Bash is no different in this respect than the more visually dominant GNOME and KDE window managers. In this section, you will learn how to change the Bash command prompt to your liking.

Before proceeding, bear in mind that Bash maintains four levels of prompts, named PS1, PS2, PS3, and PS4. PS1 is the primary command prompt and the one you will learn how to change. PS2 is the prompt Bash displays when it needs more input to complete a command. PS3 and PS4 are infrequently used, so they are not discussed in this book.

Bash lets you use over 20 different tokens to define its command prompt, the most commonly used of which appear in Table 9-1. Each token is a single letter or symbol preceded by a backslash (\), which stands for a certain element of information. You can also use literal text, such as numbers and letters, in the prompt string. To see how the prompt is defined, type `echo $PS1` and press Enter.

**Table 9-1: Common Bash Command Prompt Tokens**

| Token | Description |
| :--- | :--- |
| \h | Hostname up to the first . |
| \H | Full hostname |
| \t | Current time in 24-hour HH:MM:SS format |
| \T | Current time in 12-hour HH:MM:SS format |
| \@ | Current time in 12-hour a.m./p.m. format |
| \u | Username of the current user |
| \w | Current working directory |
| \W | Basename of the current working directory |
| \! | History number of the current command |
| \# | Command number of the current command |

For example, Bash’s default command prompt in Red Hat Linux is `[\u@\h \W]$`. As you can see from Table 9-1, this corresponds to a prompt of the form `Username@hostname currentdir$`. On a sample system, this looks like `[kwal@luther kwal]$` when he is in his home directory.

![](img/5fe8f856723cde0b366f73584b9e64b8_115_0.png)

Bash replaces the token `$` with a literal `$` for normal users. The literal `#` for the root user indicates when you are working as the root user.

Suppose you do not want to see your user name or your host name. Instead, you want to see the current time in a.m./p.m. format. To change your Bash prompt to show the time this way, type `export PS1='"\@"'` and press Enter. The change takes effect immediately, as shown in the following example:

```
[kwal@luther kwal]$ export PS1='\@ '
05:59pm $
```

The time displayed in the prompt will update each time you press Enter.

In Session 6, you learned how to use Bash’s command history. Table 9-1 listed two tokens, \! and \#, that display history information in the prompt. The \! token shows the cumulative history number of the current command. The \# token shows the command number of the current command for the current session only. (*Cumulative* refers to all commands that are stored in the Bash history file plus all commands executed during the current session.) To illustrate the difference between these two tokens, the following command sets the prompt to show the history number:

```
[kwal@luther kwal]$ export PS1='\! '
1019 $
```

The number to the left of $ indicates that the next command typed will be the 1019th command. However, by setting the prompt to show the command number, the displayed value will be much smaller because it only counts the commands executed during the current session:

```
1019 $ export PS1='\# '
21 $
```

In this case, the number to the left of the $ shows that the next command executed will be the twenty-first command in this session. The command values you can see in the prompt make it much easier to use and manipulate Bash's command history features. You can try other prompt forms until you settle on one that you like best.

### Formatting Text Files

Recall that many Linux activities involve working with text files. As Linux and Unix have evolved, many programs and utilities have been developed to process and manipulate text files. You will learn how to use two of these in this session: `cut` and `fmt`. These two commands reduce or eliminate much of the tedium and repetition of manipulating text files and reformatting text files.

#### Selecting text with cut

The `cut` command selects user-specified parts of each line in a file and stores those parts to stdout. The general format of the `cut` command is:

```
cut option file
```

`option` tells `cut` what information to select, and `file` tells `cut` the file to use. Table 9-2 lists the most common options.

**Table 9-2: Common cut Options**

| Option | Description |
| :--- | :--- |
| -c columns | Displays the columns specified by columns. |
| -f fields | Selects the field number(s) specified by fields. |
| -d delim | Uses the character delim as the field separator (the tab character is the default). |

You can use the `-c` option to select specific columns (or characters) from each line. The fields are specified by number, starting with 1. By default, fields are tab-separated, but the `-d` option lets you declare a different field delimiter, or separator.

Suppose you have a file named `phnlst.txt` that consists of the names and telephone numbers of your friends, such as the following:

![](img/5fe8f856723cde0b366f73584b9e64b8_117_0.png)

A tab separates the names from the telephone numbers. Suppose you want to display only the names in the file. Because tab characters separate the names and telephone numbers, use `cut`'s `-f` with the numeral 1 to tell `cut` to display only the first field. Executing the command `cut -f 1 phnlst.txt` will show only the names in the file (you type the following bold text):

```
cut -f 1 phnlst.txt
Kurt Wall
Naba Barkakat!
Bubba Tippets
```

If, on the other hand, you only want to see your friends' first names, combine the `-f` option with the `-d` option to define the space character as the field delimiter:

```
cut -f 1 -d " " phnlst.txt
Kurt
Naba
Bubba
```

Notice that the space character had to be embedded between double quotes (" ") to make the command work properly. If you only want to see the prefix of each telephone number, you could use the command `cut -f 2 -d " " phnlst.txt`.

To display one or more columns, use `cut`'s `-c` option, followed by a list of the columns to show. Use the comma character (,) to list non-contiguous characters and the minus sign (-) to identify a range of contiguous characters. For example, the command `cut -c 1,5 phnlst.txt` will show the first and fifth characters in each line, while the command `cut -c 6-8 phnlst.txt` will show columns 6, 7, and 8 from each line.

![](img/5fe8f856723cde0b366f73584b9e64b8_117_1.png)

#### Reformatting paragraphs with fmt

The `fmt` command makes short work of reformatting paragraphs. It is especially useful for breaking long lines of text into shorter lines and removing superfluous spaces. For example, suppose you have a text file named `fmtme.txt` that looks like the following:

```
fmt* prefers breaking lines at the end of a sentence, and tries to avoid line breaks after the first word of a sentence or before the last word of a sentence. A “sentence break” is defined as either the end of a paragraph or a word ending in either a period (.), a question mark (?), or an exclamation point (!), followed by two spaces or the end of a line, ignoring any intervening parentheses or quotes.
```

Although you cannot see it in the printed text, there are no embedded new lines or carriage returns in the text, so if you viewed this file in the vi editor, it would look like Figure 9-1.
