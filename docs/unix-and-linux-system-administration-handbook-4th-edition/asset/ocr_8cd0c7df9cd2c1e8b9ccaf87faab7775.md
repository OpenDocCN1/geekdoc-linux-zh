Note that **ls** shows the control character as a question mark, which can be a bit deceptive.⁴ If you don’t remember that **?** is a shell pattern-matching character and try to **rm foo?bar**, you might potentially remove more than one file (although not in this example). -i is your friend!

To delete the most horribly named files, you may need to resort to **rm -i ?***.

Another option for removing files with squirrelly names is to use an alternative interface to the filesystem such as **emacs**’s dired mode or a visual tool such as Nautilus.

# Regular files

Regular files consist of a series of bytes; filesystems impose no structure on their contents. Text files, data files, executable programs, and shared libraries are all stored as regular files. Both sequential access and random access are allowed.

# Directories

A directory contains named references to other files. You can create directories with **mkdir** and delete them with **rmdir** if they are empty. You can delete non-empty directories with **rm -r**.

The special entries “.” and “..” refer to the directory itself and to its parent directory; they may not be removed. Since the root directory has no parent directory, the path “/../” is equivalent to the path “/.” (and both are equivalent to /).

A file’s name is stored within its parent directory, not with the file itself. In fact, more than one directory (or more than one entry in a single directory) can refer to a file at one time, and the references can have different names. Such an arrangement creates the illusion that a file exists in more than one place at the same time.

These additional references (“links,” or “hard links” to distinguish them from symbolic links, discussed below) are synonymous with the original file; as far as the filesystem is concerned, all links to the file are equivalent. The filesystem maintains a count of the number of links that point to each file and does not release the file’s data blocks until its last link has been deleted. Hard links cannot cross filesystem boundaries.

You create hard links with **ln** and remove them with **rm**. It’s easy to remember the syntax of ln if you keep in mind that it mirrors the syntax of cp. The command **cp oldfile newfile** creates a copy of **oldfile** called **newfile**, and **ln oldfile newfile** makes the named file an additional reference to **oldfile**. You can make hard links to directories as well as to flat files, but that’s less commonly done.

You can use **-l** to see how many links to a given file exist. See the example output on page 154 for some additional detail.

⁴. **ls -b** shows the special characters as octal numbers, which can be helpful if you need to identify them specifically. <Control-A> is 1 (\001 in octal), <Control-B> is 2, and so on.