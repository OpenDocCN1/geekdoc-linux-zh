Previously when you looked at the output of the `ls -l` command, I mentioned that the character in column one designates the type of file. A file can be thought of as a collection of information referred to by a name. Linux views peripheral devices as files, enabling you to read and write to them the same as you do with any other type of file.

Types of files include

+   - Ordinary files, such as text or binary
+   - Directories
+   - Printers
+   - Hard disk
+   - Floppy disk
+   - CD-ROM

The `file` utility enables you to get information about the contents of a file without having to examine the file directly. The output classifies the file by type. Although `file` presents information on any file, this information is not always correct. The syntax for `file` is

```
```bash
file [options] filename
```
```

By default, the output of the `file` command displays the name of the file followed by a brief classification. To prevent listing the filename, use the `-b` option. A list of files to be examined can be passed to the `file` command by using the `-f` file list option.

`file` will attempt to examine compressed files if you use the `-z` option. A discussion of compressed files is presented later in this chapter.

The following is sample output from the `file` command

```
```bash
$ file letters dog shout
letters: directory
dog: ascii text
shout: executable
```
```

# **cat**

The `cat` (concatenate file) command can be used to create new files; however, it is primarily used to send the contents of one or more files to your display or other output device. `cat`'s functionality can be increased by using either `>` or `>>`.