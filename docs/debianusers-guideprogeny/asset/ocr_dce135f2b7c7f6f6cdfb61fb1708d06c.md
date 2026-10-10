# The find Command

| Option | Action | Comments |
| :--- | :--- | :--- |
| -type ARGUMENT | Searches for types of files | Arguments include:
\n- d: Directory.
- l: Symbolic link.
- f: Regular file. |
| -user USER | Searches for files that belong to the user included in the command. | |

# Searching for Files From the Command Line Using the locate Command

The locate command searches a database for files. It is often the quickest way to find a file.

*Type: locate string. If you want to specify the database, add the -d PATH or --database=PATH option.*

# Searching for Text From the Command Line: Using grep Commands

Linux uses the grep command line tools to search for text in files. This family of tools contains three commands:

+   - **grep**: A general purpose search tool that uses text strings, sometimes with metacharacters. The grep command contains most of the functionality of the other tools, but has fewer options for customizing the search.

+   - **fgrep**: A specialized search tool for locating literal text strings - that is, text strings without metacharacters. Because fgrep uses literal text strings, it does not require you to remember any special characters in your search.