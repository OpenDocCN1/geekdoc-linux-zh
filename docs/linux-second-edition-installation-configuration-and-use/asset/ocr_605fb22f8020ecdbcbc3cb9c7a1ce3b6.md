# DISPLAYING AND EDITING TEXT FILES 63

invisible. For this reason, this kind of name is often used for configuration files. To make it show these files as well, the additional option -a must be used.

Please note that Linux is case sensitive and distinguishes between upper and lower case letters in files. Thus, readme, Readme, and README are three different files. In the Linux standard file system, file names can be up to 255 characters long.

With cp you can copy files, with mv you can rename them, and with rm you can delete them. Use of wildcard characters is allowed; they work similarly but not exactly as DOS. For the most important difference is that * comprises only those files that have a dot in their file name. Be careful when using wildcards, particularly in combination with rm!; instead of rm, use the echo command, and all directories and files are displayed on screen (for example, .tex).

When looking for a file, it is best to use the command find -name name*. Linux will search the directory tree, starting with the current directory, for a file that contains name. If you change to the root directory / beforehand, the entire file system is searched. This can take a while, especially if a CD-ROM is linked.

> Wildcard characters and their function are described from page 87 onwards. A complete file management command reference is given in Chapter 14, starting on page 437.

# 3.2 Displaying and editing text files

To display a file on screen, you can use the commands cat, more, and less. cat corresponds to the DOS command TYPE and displays the file to the end without pausing. more and less allow you to view the text page by page. With less, you can move freely automatically when it reaches the text with your cursor keys (even backwards). more is terminated automatically when it reaches the end of the file, less must be terminated manually by entering Q more and less can also be used for pagewise display of other information.

```
user cat file      # displays the whole text file
user more file      # pairwise display of the file
user less file      # pairwise display of the file, also backwards
user ls -l | more # pairwise display of the current directory
```

If you use one of these three programs to display a file that does not contain text, but contains binary data, the terminal emulator may interpret such data as special characters and get confused. In this case, strange characters appear on the screen, because the character set mapping is no longer correct. Remedy: execute the reset command.