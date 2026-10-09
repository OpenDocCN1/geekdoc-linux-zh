+   • davis
+   • reports
+   • 2001
+   • acct_payable



When you share your files with users on other systems, you might need to make long filenames differ within the first few characters. Systems running DOS or older versions of Windows have an 8-character filename body length limit and a 3-character filename extension length limit. Some UNIX systems have a 14-character limit, and older Macintosh systems have a 31-character limit. If you keep filenames short, they are easy to type; later you can add extensions to them without exceeding the shorter limits imposed by some filesystems. The disadvantage of short filenames is that they are typically less descriptive than long filenames. See “stat: Displays Information About a File or Filesystem” on page 468 for a way to determine the maximum length of a filename on the local system.

Long filenames enable you to assign descriptive names to files. To help you select among files without typing entire filenames, shells support filename completion. For more information about this feature, see the “Filename completion” tip on page 224.



You can use uppercase and/or lowercase letters within filenames. Linux is case sensitive, so files named JANUARY, January, and january represent three distinct files.



Although Linux allows you to use spaces within filenames, it is a poor idea. Because a SPACE is a special character, you must quote it on a command line. Quoting a character on a command line can be difficult for a novice user and cumbersome for an experienced user. Use periods or underscores instead of SPACES: joe.05.04.26_new_stuff.

If you are working with a filename that includes a SPACE, such as a file from another operating system, you must quote the SPACE on the command line by preceding it with a backslash or by placing quotation marks on either side of the filename. The two following commands send the file named my_file to the printer.

```
$ lpr my\ file
$ lpr "my file"
```



A filename extension is the part of the filename that follows an embedded period. In the filenames listed in Table 6-1 on the next page, filename extensions help describe the contents of the file. Some programs, such as the C programming language compiler, default to specific filename extensions; in most cases, however, filename extensions are optional. Use extensions freely to make filenames easy to understand. If you like, you can use several periods within the same filename—for example, notes.4.10.54 or files.tar.gz.