
### -f
Don't split lines being displayed.

### -n
A command is issued as soon as a command letter is typed, rather than having to issue a new line character.

### **more**
Display all or parts of a file one screen at a time.

**Options**

- **-c**: Clear the screen before displaying the next page of the file.
- **-d**: Display a prompt at the bottom of the screen with brief instructions.
- **-f**: Wrap text to fit screen and judge page length accordingly.
- **-n**: The number of lines in the display window is set to n.
- **-s**: Squeeze multiple consecutive empty lines into one empty line.

### **head**
Provide only the first few lines of a file.

**Options**

- **-c**: The output is produced with a specified number of bytes.
- **-l**: The output is produced with a specified number of lines. This is the default.
- **-n count**: The number of bytes or lines is specified by *count*. You can also use *-count* to specify the number of bytes or lines, which is shown in the example. The default *count* is 10.

### tail
Provide the last few lines of a file.

**Options**

- **-number**: Specify number of blocks from the end of the file you wish to begin displaying.
- **-cnumber**: Specify number of characters from the end of the file you wish to begin displaying.
- **-nnumber**: Specify number of lines from the end of the file you wish to begin displaying. You can also specify a number or minus sign and number, as shown in the example, to specify the number of lines from the end of file to begin displaying.

### split

Some files are just too long. The file **listing** we earlier looked at may be more easily managed if split into multiple files. We can use the **split** command to make **listing** into files 25 lines long as shown in Figure 3-23.

```
$ ll listing
-rw------- 1 denise users        1430 Dec 19 16:30 listing
$
$ split -l 25 listing
$
$ ll x*
-rw------- 1 denise users          330 Dec 19 16:40 xaa
-rw------- 1 denise users          267 Dec 19 16:40 xab
-rw------- 1 denise users          268 Dec 19 16:40 xac
-rw------- 1 denise users          256 Dec 19 16:40 xad
-rw------- 1 denise users          274 Dec 19 16:40 xae
-rw------- 1 denise users           35 Dec 19 16:40 xaf
$ 
```

![](img/75f39fc91296b889c0653851accdfd46_180_0.png)

![](img/75f39fc91296b889c0653851accdfd46_181_0.png)

Note that the `split` command produced several files from **listing** called xaa, xab, and so on. The `-l` option is used to specify the number of lines in files produced by `split`. Here is a summary of the `split` command.

**split** - Split a file into multiple files.

**Options**

- **-l `line_count`**: Split the file into files with `line_count` lines per file.
- **-b n**: Split the file into files with n bytes per file.

## Manual Pages of Some Commands Used in Chapter 3

The following are the HP-UX manual pages for many of the commands used in the chapter. Commands often differ among UNIX variants, so you may find differences in the options or other areas for some commands, however; the following manual pages serve as an excellent reference.

## cat

![](img/75f39fc91296b889c0653851accdfd46_183_0.png)

**cat** - Concatenate files.

**NAME**

**cat** - concatenate, copy, and print files

**SYNOPSIS**

**cat** [-benrstuv] *file* ...

**DESCRIPTION**

**cat** reads each *file* in sequence and writes it on the standard output. Thus:

**cat** *file*

prints *file* on the default standard output device;

**cat** *file1* *file2* > *file3*

concatenates *file1* and *file2*, and places the result in *file3*.

If **-** appears as a *file* argument, **cat** uses standard input. To combine standard input and other files, use a combination of **-** and *file* arguments.

**Options**

**cat** recognizes the following options:

- **-b**: Omit line numbers from blank lines when **-n** option is specified. If this option is specified, the **-n** option is automatically selected.
- **-e**: Print a $ character at the end of each line (prior to the new-line). If this option is specified, the **-v** option is automatically selected.
- **-n**: Display output lines preceded by line numbers, numbered sequentially from 1.
- **-r**: Replace multiple consecutive empty lines with one empty line, so that there is never more than one empty line between lines containing characters.
- **-s**: Silent option. **cat** suppresses error messages about non-existent files, identical input and output, and write errors. Normally, input and output files cannot have identical names unless the *file* is a special file.
- **-t**: Print each tab character as ^I. If this option is specified, the **-v** option is automatically selected.
- **-u**: Do not buffer output (handle character-by-character). Normally, output is buffered.
- **-v**: Cause non-printing characters (with the exception of tabs, new-lines and form-feeds) to be printed visibly. Control characters are printed using the form ^X (Ctrl-X), and the DEL character (octal 0177) is printed as ^? (see ascii(5)). Single-byte control characters whose most significant bit is set, are printed using the form M-^x, where x is the character specified by the seven low order bits. All other non-printing characters are printed as M-x, where x is the character specified by the seven low order bits. This option is influenced by the LC CTYPE environment variable and its corresponding code set.

**EXTERNAL INFLUENCES**

**Environment Variables**

- LANG provides a default value for the internationalization variables that are unset or null. If LANG is unset or null, the default value of "C" (see lang(5)) is used. If any of the internationalization variables contains an invalid setting, cat will behave as if all internationalization variables are set to "C". See environ(5).
- LC_ALL If set to a non-empty string value, overrides the values of all the other internationalization variables.
- LC_CTYPE determines the interpretation of text as single and/or multi-byte characters, the classification of characters as printable, and the characters matched by character class expressions in regular expressions.
- LC_MESSAGES determines the locale that should be used to affect the format and contents of diagnostic messages written to standard error and informative messages written to standard output.
- NLSPATH determines the location of message catalogues for the processing of LC_MESSAGES.

**International Code Set Support**

Single- and multi-byte character code sets are supported.

**RETURN VALUE**

Exit values are:

- 0: Successful completion.
- >0: Error condition occurred.

**EXAMPLES**

To create a zero-length file, use any of the following:

```c
cat /dev/null > file
cp /dev/null file
touch file
```

The following prints ^I for all the occurrences of tab character in file1:

```c
cat -t file1
```

To suppress error messages about files that do not exist, use:

```c
cat -s file1 file2 file3 > file
```

If file2 does not exist, the above command concatenates file1 and file3 without reporting the error on file2. The result is the same if -s option is not used, except that cat displays the error message.

To view non-printable characters in file2, use:

```
cat -v file2
```

**WARNINGS**

Command formats such as:

```
cat file1 file2 > file1
```

overwrites the data in file1 before the concatenation begins, thus destroying the file. Therefore, be careful when using shell special characters.

**SEE ALSO**

cp(1), more(1), pg(1), pr(1), rm(1), ssp(1).

**STANDARDS CONFORMANCE**

cat: SVID2, SVID3, XPG2, XPG3, XPG4, POSIX.2

## cd

**cd** - Change working directory.

**NAME**

cd - change working directory

**SYNOPSIS**

cd [directory]

**DESCRIPTION**

If directory is not specified, the value of shell parameter HOME is used as the new working directory. If directory specifies a complete path starting with /, ., .., directory becomes the new working directory. If neither case applies, cd tries to find the designated directory relative to one of the paths specified by the CDPATH shell variable. CDPATH has the same syntax as, and similar semantics to, the PATH shell variable. cd must have execute (search) permission in directory.

cd exists only as a shell built-in command because a new process is created whenever a command is executed, making cd useless if written and processed as a normal system command. Moreover, different shells provide different implementations of cd as a built-in utility. Features of cd as described here may not be supported by all the shells. Refer to individual shell manual entries for differences.

If cd is called in a subshell or a separate utility execution environment such as:

```
find . -type d -exec cd {}; -exec foo {};
```

(which invokes foo on accessible directories)

cd does not affect the current directory of the caller's environment. Another usage of cd as a stand-alone command is to obtain the exit status of the command.

**EXTERNAL INFLUENCES**

**International Code Set Support**

Single- and multi-byte character code sets are supported.

**EXAMPLES**

Change the current working directory to the HOME directory from any location in the file system:

```
cd
```

Change to new current working directory foo residing in the current directory:

```
cd foo
```

![](img/75f39fc91296b889c0653851accdfd46_186_0.png)
