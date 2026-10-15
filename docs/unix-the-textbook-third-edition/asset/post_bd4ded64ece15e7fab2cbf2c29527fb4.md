
```
f. rm -f ~/courses/ece446/lab[1-6].c[c]
```

```
g. rm -r ~/NotNeededDirectory
```

```
h. rm -rf ~/NotNeededDirectory
```

```
i. rm -ri ~/NotNeededDirectory
```

11. Give a command for moving files lab1, lab2, and lab3 from the ~/courses/ece345 directory to a newlabs.ece345 directory in your home directory. If a file already exists in the destination directory, the command should prompt the user for confirmation.

12. Give a command to display the lines in the ~/personal/phones file that are not repeated.

13. Refer to In-Chapter Exercise 9. Give a sequence of commands to save the sequence of commands for the ed editor and use them to make sample and example the same files.

14. You have a file in your home directory called tryit&. Rename this file. What command did you use?

15. Give a command for displaying attributes of all the files starting with a string prog, followed by zero or more characters and ending with a string .c in the courses/ece345 directory in your home directory.

16. Refer to Problem 15. Give a command for file names with two English letters between prog and .c. Can you give another command line to accomplish the same task?

17. Give a command for displaying files gotcha and M*A*S*H one screenful at a time.

24. What is the difference between the tail -15 file1 and tail +15 file1 commands? Which of the following commands is equivalent to cat file1: tail -$ file, tail -1 file1, or tail +1 file1? Why?

25. What is the purpose of the more -n5 file1?

26. What are the differences between the more and less commands? Which of the two is more powerful and user friendly in your opinion and why?

27. Create a file in your current directory called f1. What is the inode number of the file? Move the file to your home directory and name it f1.moved. What is the inode number of the moved file? Move the moved file to the /tmp directory. What is the inode number of the /tmp/f1.moved file? Why are the inode numbers for f1 and f2 the same? Why is the inode number of /tmp/f1.moved different from f1 (or ~/f1.moved)?

## Advanced File Processing

## Objectives

- To explain file compression and how it can be performed
- To explain the sorting process and how files can be sorted
- To discuss searching for commands and files in the UNIX file structure
- To discuss the formation and use of regular expressions
- To describe searching files for expressions, strings, and patterns
- To describe how database-type operations of cutting and pasting fields in a file can be performed
- To discuss encoding and decoding of files
- To explain file encryption and decryption
- To cover the commands and primitives

```
>, ~, compress, crypt, crypto, cut, egrep, fgrep, find, grep, openssl, paste, pcat, sort, uncompress, uuencode, uudecode, whereis, which, zcat
```

## 7.1 INTRODUCTION

In this chapter, we describe some of the more advanced file-processing operations and show how they can be performed in UNIX. But before describing these operations, we discuss the important topic of regular expressions, which are a set of rules that can be used to specify one or more strings using a sequence of special text characters. While discussing the operations, we also describe the related shell commands and tools that make use of regular expressions. We also give examples to illustrate how these commands can be used to perform the required operations.

## 7.2 COMPRESSING FILES

Reduction in the size of a file is known as file compression, which has both space and time advantages. A compressed file takes less disk space to store, less time to transmit from one computer to another in a network or internet environment, and less time to copy. It takes time to compress a file, but if a file is to be copied or transmitted several times, the time spent compressing the file could be just a fraction of the total time saved. In addition, if the compressed file is to be stored on a secondary storage device (e.g., a disk) for a long time, the savings in disk space can be considerable. Another consequence of compression is that a compressed file reads as garbage. However, this is not a problem because the process is fully reversible and a compressed file can be converted back to its original form. If you can fully recover the original file from its compressed version, the compression is known as lossless compression. Lossless compression techniques are normally used for text files. There are lossy compression techniques too. These techniques are used to reduce the size of a file for storing, handling, and transmitting its content between computers on a network. Lossy compression techniques are normally used for image files such as JPEGs. In this chapter, we discuss tools for compressing and decompressing text and executable files. We also discuss commands for displaying and searching compressed files.

The UNIX operating system has many commands for compressing and decompressing files and for performing various operations on compressed files. These commands include the traditional UNIX commands for compressing and decompressing files, compress and uncompress, and the GNU tools g zexe (compress executable files), gzip (for compressing files), gunzip (for uncompressing files that were compressed with gzip), zcat (for displaying compressed files; gzcat does the same), gzcmp (for comparing compressed files), gzforce (for forcing the .gz extension onto compressed files so that gzip will not compress them twice), z more (for displaying compressed files one page at a time), and zgrep (the grep command for compressed files; it searches possibly compressed files for a regular expression). This section will primarily discuss file compression and decompression. Although the GNU tools (gzip and gunzip) are better than compress and uncompress commands, we discuss both sets of commands for completion.

### 7.2.1 The compress Command

The compress command reads contents of files that are passed to it as parameters, analyzes their contents for repeated patterns, and then substitutes a smaller number of characters for these patterns by using adaptive Lempel–Ziv coding. A compressed file’s contents are altogether different from the original file. The compressed file contains nonprintable characters, so displaying a compressed file on the screen shows a bunch of control characters, or garbage. The compress command saves the compressed file in a file that has the same name as the original file, with an extension .Z appended to it. The file has the same access permissions and modification date as the original file. The original file is removed from the file structure.

The following is a brief description of the compress command; the syntax of and options used in the uncompress command are exactly the same.
