
## Chapter 1: Getting started with GNU/Linux

### Section 1.1: Useful shortcuts

#### Using The Terminal

> The examples in this document assume that you are using a POSIX-compliant (such as **bash**, **sh**, **zsh**, **ksh**) shell.

Large portions of GNU/Linux functionality are achieved using the terminal. Most distributions of Linux include terminal emulators that allow users to interact with a shell from their desktop environment. A shell is a command-line interpreter that executes user inputted commands. **Bash** (Bourne Again Shell) is a common default shell among many Linux distributions and is the default shell for macOS.

These shortcuts will work if you are using **Bash** with the *emacs* keybindings (set by default):

#### Open terminal

- `Ctrl + Alt + T` or `Super + T`

#### Cursor movement

- `Ctrl + A` Go to the beginning of the line you are currently typing on.
- `Ctrl + E` Go to the end of the line you are currently typing on.
- `Ctrl + XX` Move between the beginning of the line and the current position of the cursor.
- `Alt + F` Move cursor forward one word on the current line.
- `Alt + B` Move cursor backward one word on the current line.
- `Ctrl + F` Move cursor forward one character on the current line.
- `Ctrl + B` Move cursor backward one character on the current line.

#### Text manipulation

- `Ctrl + U` Cut the line from the current position to the beginning of the line, adding it to the clipboard. If you are at the end of the line, cut the entire line.
- `Ctrl + K` Cut the line from the current position to the end of the line, adding it to the clipboard. If you are at the beginning of the line, cut the entire line.
- `Ctrl + W` Delete the word before the cursor, adding it to the clipboard.
- `Ctrl + Y` Paste the last thing from the clipboard that you cut recently (undo the last delete at the **current** cursor position).
- `Alt + T` Swap the last two words before the cursor.
- `Alt + L` Make lowercase from cursor to end of word.
- `Alt + U` Make uppercase from cursor to end of word.
- `Alt + C` Capitalize to end of word starting at cursor (whole word if cursor is at the beginning of word).
- `Alt + D` Delete to end of word starting at cursor (whole word if cursor is at the beginning of word).
- `Alt + .` Prints the last word written in previous command.
- `Ctrl + T` Swap the last two characters before the cursor.

#### History access

- `Ctrl + R` Lets you search through previously used commands.
- `Ctrl + G` Leave history searching mode without running a command.
- `Ctrl + J` Lets you copy current matched command to command line without running it, allowing you to make modifications before running the command.
- `Alt + R` Revert any changes to a command you've pulled from your history, if you've edited it.
- `Ctrl + P` Shows last executed command, i.e. walk back through the command history (Similar to up arrow).
- `Ctrl + N` Shows next executed command, i.e. walk forward through the command history (Similar to down arrow).

#### Terminal control

- `Ctrl + L` Clears the screen, similar to the clear command.
- `Ctrl + S` Stop all output to the screen. This is useful when running commands with lots of long output. But this doesn't stop the running command.
- `Ctrl + Q` Resume output to the screen after stopping it with Ctrl+S.
- `Ctrl + C` End currently running process and return the prompt.
- `Ctrl + D` Log out of the current shell session, similar to the exit or logout command. In some commands, acts as End of File signal to indicate that a file end has been reached.
- `Ctrl + Z` Suspends (pause) currently running foreground process, which returns shell prompt. You can then use bg command allowing that process to run in the background. To again bring that process to foreground, use fg command. To view all background processes, use jobs command.
- `Tab` Auto-complete files and directory names.
- `Tab Tab` Shows all possibilities, when typed characters doesn't uniquely match to a file or directory name.

#### Special characters

- `Ctrl + H` Same as Backspace.
- `Ctrl + J` Same as Return (historically Line Feed).
- `Ctrl + M` Same as Return (historically Carriage Return).
- `Ctrl + I` Same as Tab.
- `Ctrl + G` Bell Character.
- `Ctrl + @` Null Character.
- `Esc` Deadkey equivalent to the `Alt` modifier.

#### Close Terminal

- `Ctrl + Shift + W` To close terminal tab.
- `Ctrl + Shift + Q` To close entire terminal.

In Linux `..` represents the parent directory and `.` represents the current directory.

Therefore, if the current directory is `/home/user/somedir`, then `cd ../somedir` will not change the working directory.

The table below lists some of the most used file management commands

#### Directory navigation

| Command | Utility |
| :--- | :--- |
| `pwd` | Get the full path of the current working directory. |
| `cd -` | Navigate to the last directory you were working in. |
| `cd ~` or just `cd` | Navigate to the current user's home directory. |
| `cd ..` | Go to the parent directory of current directory (mind the space between `cd` and `..`). |

#### Listing files inside a directory

| Command | Utility |
| :--- | :--- |
| `ls -l` | List the files and directories in the current directory in long (table) format (It is recommended to use `-l` with `ls` for better readability). |
| `ls -ld dir-name` | List information about the directory `dir-name` instead of its contents. |
| `ls -a` | List all the files including the hidden ones (File names starting with a `.` are hidden files in Linux). |
| `ls -F` | Appends a symbol at the end of a file name to indicate its type (`*` means executable, `/` means directory, `@` means symbolic link, `=` means socket, `\|` means named pipe, `>` means door). |
| `ls -lt` | List the files sorted by last modified time with most recently modified files showing at the top (remember `-l` option provides the long format which has better readability). |
| `ls -lh` | List the file sizes in human readable format. |
| `ls -lR` | Shows all subdirectories recursively. |
| `tree` | Will generate a tree representation of the file system starting from the current directory. |

#### File/directory create, copy and remove

| Command | Utility |
| :--- | :--- |
| `cp -p source destination` | Will copy the file from `source` to `destination`. `-p` stands for preservation. It preserves the original attributes of file while copying like file owner, timestamp, group, permissions etc. |
| `cp -R source_dir destination_dir` | Will copy source directory to specified destination recursively. |
| `mv file1 file2` | In Linux there is no `rename` command as such. Hence `mv` moves/renames the file1 to file2. |
| `rm -i filename` | Asks you before every file removal for confirmation. **IF YOU ARE A NEW USER TO LINUX COMMAND LINE, YOU SHOULD ALWAYS USE `rm -i`.** You can specify multiple files. |
| `rm -R dir-name` | Will remove the directory `dir-name` recursively. |
| `rm -rf dir-name` | Will remove the directory `dir-name` recursively, ignoring non-existent files and will never prompt for anything. **BE CAREFUL USING THIS COMMAND!** You can specify multiple directories. |
| `rmdir dir-name` | Will remove the directory `dir-name`, if it's empty. This command can only remove empty directories. |
| `mkdir dir-name` | Create a directory `dir-name`. |
| `mkdir -p dir-name/dir-name` | Create a directory hierarchy. Create parent directories as needed, if they don't exist. You can specify multiple directories. |
| `touch filename` | Create a file `filename`, if it doesn't exist, otherwise change the timestamp of the file to current time. |

#### File/directory permissions and groups

| Command | Utility |
