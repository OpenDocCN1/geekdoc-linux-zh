
# Table 2-2: Internationalized Pattern-matching Characters

| Character | Action |
|---|---|
| [[::class:]] | A character class name enclosed in bracket-colon delimiters matches any of the set of characters in the named class. The supported classes are alpha, upper, lower, digit, alnum, xdigit, space, print, punct, graph, and cntrl. For example, the alpha character class name specifies that you want to match any alphabetic character (uppercase and lowercase) as defined by the current locale. If you are running an American-based locale, alpha matches any character in the alphabet (A-Z, a-z). |
| [[=char=]] | A character enclosed in bracket-equal delimiters matches any equivalence class character. An equivalence class is a set of collating elements that all sort to the same primary location. It is generally designed to deal with primary-secondary sorting; that is, for languages such as French that define groups of characters as sorting to the same primary location, and then having a tie-breaking, secondary sort. |

For more information on internationalized pattern-matching characters, see the grep(1) reference page. For more information on internationalization features, see Appendix C.

## 3
## Managing Files

This chapter describes how to manage files on your system. After completing this chapter, you will be able to:

- List files
- Display and print files
- Link files
- Copy, rename, and move files
- Compare and sort files
- Remove files from the system
- Determine file type

To learn about managing files, follow the examples in this chapter. Do each example in order so that the information on your screen is consistent with the information in this book.

Before you can work through the examples, you must be logged in and your login directory must contain the following three files created in Chapter 2: `file1`, `file2`, and `file3`. To produce a listing of the files in your login directory, enter the `ls` command, which is explained in Section 3.1. If you are using files with different names, make the appropriate substitutions as you work through the examples.

In the following examples, when you are asked to return to your login directory, enter the `cd` (change directory) command as follows:

```
```shell
$ cd
```
```

In the preceding example, the dollar sign ($) represents the shell prompt. Your shell prompt may vary.

In addition, before working on the examples in this chapter, create a subdirectory called `project` in your login directory. To do so, enter the following `mkdir` (make directory) command from your login directory:

```
```shell
$ mkdir project
```
```

For more information on the cd and mkdir commands, see Section 4.2 or the cd(1) reference page and Section 4.1 or the mkdir(1) reference page, respectively.

### 3.1 Listing Files (ls)

You can display a listing of the contents of one or more directories with the ls command. This command produces a list of the files and subdirectories (if any) in your current directory. You can also display other types of information, such as the contents of directories other than your current directory.

The format of the ls command is:

```
ls
```

The ls command has a number of options, called flags that enable you to display different types of information about the contents of a directory. Refer to Section 3.1.3 for information about these flags.

#### 3.1.1 Listing Contents of the Current Directory

To list the contents of your current directory, enter:

```
$ ls
```

Used without flags in this format, the ls command lists the names of the files and directories in your current directory:

```
$ ls
file1  file2  file3  project
$
```

You may also list portions of your current directory's contents by using the command format:

```
ls  filename
```

The filename entry can be the name of the file or a list of file names separated by spaces. You may also use pattern-matching characters to specify files. See Chapter 2 for information on pattern matching.

For example, to list the files whose names begin with the characters file, you would enter the following command:

```
$ ls file*
file1  file2  file3
$
```

#### 3.1.2 Listing Contents of Other Directories

To display a listing of the contents of a directory other than your current directory, use the following format:
