
When creating and using hard links, there are a few important items to remember:

- The original file must exist before you issue the `ln` command.
- The second file listed in the `ln` command must *not* exist prior to issuing the command.
- An original file and its hard links share the same inode number.
- An original file and its hard links share the same data.
- An original file and any of its hard links can exist in different directories.
- An original file and its hard links must exist on the same filesystem.

## Constructing a Soft Link

Typically, a soft link file provides a pointer to a file that may reside on another filesystem. The two files do not share inode numbers because they do not point to the same data. Figure 3.3 illustrates the soft link relationship.

### FIGURE 3.3 Soft-link file relationship

![](img/c0a399aca0d18f8822d714ad0a173123_127_0.png)

To create a symbolic link, the `ln` command is used with the `-s` (or `--symbolic`) option. An example is shown in Listing 3.20.

### Listing 3.20: Using the `ln` command to create a soft link

```
$ touch OriginalSFile.txt
$
$ ls
OriginalSFile.txt
$
$ ln -s OriginalSFile.txt SoftLinkFile.txt
$
$ ls -i
2101456 OriginalSFile.txt 2101468 SoftLinkFile.txt
$
$ ls -og
total 0
-rw-rw-r--, 1 0 Aug 24 19:04 OriginalSFile.txt
lrwxrwxrwx. 1 17 Aug 24 19:04 SoftLinkFile.txt -> OriginalSFile.txt
$
```

Similar to a hard link, the original file must exist prior to issuing the `ln -s` command. The soft-linked file must not exist. It is created when the command is issued. In Listing 3.20, you can see via the `ls -i` command that soft-linked files do not share the same inode number, unlike hard-linked files. Also, soft-linked files do not experience a link count increase. The `ls -og` command shows this, and it also displays the soft-linked file’s pointer to the original file.

> **TIP**
> Sometimes you have a soft-linked file that points to another soft-linked file.
> If you want to quickly find the final file, use the `readlink -f` command and pass one of the soft-linked filenames as an argument to it. The `readlink` utility will display the final file’s name and directory location.

When creating and using soft links, keep a few things in mind:

- The original file must exist before you issue the `ln -s` command.
- The second file listed in the `ln -s` command must not exist prior to issuing the command.
- An original file and its soft links do not share the same inode number.
- An original file and its soft links do not share the same data.
- An original file and any of its soft links can exist in different directories.
- An original file and its soft links can exist in different filesystems.

> **WARNING**
> Stale links can be a serious security problem. A stale link, sometimes called a *dead link*, is when a soft link points to a file that was **deleted** or moved. The soft-linked file itself is not removed or updated. If a file with the original file’s name and location is created, the soft link now points to that new file. If a malicious file is put in the original file’s place, your server’s security could be compromised. Use symbolic links with caution and employ the `unlink` command if you need to remove a linked file.

File and directory links are easy to create. However, it is important that you understand the underlying structure of these links in order to use them properly.

## Reading Files

Linux systems contain many text files. They include configuration files, log files, data files, and so on. Understanding how to view these files is a basic but important skill. In the following sections, we’ll explore several utilities you can use to read text files.

## Reading Entire Text Files

The basic utility for viewing entire text files is the **concatenate (cat)** command. Though this tool’s primary purpose in life is to join together text files and display them, it is often used just to display a single small text file. To view a small text file, use the **cat** command with the basic syntax that follows:

```
cat [OPTION]… [FILE]…
```

The **cat** command is simple to use. You just enter the command followed by any text file you want to read, as shown in Listing 3.21.

### Listing 3.21: Using the cat command to display a file

```
$ cat numbers.txt
42
2A
52
0010 1010
*
$
```

The **cat** command simply spits out the entire text file to your screen. When you get your prompt back (shown as the $ in Listing 3.21), you know that the line above the prompt is the file’s last line.

![](img/c0a399aca0d18f8822d714ad0a173123_129_0.png)

> There is a handy new clone of the cat command called **bat**. Its developer calls it “cat with wings” because of the bat utility’s many additional features. You can read about its features at https://github.com/sharkdp/bat.

One cat command option that is useful is the -n (or --number) switch. Using this option will display line numbers along with the file text, as shown in Listing 3.22.

### Listing 3.22: Employing the cat -n command to display a file

```
$ cat -n numbers.txt
  1 42
  2 2A
  3 52
  4 0010 1010
  5 *
$
```

Another useful command to view entire text files is the **pr** command. Its original use was to format text files for printing. However, nowadays it is far more useful for displaying a file when you need some special formatting. To view a small text file, use the **pr** command with the basic syntax that follows:

```
pr [OPTION]… [FILE]…
```

The special formatting options are what set this command apart from simply using the cat command. Table 3.6 shows some useful pr utility options for displaying a file.

**TABLE 3.6** The pr command's useful file display options

| Short | Long | Description |
| :--- | :--- | :--- |
| -n | --columns=n | Display the file(s) in column format, using *n* columns. |
| -l n | --length=n | Change the default 66-line page length to *n* lines long. |
| -m | --merge | When displaying multiple files, display them in parallel, with one file in each column, and truncate the files' lines. |
| -s c | --separator=c | Change the default column separator from tab to *c*. |
| -t | --omit-header | Do not display any file header or trailers. |
| -w n | --width=n | Change the default 72-character page width to *n* characters wide. The -s option overrides this setting. |

To display one file, you need to use the page length option, -l (or --length), to shorten the page length. If you do not use this switch and have a very short file, the text will scroll off the screen. Also the -t (or --omit-header) option is useful if you only want to see what text is in the file. Listing 3.23 shows the pr command in action.

### Listing 3.23: Employing the pr command to display a file

```
$ pr -tl 15 numbers.txt
42
2A
52
0010 1010
 *
$
```

Where the pr utility really shines is displaying two short text files at the same time. You can quickly view the files side by side. In this case, it is useful to employ the -m (or --merge) option, as shown in Listing 3.24.

### Listing 3.24: Using the pr command to display two files

```
$ pr -mtl 15 numbers.txt random.txt
42 42
2A Flat Land
52 Schroedinger's Cat
0010 1010 0010 1010
* 0000 0010
$
```

![](img/c0a399aca0d18f8822d714ad0a173123_131_0.png)

If you want to display two files side by side and you do not care how sloppy the output is, you can use the paste command. Just like school paste, it will glue them together but not necessarily be pretty.

When a text file is larger than your output screen, if you use commands such as cat and pr, text may scroll off the screen. This can be annoying. Fortunately, there are several utilities that allow you to read portions of a text file, which are covered next.

## Reading Text File Portions

If you just want to read a single line from or a small portion of a file, it makes no sense to use the cat command. This is especially true if you are dealing with a large text file.

The grep utility can help you find a file line (or lines) that contain certain text strings. While this utility, covered in more detail later, is primarily used to search for text patterns within a file, it is also very useful in searching for a single string. The basic syntax for the grep command is as follows:

```
grep [OPTIONS] PATTERN [FILE...]
```

When searching for a particular text string, you use the string for PATTERN in the command's syntax and the file you are searching as FILE. Listing 3.25 shows an example of using the grep command.

### Listing 3.25: Using the grep command to find a file line

```
$ grep christine /etc/passwd
$
$ grep -i christine /etc/passwd
Christine:x:1001:1001::/home/Christine:/bin/bash
$
```

Be aware that the grep utility pays attention to case. If the string you enter does not match a string exactly (including case) within the file, the grep command will return nothing, as happened for the first command in Listing 3.25. If you employ the -i (or --ignore-case) switch, grep will search for any instance of the string disregarding case, as shown in Listing 3.25’s second command.
