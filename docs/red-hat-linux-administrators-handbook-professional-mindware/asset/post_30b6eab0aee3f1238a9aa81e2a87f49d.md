
![](img/f9ec99365f159bfe663f8ac29732663c_535_0.png)

## Caution

If multiple patches are available for a kernel, apply the patches in order. In other words, apply *patch01.gz* before you apply *patch02.gz*, and so on.

Alternatively, the script *patch-kernel* can be used to automate this process. Store the patch file(s) in the */usr/src* directory and run the following from the */usr/src* directory:

```bash
./linux/scripts/patch-kernel
```

After patching the kernel, follow the instructions for compiling and installing the new kernel, as discussed earlier.

Because the modern Linux kernel supports modules that can be automatically loaded and unloaded via the *kerneld* daemon, you might need to configure one or more parameters for these modules to work properly. You can use *kernelcfg* for such a job.

## Using kernelcfg

All the module configuration information is stored in */etc/conf.modules*. You can either modify this file manually or use the *kernelcfg* tool.

You can add, delete, or modify module configuration information using this interface. To understand how to configure a module, take a look at the */etc/conf.modules* file, which is what the *kernelcfg* tool manages.

To add a new module configuration, click the *Add* button and select the module name from the drop-down menu. Click **OK** to continue. If the module requires any arguments, add them in the next screen.

After you add the arguments and click **OK** in the argument entry window, the new module configuration appears in the main window. You can also edit or delete an existing module configuration by using the appropriate buttons available on the interface. After you finish making changes, restart the *kerneld* daemon by clicking the *Restart kerneld* button.

## Appendix A

### Common Commands

### General File and Directory Commands

This section reviews the file- and directory-specific commands that you are likely to use on a daily basis.

### cat

**Syntax:** `cat file [> [>>] [destination file]]`

The cat command displays the contents of a file to stdout. It is often helpful to examine the contents of a file by using the cat command. The argument that you pass to cat is the file that you want to view. To view the contents of a file called `myfile`, run:

```
cat myfile
```

cat can also merge existing multiple files into one:

```
cat name1 name2 name3 > allnames
```

This example combines the files `name1`, `name2`, and `name3` to produce the final file `allnames`. The order of the merge is established by the order in which the files are entered at the command line.

Using cat, you can append a file to another existing file. For instance, if you had forgotten to add names4 in the previous command, you could still produce the same results by executing:

```
cat names4 >> allnames
```

to append names4 to allnames.

### chmod

**Syntax:** `chmod [ -R ] *permission-mode*  *file or directory*`

The chmod command is used to change the permission mode of a file or directory. The permission mode is specified as a three- or four-digit octal number. For example:

```
chmod 755 myscript.pl
```

changes the permission of myscript.pl script to 755 (rwxr-xr-x), which allows the file owner to read, write, and execute and allows only read and execute privileges for everyone else. As another example:

```
chmod -R 744 public_html
```

changes the permissions of the public_html directory and all of its contents (files and subdirectories) to 744 (rwxr-r--), which is a typical permission setting for personal Web directories that are accessed using http://server/~username URLs under Apache server. The -R option tells chmod to recursively change permissions for all the files and directories under the named directory.

### chown

**Syntax:** `chown [ -fhr ] *Owner* [ : *Group* ] [ *File* ... ] [ *Directory* ... ]`

The chown command changes the owner of the file specified by the File parameter to the user specified by the Owner parameter. The value of the Owner parameter can be a user ID or a login name found in the /etc/passwd file. Optionally, a group can also be specified. The value of the Group parameter can be a group ID or a group name found in the /etc/group file.

Only the root user can change the owner of a file. You can change the group of a file only if you are a root user or own the file. If you own the file but are not a root user, you can change the group only to a group of which you are a member. Table A-1 lists and describes the chown options.

### Table A-1 _chown_ Options

| Option | Description |
| :--- | :--- |
| `-f` | Suppresses all error messages except usage messages. |
| `-h` | Changes the ownership of an encountered symbolic link but not that of the file or directory pointed to by the symbolic link. |
| `-R` | Descends directories recursively, changing the ownership for each file. When a symbolic link is encountered and the link points to a directory, the ownership of that directory is changed but the directory is not further traversed. |

The following example changes the existing owner of the file to another user:

```
chown bert hisfile.txt
```

### clear

**Syntax:** `clear`

The clear command clears your terminal and returns the command-line prompt to the top of the screen. This command works properly only when an environment variable called TERM is set to an appropriate terminal type. Typically, the terminal type is vt100. If the clear command does not work, use your shell's set command to set the term. For example, to set TERM for a tcsh shell session, use:

```
set TERM = vt100
```

### cmp

**Syntax:** `cmp [ -ls ] file1 file2`

The cmp command compares the contents of two files. If no differences exist within the two files, cmp is silent, by default.

To demonstrate, `file1.txt` contains:

```
this is file 1
the quick brown fox jumps over the lazy dog.
```

and `file2.txt` contains:

```
this is file 2
the quick brown fox jumps over the lazy dog.
```

The only difference between the two files is the first line, last character. In one file, the character is `1`, while the other file has `2`:

```
cmp file1.txt file2.txt
file1.txt file2.txt differ: char 14, line 1
```

The results of `cmp` correctly identify character 14, line 1 as the unequal character between the two files. The `-l` option will print the byte number and the differing byte values for each of the files:

```
cmp -l file1.txt file2.txt
14 61 62
```

The results of the preceding example show that byte 14 is different between the two files, with the first file having an octal 61 and the second file having an octal 62 at that location.

Finally, the `-s` option will display nothing. The `-s` option returns only an exit status indicating the similarities between the files. A 0 (zero) is returned if the files are identical. A 1 is returned if the files are different. A number greater than 1 is returned when an error has occurred. By the way, you might want to look at the `diff` and `uniq` commands if `cmp` is not what you are looking for.

### cp

**Syntax:** `cp [-R] source file or directory file or directory`

Use the `cp` command to make an exact copy of a file. The `cp` command requires at least two arguments. The first argument is the file you want to copy, and the second argument is the location or filename of the file. If the second argument is an existing directory, cp will copy the source file into the directory with the target file's name.

```
cp main.c main.c.bak
```

The preceding example will copy the existing file main.c and create a new file called main.c.bak in the same directory. These two documents will be identical, bit per bit.

### cut

**Syntax:** `[ -cdf list ] *file*`

The cut command extracts columns of data. The data can be in bytes, characters, or fields from each line in a file. For instance, a file called names contains information about a group of people. Each line contains data pertaining to one person:

```
Fast    Freddy:Sacramento:CA:111-111-1111
Joe     Smoe:Los Angeles:CA:222-222-2222
Drake   Snake:San Francisco:CA:333-333-3333
Bill    Steal:New York:NY:444-444-4444
```

To list the names and telephone numbers of all the individuals in the file, the options -f and -d should suffice:

```
cut -f 1,4 -d : names
```

```
Fast    Freddy:111-111-1111
Joe     Smoe:222-222-2222
Drake   Snake:333-333-3333
Bill    Steal:444-444-4444
```

The -f list option specifies the fields you elect to display. Each field is defined by the -d options. In the preceding example, -d : indicates that each field is separated by a colon. Using 1 as the field delimiter makes fields 1 and 4 the name and phone number fields.
