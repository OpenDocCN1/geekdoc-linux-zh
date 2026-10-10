# ## Searching From the Command Line

The Linux command line includes many tools for locating files or informa-tion in them. These tools can be divided into two main categories:

+   - File-Locating Tool: `find`, `locate`.

+   - Text-Locating Tools: `grep`, `egrep`, and `fgrep`.

Some of these commands, including `grep`, `egrep` and `find` can use variable text patterns (metacharacters or regular expressions) to extend their search abili-ties. See "Using Metacharacters or Wild Cards," page 118.

# ## Searching for Files: Using the find Command

The basic tool for finding files is `find`. The `find` command is useful for locating files by their attributes or by their position in the directory tree.

You can search by a wide variety of criteria, including:

+   - When the file was last accessed.

+   - When the file was last changed.

+   - The file's owner or the owner's group.

+   - A text string, including one that uses metacharacters. see "Using Meta-characters or Wild Cards," page 118.

+   - The type of file.

+   - The file's age relative to another file.

+   - The file's permissions.

Usually, `find` starts with the current directory, then searches its sub-directo-ries. However, you can specify the starting directory.

You can also specify how many levels of sub-directories down to search.