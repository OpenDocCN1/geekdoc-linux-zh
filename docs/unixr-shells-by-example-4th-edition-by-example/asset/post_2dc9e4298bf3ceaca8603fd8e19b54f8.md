
# Table 13.8 vi Commands (continued)

| Command | Function |
|---|---|
| Editing with vi | |
| a A | Append text |
| i I | Insert text |
| dd dw x | Delete text into a buffer (line, word, or character) |
| cc C | Change text |
| u U | Undo |
| yy Y | Yank (copy a line into buffer) |
| p P | Put yanked or deleted line down below or above the line |
| r R | Replace a letter or any amount of text on a line |

The emacs Built-In Editor. If using the emacs built-in editor, like vi, start at the command line. To start moving upward through the history file, press ^P. To move down, press ^N. Use emacs editing commands to change or correct text, then press Enter and the command will be re-executed. See Table 13.9.

## Table 13.9 emacs Commands

| Command | Function |
|---|---|
| Ctrl-P | Move up history file |
| Ctrl-N | Move down history file |
| Ctrl-B | Move backward one character |
| Ctrl-R | Search backward for string |
| Esc B | Move backward one word |
| Ctrl-F | Move forward one character |
| Esc F | Move forward one word |
| Ctrl-A | Move to the beginning of the line |
| Ctrl-E | Move to the end of the line |
| Esc < | Move to the first line of the history file |
| Esc > | Move to the last line of the history file |

## Table 13.9 emacs Commands (continued)

| Command | Function |
|---|---|
| Editing with emacs | |
| Ctrl-U | Delete the line |
| Ctrl-Y | Put the line back |
| Ctrl-K | Delete from cursor to the end line |
| Ctrl-D | Delete a letter |
| Esc D | Delete one word forward |
| Esc H | Delete one word backward |
| Esc space | Set a mark at cursor position |
| Ctrl-X Ctrl-X | Exchange cursor and mark |
| Ctrl-P Ctrl-Y | Push region from cursor to mark into a buffer (Ctrl-P) and put it down (Ctrl-Y) |

## FCEDIT and Editing Commands.

If the fc command is given the -e option followed by the name of a UNIX/Linux editor, that editor is invoked containing history commands selected from the history list; for example, fc -e vi -1 -3 will invoke the vi editor, create a temporary file in /tmp, with the last three commands from the history list in the vi buffer. The commands can be edited or commented out. (Preceding the command with a # will comment it.) If the user quits the editor, the commands will all be echoed and executed.⁶

If the editor name is not given, the value of the FCEDIT variable is used (typically set in the initialization files, either bash_profile or .profile), and the value of the EDITOR variable is used if FCEDIT is not set. When editing is complete, and you exit the editor, all of the edited commands are echoed and executed.

> 6. Whether the user saves and quits the editor, or simply quits the editor, the commands will all be executed, unless they are commented or deleted.

## EXAMPLE 13.36

```
1  $ FCEDIT=/bin/vi
2  $ pwd
3  $ fc
< Starts up the full screen vi editor with the pwd command on line 1 >
```

![](img/60a0b5d254bd6007403850f972cbfad8_834_0.png)

```
4  $ history
1 date
2 ls -l
3 echo "hello"
4 pwd

5  $ fc -3 -1    # Start vi, edit, write/quit, and execute
                  # last 3 commands.
```

## EXPLANATION

1 The FCEDIT variable can be assigned the pathname for any of the UNIX/Linux text editors you have on your system, such as vi, emacs, and so on. If not set, the vi editor is the default.

2 The pwd command is typed at the command line. It will be placed in the history file.

3 The fc command caused the editor (set in FCEDIT) to be invoked with the last command typed in the editor window. After the user writes and quits the editor, any commands typed there will be executed.

4 The history command lists recently typed commands.

5 The fc command is used to start up the editor with the last three commands from the history file in the editor's buffer.

## 13.6 Aliases

An alias is a bash user-defined abbreviation for a command. Aliases are useful if a command has a number of options and arguments or the syntax is difficult to remember. Aliases set at the command line are not inherited by subshells. Aliases are normally set in the .bashrc file. Because the .bashrc is executed when a new shell is started, any aliases set there will be reset for the new shell. Aliases may also be passed into shell scripts but will cause potential portability problems unless they are set directly within the script.

### 13.6.1 Listing Aliases

The alias built-in command lists all set aliases. The alias is printed first, followed by the real command or commands it represents.

## EXAMPLE 13.37

```
$ alias
alias cow='compress'
alias cpe='cp -i'
alias mroe='more'
alias mv='mv -i'
alias ls='ls --color=tty'
alias uc='uncompress'
```

## EXPLANATION

The alias command lists the alias (nickname) for the command and the real command the alias represents after the = sign.

### 13.6.2 Creating Aliases

The alias command is used to create an alias. The first argument is the name of the alias, the nickname for the command. The rest of the line consists of the command or commands that will be executed when the alias is executed. Bash aliases cannot take arguments (see "Defining Functions" on page 841). Multiple commands are separated by a semicolon, and commands containing spaces and metacharacters are surrounded by single quotes.

## EXAMPLE 13.38

```
1 $ alias m=more
2 $ alias mroe=more
3 $ alias lf='ls -alF'
4 $ alias r='fc -s'
```
