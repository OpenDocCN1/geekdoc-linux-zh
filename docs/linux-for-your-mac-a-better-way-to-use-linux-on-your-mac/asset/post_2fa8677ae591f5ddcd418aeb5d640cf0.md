
The difference between the grep commands may not be readily apparent unless you are familiar with each command’s capabilities. For example, the egrep command is easily suited to the task of finding simple strings in files. For example:

```bash
$ cd /usr/share/doc/howto/en
$ egrep "(d)" *
```

UPS-HOWTO: (d) DSR and DCD are dropped to zero -> power has failed and

In this example, the egrep command is asked to display all lines from files with the matching string (d). If you try the same match using the egrep command, you will get thousands of screens of text! Why? Because the egrep command uses a different syntax, and must use extended expressions. The correct egrep equivalent command line is:

```bash
$ egrep "\(d)\)" *
```

In this example, the parentheses are properly escaped. Since the search is only for one character, the line could also be written:

```bash
$ egrep "[d]" *
```

Some of the constructs used to build expressions include:

| Syntax | Description |
| :--- | :--- |
| `pat$` | Match pat at the end of a line |
| `[-z]` | Match starting character in range |
| `*` | Match any character |
| `\x` | A character such as ? or \ |
| `^pat` | Match pat at start of line |
| `.` | Match single character |
| `?` | Match single character |
| `{str}STR}` | Match string str or STR |
| `{ABC}` | Match A, B, or C once |
| `*[a-z]` | Match ending character in range |
| `[a-z]` | Match character in range |
| `XYZ]+` | Match X, Y, or Z at least once |
| `{n}` | Match previous character n times |

Another document describing regular expressions is found in the regex manual page (to read the document, type `man 7 regex` and press Enter).

## Customizing the Shell Prompt

Your shell’s prompt is defined by one or more environment variables. When using the bash shell, the value of the PS1 variable defines the first login prompt. This value, defined by default by your system’s /etc/profile, determines what kind of information is displayed in your shell prompt.

You can use the printenv command, along with the fgrep command, to display the current prompt definition like this:

```bash
$ printenv | fgrep PS1
```

You may see the following value returned:

```bash
PS1=\u@h:\w >
```

This example from a SuSE Linux system indicates that the shell prompt should be the user’s name, then the at symbol (@), followed by the hostname of the computer, a colon (:), the current working directory, and finally, a greater than (>) symbol. This will look like:

```bash
bball@cubie: ~ >
```

Note in this example that the home directory is shown as a tilde (~). Read the bash manual page to see a list of predefined values you can use for your shell prompt. Some of the more commonly used variables are:

| Variable | Description |
| :--- | :--- |
| `\d` | The date in “Wed March 07” format |
| `\h`, `\H` | Host name of the computer |
| `\s` | Name of the shell |
| `\t` | The time in 24-hour format |
| `\T` | The time in 12-hour format |
| `\u` | Username |
| `\w` | Current working directory |
| `\W` | Basename of the current working directory |
| `\#` | Number of this command |
| `\\` | A backslash |

You can redefine your shell prompt by redefining or exporting your shell’s prompt variable. For example, if you use bash and would rather see the time updated after every command, use bash’s export command like this:

```bash
$ export PS1='It is now: \t $ '
```

After you press Enter, you will see:

```bash
It is now: 17:10:50 $
```

## Customizing the Console

This section introduces a number of ways you can customize the appearance of your console. You will see how to change your console’s fonts and color usage. If you spend a lot of time at the console, this can be a great way to reduce eyestrain and adjust your work environment.

### Changing the Console Fonts

When booting Linux to the text-only or console mode, most users accept the default font provided by the Linux distribution, which generally provides an 80-character by 25-line screen. Does this mean you cannot use other fonts? Certainly not!

Nearly all Linux distributions come with 150 to nearly 200 different fonts that may be used with the console. You will find these fonts under the /usr/lib/kbd/consolefonts directory. Use the `setfont` command to immediately change the font used at your console. For example, if you would prefer a smaller font, try using the `alt-8x14` font (compressed, with a .gz extension) with the `setfont` command like this:

```bash
$ setfont /usr/lib/kbd/consolefonts/alt-8x14.gz
```

You will find many different types of fonts available for your system.

### Booting Console Fonts

Intel-based Linux users can also change fonts by using the Intel-based Linux LILO command. However, this approach is not supported when using Linux on the PowerPC.

### Changing the Console Colors

The Linux console recognizes a number of control codes and escape sequences that can be used to set the default background and foreground (text color) of your display. The default console uses white characters on a black background. However, if you would prefer to use green characters with a black background, use the `echo` command, its `-e` option, and the magic sequence like this:

```bash
$ echo -e '\033[32m'
```

After you press Enter, your characters will now be in green. To make this the default color scheme for your session, again use the `echo` command, but like this:

```bash
$ echo -e '\033[0m'
```

To go back to your default console, use:

```bash
$ echo -e '\033[0m'
```

The `console_codes` man page details nearly all the codes you can use to change the color or cursor attributes for your console. For details on how to customize the default color settings used in the `ls` command when displaying files and directories, see the `ls` man page. In general, using the `LS_OPTIONS` or `LS_COLORS` environment variables enable this option.

### How to Use Virtual Consoles

When you use Linux in its console or text-only mode, you can jump to another login prompt and start multiple sessions or log in as another user. By default, most Linux distributions provide a Linux kernel that supports six login sessions, or *virtual consoles*. The consoles are numbered one through six, and represented by function keys one through six.

Jumping to another virtual console is quite easy. Using SuSE Linux, press Cmd+F2 to go to the second virtual console. Yellow Dog Linux users may have to press Ctrl+Cmd+2. To return to the original console, press Cmd+F1. Linux/PPC 2000 users may have to use the following `chvt` command:

```bash
$ chvt 2
```

After you press Enter, you will be at the second console, and will be presented a login prompt. After logging in, you can return to the first console by using the `chvt` command like this:

```bash
$ chvt 1
```

Using multiple logins is a handy way to run different text-based applications at once in full-screen mode on your notebook.

### Resources

- http://www.apple.com/applescript/techsheet/AppleScript.00.html. All about Apple's AppleScript for Mac OS.
- http://www.luv.asu.au/overheads/shells-talk.html. An overview of shells for Linux.
- http://www.gnu.org/software/bash/bash.html. Home page for the bash shell.
- http://www.ibiblio.org/pub/Linux/system/shells/. One source for a number of different shells for Linux.
- http://www.cs.mun.ca/~michael/pdksh/. Home page for pdksh and new versions.
- http://www.kornshell.com/. Home page for the formerly proprietary, closed-source Korn shell. You can download the latest version of the commercial KornShell through this home page.
- ftp://ftp.astron.com. The primary site for the latest version of tcsh.
- http://www.primate.wisc.edu/software/csh-tcsh-book/#sources. A great site with many links to more information about tcsh, including Bill Joy’s abstract and introduction to the C shell (csh-intro.ps) in PostScript format.
- http://sunsite.dk/zsh/. Home page for the Z shell, included with nearly every Linux distribution. Check this site for the latest versions, up-to-date documentation, and a handy reference card!
- ftp://ftp.zsh.org. Home site for downloading the latest version of the Z shell.
- http://www.faqs.org/faq/unix-faq/shell/shell-differences/. The UNIX FAQ on differences between shells.
- http://www.linuxppc.org/documentation/?css_ok=1. The Linux PPC documentation page, with links to many different sources of information about PPC Linux.
- http://etext.lib.virginia.edu/helphsheets/regex.html. An on-line guide to using regular expression patterns.
