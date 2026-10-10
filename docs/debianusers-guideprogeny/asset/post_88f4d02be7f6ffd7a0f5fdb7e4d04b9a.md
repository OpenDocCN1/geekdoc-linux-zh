
Within a string, you can type in multiple words, or disable metacharacters (also known as wild cards). A string that uses metacharacters is referred to as a regular expression. See “Using Metacharacters or Wild Cards,” page 118.

If you use double straight quotation marks, all metacharacters are disabled except environment variables, such as $HOME.

Single straight quotation marks disable all special characters. In most cases, use single quotation marks.

Do not use true quotation marks (“ ”). True quotation marks may be a problem if you copy and paste from a word processor.

For example, if you wanted to search user jsmith’s home directory for a file that contained the phrase “business expenses,” you would use the grep command with the phrase as an argument: `grep 'business expenses' /home/jsmith/`.

## Using Metacharacters or Wild Cards

Metacharacters are characters that designate a range of choices. They are also called special characters or wild cards.

You may know the basic metacharacters from other operating systems:

- An asterisk (*) includes any number of characters.
- A question (?) mark includes any single character.

**Warning**

Metacharacters can be extremely powerful, especially when used in combination. Be careful about using them when you are deleting and copying files.

**Note**

If you want to search for a character that is usually used as a metacharacter, place a backward slash (\) in front of it. For example, \? searches for a question mark, instead of any character.

## Metacharacters or Wild Cards

| Metacharacter | Stands for |
| :--- | :--- |
| . | Any character except a new line marker. |
| ? | Any one character, or none. |
| [ ] | Any one of the enclosed characters. |
| * | Any number of characters, or none. |
| ^STRING | The string at the start of the line. |
| STRING$ | The string at the end of the line. |
| STRING+ | Match one or more of the characters in the string |
| STRING | Match a range of instances |
| (STRING \| STRING) | One of the strings. |

Metacharacters are especially powerful when used together. For example:

- `^contacts$` matches text in which `contacts` is the only word on a line.
- `[Cc]ontacts` matches `Contacts` or `contacts`.
- `^...5` searches for any line of three characters.
- `compan(y|ies)` searches for `company` or `companies`.
- `[A-Za-z]` searches for any upper or lowercase letter. Similarly, `[0-9A-Za-z]` searches for any number or any letter.

## Entering Multiple Commands

Separate multiple commands by a semi-colon.

For example, if you type `cd /backup;ls s*`, you move to the `/backup` directory (using `cd`), and list all files in the directory that start with `s`.

## Combining Commands

You can combine commands by typing them with the pipe character (`|`) between them. This technique is known as piping.

For example, if you type `ls|less`, you display the files of the current directory (`ls`) using the `less` command, which allows you to scroll back and forth in the list. This combination would be useful if you had a long list of files.

![](img/e36b94f8548b09d00212238f073b11d9_121_0.png)

**Warning**

Use piping carefully. Sometimes, it has unwanted or unexpected results.

## Running Programs in the Background

If you are using the X Window System, the command prompt is generally in its own window. As a result, you can easily do another task while a command is running. However, if you are using only the command line, you can run a command in the background, so that you can use the shell for another task while the command is running.

To run a command in the background, type `COMMAND &`.

## Stopping Commands from Running

Press Ctrl-C.

The command that is running stops. Then a new command prompt displays below the previous one.

## Navigating the Command Line

Linux systems store files in directories. The directories are arranged in a tree-like structure. At the top of the tree is the root directory (\/). Even directories on another partition are sub-directories of the root directory. See “Searching for Files and Text,” page 167.

Using a few basic commands, you can:

- Change directories.
- Read the contents of directories.
- Identify the type of entries in a directory.
- Find your current directory.
- Clear the screen.

## Changing directories

Type `cd` DIRECTORY.

Unless the directory you are changing to is a sub-directory of the current one, usually you should type the full path name to the directory.

To change to the directory immediately above the present one, type `cd ..` (two periods).

## Reading the Contents of Directories

Type `ls` OPTIONS DIRECTORY.

By carefully selecting your options, you can use the `ls` list command to help you locate files. For example, `-s` lists files in order of size, while `-t` lists files by when they were modified.

Another trick is to set an alias, so that typing `list` results in `ls -- color`, which prints files in different colors, depending on what kind they are. See “Creating an Alias,” page 126.

## The `ls` Command (List)

| Option | Action | Comments |
| :--- | :--- | :--- |
| `-a` | Includes hidden files in the list. | Most hidden files start with a period. |
| `--color` / `--colour` | Displays types of files in color. | |
| `-f` / `--classify` | Displays types of files using symbols. | Common symbols are: <br> - `/`: Directories. <br> - `*`: Executable files. <br> - `@`: Symbolic links. |
| `--full-time` | Prints complete file attributes. | |
| `-l` / `format=long` | Displays file attributes. | |
| `-L` / `--dereference` | Lists the files referenced by symbolic links instead of the links themselves. | See “Working With Symbolic Links,” page 218. |
| `-R` / `--recursive` | Includes sub-directories. | |
| `-S` / `sort=size` | Sorts files by size. | Largest files are displayed first. |
| `-t` / `--sort=time` | Displays files in the order in which they were modified. | The most recently modified files are displayed first. |
| `-X` / `--sort=extension` | Sorts by file extensions. | Not all files may have extensions. |
| `-x` / `--format=across` | Lists files in multiple columns. | |

## Identifying Types of Directory Listings

Type: `file` OPTIONS FILE.

To see the types of all the listings in a directory, type the directory name followed by the asterisk wild card. For example: `file /root/*`.

> **Note**
> The file command does not read compressed files or symbolic links unless the -z option is chosen.

Another way to identify directory listing is to use the `ls` command with the `-color` option. See “Reading the Contents of Directories,” page 121.

## The file Command (Identifies File Types)

| Option | Action | Comment |
| :--- | :--- | :--- |
| `-l` | Lists the files referenced by symbolic links, rather than the links themselves. | Traces the original file. |
| `-z` | Reads compressed files. | |

## Finding Your Current Location

Type `pwd`.

The current or working directory displays on the screen.

## Clearing the Screen

Type `clear`.

Only the screen display is affected. The command history is not.

## Using Command Line Shortcuts

Linux has several shortcuts for entering commands:

- Tab completion.
- History.
- Command pasting.
- Aliases.
- Abbreviating file paths.
- Redirecting inputs and outputs.
- Environment variables.

### Using Tab Completion

By pressing the Tab key, you can have the shell complete the command you are typing. You can also use Tab completion as a guide to commands if you are unsure of which command you want.

If only one command completes what you have typed, then the full command is entered automatically. However, you still need to add any options, arguments and files, and press the Enter key.

If more than one command completes what you typed, then a list of possible completions displays. You can use the list as a guide to commands. Or you can type another letter, press the Tab key, and display another list of completions.

For example, if you type `chg` then press the Tab key, the command `chgrp` is entered at the prompt. No other command completes `chg`.

On the other hand, if you type `cha`, you get the following list:

`chage` `chat` `chattr`

This time, these three commands complete what you have typed.

### Using Command History

The `.bash_history` file in your home directory lists all the commands that you have entered from the command line.

You can use this file to re-enter commands that you have already used. This ability is useful if you are doing repetitive work, or if you have made a mistake and want to correct it without re-typing.
