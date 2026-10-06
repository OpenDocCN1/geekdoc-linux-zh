# Notes

The utility with the -l option shows how many hard links has a file. Refer to
"Links" on page 123.

If new-link is the name of an existing file, In does not create the link unless you
the --force option or answer yes when using the --interactive option.

You can use symbolic links to link across filesystems and create links to di-
irectories. When you use the -l command to list information about a symbolic
link, ls displays -> and the name of the linked-to file after the name of the link.

# Examples

The following command makes a link between memo2 in the /home/alex/literature
directory and the working directory. The file appears as memo2 (the simple-name of the existing file) in the working directory:

+   $ ln /home/alex/literature/memo2

The next command makes a link to the same file. Time this file appears as
new_memo in the working directory:

+   $ ln /home/alex/literature/memo2 new_memo

The following command makes a link that causes the file to appear in another
user's directory:

+   $ ln /home/alex/literature/memo2 /home/jenny/new_memo

You must write and execute access permission to the other user's directory for
this command to work. If you own the file, you can use chmod to give the other user
write access to the file.

The next command makes a symbolic link to an existing file, memo3, in the di-ectory /home/alex/literature. The symbolic link is in a different filesystem, /tmp.
The ls -l command shows the linked-to filename:

```
$ pwd
/home/alex/literature
$ ln -s memo3 /tmp/memo
$ ls -l /tmp/memo
lrwxrxrwx 1 alex 5 Jul 31 11:44 /tmp/memo -> memo3
```

The final example attempts to make a symbolic link named memo1 to the file
memo2. Because the file memo1 exists, in refuses to make the link. If you use the
--interactive option, it asks whether you want to replace the existing memo1 file with
symbolic link. If you enter y or yes, the link is made, and the old memo1 disappears:

```
$ ls -l memo1
-rw-r--r-- 1 alex group 224 Jul 31 14:48 memo1
-rw-r--r-- 1 alex group 753 Jul 31 14:49 memo2
$ ln --symbolic memo2 memo1
In: File exists
ln: replace 'memo1'? y
$ ls -l memo1
lrwxrxrwx 1 alex group 5 Jul 31 14:49 memo1 -> memo2
-rw-r--r-- 1 alex group 753 Jul 31 14:49 memo2
```