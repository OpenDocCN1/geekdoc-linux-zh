
# The find Command

| Option | Action | Comments |
|---|---|---|
| -amin ARGUMENT | Searches by minutes since files were accessed. | Arguments include:<br> - +NUMBER: More than the given number of minutes ago.<br> - -NUMBER: Less than the given number of minutes ago.<br> - NUMBER: Exactly the given number of minutes ago. |
| -atime ARGUMENT | Searches by days since files were accessed. | Arguments are:<br> - +NUMBER: More than the given number of days ago.<br> - -NUMBER: Less than the given number of days ago.<br> - NUMBER: Exactly the number of days ago. |
| -cmin ARGUMENT | Searches by minutes since files were changed. | Arguments include:<br> - +NUMBER: More than the given number of minutes ago.<br> - -NUMBER: Less than the given number of minutes ago.<br> - NUMBER: Exactly the given number of minutes ago. |
| -ctime ARGUMENT | Searches by the number of days since file attributes were changed. | Arguments are:<br> - +NUMBER: More than the given number of days ago.<br> - -NUMBER: Less than the given number of days ago.<br> - NUMBER: Exactly the number of days ago. |
| -follow | Traces symbolic links to original files. | |
| -group GROUP | Searches for files that belong to a particular group of users. | The group can be identified by name or by group ID. |
| -maxdepth NUMBER | Sets the maximum level of sub-directories to search. | |
| -mindepth NUMBER | Sets the minimum level of sub-directories to search. | |
| -name STRING | Searches for files that match the string. | Put a string in quotation marks to use shell metacharacters. |
| -newer FILE | Finds files newer than one included in the command. | |
| -perm PERMISSIONS | Searches with permissions in absolute mode. | |
| -type ARGUMENT | Searches for types of files. | Arguments include:<br> - d: Directory.<br> - l: Symbolic link.<br> - f: Regular file. |
| -user USER | Searches for files that belong to the user included in the command. | |

Type: find DIRECTORY OPTIONS ARGUMENT.

# Searching for Files From the Command Line Using the locate Command

The locate command searches a database for files. It is often the quickest way to find a file.

Type: locate string. If you want to specify the database, add the -d PATH or --database=PATH option.

# Searching for Text From the Command Line: Using grep Commands

Linux uses the grep command line tools to search for text in files. This family of tools contains three commands:

- **grep**: A general purpose search tool that uses text strings, sometimes with metacharacters. The grep command contains most of the functionality of the other tools, but has fewer options for customizing the search.
- **fgrep**: A specialized search tool for locating literal text strings - that is, text strings without metacharacters. Because fgrep uses literal text strings, it does not require you to remember any special characters in your search.
- **egrep**: A specialized search tool that uses metacharacters. The command uses more metacharacters than grep. In addition, the egrep command is often said to be the fastest of the three tools.

All three commands use a similar format. Type:

- grep OPTIONS STRING FILES.
- egrep OPTIONS STRING FILES.
- fgrep OPTIONS STRING FILES.

# Note

To use grep or egrep as fully as possible, you should familiarize yourself with metacharacters. See “Using Metacharacters With grep Commands,” page 189.

If you want to save your search results to a file or print them, use redirection operators. See “Redirecting Input and Output for Commands,” page 128.

# The grep, egrep, and fgrep Commands (Find Text)

| Option | Action | Comment |
| :--- | :--- | :--- |
| -e | Treats the string as an extended regular expression. | Used only with grep. Similar to using egrep. |
| -f | Treats strings as regular text. | Used only with grep. Similar to using fgrep. |
| -f FILE<br>--file=FILE | Searches using a text file containing a list of patterns to match. | Strings must be listed one per line in the file. |
| -i<br>--ignore-case | Ignores the distinction between upper and lower case letters. | If this option is not used, lower case letters are distinguished from upper case ones. |
| -l<br>--files-with-matches | Lists files with matches. | Individual lines are not listed. |
| -L<br>--files-without-match | Searches for files that do not match the string. | |
| -n<br>--line-number | Displays lines numbered. | |
| -C NUMBER<br>--context=NUMBER | Sets the number of lines to display before and after each match. | Sometimes referred to as “context.” |
| -q<br>--quiet | Stops at the first match. | Whether other matches are available is not listed. |
| -r<br>--recursive | Searches sub-directories. | |
| -v<br>--invert-match | Searches for lines that do not match the string. | |
| -x<br>--line-regexp | Displays lines that match the entire string. | |

# Using Metacharacters With grep Commands

Metacharacters are characters that can be used to set special conditions for searching. They are also known as wild cards. See “Using Special Symbols,” page 127.

Metacharacters are added to a text string. A text string that includes metacharacters is called a regular expression. Regular expressions are useful for finding variations in wording or in the positioning of the string on a line.

Metacharacters can be used with both grep and egrep. However, grep can use fewer metacharacters than egrep. Whenever you want to use metacharacters, egrep is usually the tool to use.

If you do not want to use any metacharacters at all, or do not have the characters memorized for use, use fgrep.

Metacharacters can be extremely powerful, especially when used in combination. However, when you are using search tools, little is likely to go wrong unless you combine a grep command with another one that makes changes to files.

# Note

> If you want to search for a character that is usually used as a metacharacter, place a backward slash (\) in front of it. For example, \? searches for a question mark, instead of any character.

Metacharacters are especially powerful when used together. For example:

- `^contacts$` searches for matches in which contacts is the only word on a line.
- `[cC]ontacts` matches contacts or Contacts.
- `^...$` searches for any line of three characters.
- `compan(ies)` searches for company or companies.
- `[A-Za-z]` searches for any upper or lowercase letter. Similarly, `[0-9A-Za-z]` searches for any number or any letter.

# Viewing Files From the Desktop

The desktop offers only limited choices for viewing files. For selective viewing of parts of files, use the command line instead. See “Viewing Files From the Command Line,” page 193.

To view a file from the desktop:

1. Open the GNOME Midnight Commander. Do one of the following:
    - From the workspace, select the Home directory launcher.
    - From the menu, select Programs > File Manager.
    
    In both cases, the GNOME Midnight Commander opens, displaying your home directory.

![](img/e36b94f8548b09d00212238f073b11d9_192_0.png)

2. Use the directory tree and the Back, Up, and Forward icons to display the directory you want.

3. Right click on the icon for the file that you want. A pop-up menu appears.

   - Open
   - Open with...
   - View
   - Edit
   - Copy...
   - Move to Trash
   - Delete
   - Move...
   - Symlink...
   - Properties...

4. Select **Open** or **Open With** from the menu. One of two things happens:
   
   If the file's type is associated with a program, selecting **Open** displays the file. See “Adding MIME Types,” page 163.
   
   or
   
   If the file's type is not associated, selecting **Open** or **Open With** displays a window to choose a viewer from.

![](img/e36b94f8548b09d00212238f073b11d9_193_0.png)
