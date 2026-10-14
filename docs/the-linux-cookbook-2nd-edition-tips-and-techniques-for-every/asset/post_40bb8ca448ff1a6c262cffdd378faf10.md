
### METHOD #2

When a file name begins with a control character or other strange character, you can specify the file name with a file name pattern that uniquely identifies it (see Recipe 5.8 [Specifying File Names with Patterns], page 153, for tips on building file name patterns). Use the -i option to verify the deletion first.

⇒ To delete the file ^Acat in a directory that also contains the files cat and dog, type:

```
$ rm -i ?cat RET
rm: remove '^Acat'? y RET
$
```

In the preceding example, the expansion pattern "?cat" matches the file ^Acat and no other files in the directory. The -i option was used because, in some cases, no unique pattern can be made for a file—for example, if this directory also contained a file called 1cat, the preceding rm command in the example would also attempt to remove it; with the -i option, you can answer n to it.

### METHOD #3

The two previous methods won’t work with a file that begins with a hyphen character, because rm interprets such a file name as an option; to remove a file like that, use the -- option—it specifies that what follows are arguments and not options.

⇒ To remove the file -cat from the current directory, type:

```
$ rm -- -cat RET
```

### 5.6.2 Removing Files Interactively

Once a file is removed, it is permanently deleted and there is no command you can use to restore it; you cannot "undelete" it. (However, if you can unmount the filesystem that contained the file immediately after you delete the file, a wizard might be able to help reconstruct the lost file by using grep to search the filesystem device file.)

A safer way to remove files is to use rm with the -i option, which specifies that rm run in interactive mode, where it will ask you to confirm the deletion of each file.

⇒ To interactively remove the files in the ~/tmp directory, type:

```
$ rm -i ~/tmp RET
```

In the preceding example, rm will prompt for confirmation before deleting any file in ~/tmp.

You might consider making an alias word for rm with the -i option, such as del, and get in the habit of using this word in place of rm (see Recipe 3.6.1 [Calling a Command by Some Other Name], page 83).

You can get the same effect as an alias by making the following two-line shell script, which you might write to a file called del and put in your personal bin directory (see Recipe A.3.4 [Installing a Shell Script], page 708, and Recipe C.1 [Using a Directory for Personal Binaries], page 727):

```
#!/bin/sh
/bin/rm -i $*
```

NOTES: Question 3.6 in the UNIX FAQ⁴ discusses this issue and gives a shell script called can that you can use in place of rm—it puts files in a “trash-can” directory instead of removing them; you then periodically empty out the trashcan with rm.

### 5.6.3 Removing Files without Verification

If a file is write-protected, rm will always ask you to verify its removal first, should you try to remove it. When you have a lot of files to remove, this is cumbersome. In this case, use yes to pipe an automatic “y” answer to rm with the -R option (see Recipe 3.1.10 [Automatically Answering a Command Prompt], page 65).

⇒ To remove the scrap directory and all its contents, including any write-protected files, type:

```
$ yes | rm -R scrap RET
```

NOTES: This is a dangerous operation! This command will permanently remove all files and directories you give it, so be certain you want them removed before you run it!

⁴ See the file /usr/doc/FAQ/unix-faq-part3, or on the Web: http://www.faqs.org/faqs/unix-faq/faq/.

## 5.7 Giving a File More Than One Name

*Links* are special files that point to other files; when you act on a file that is a link, you act on the file it points to. There are two kinds of links: symbolic links and hard links.

A *symbolic link* (sometimes called a “symlink” or “soft link”) passes most operations—such as reading and writing—to the file it points to. Symlinks are identified in file listings with an “l” in the first character of the first column, and, by default, are output as cyan in color listings.

If you remove a symlink, you remove only the symlink itself, and *not* the original file. However, if you remove the original file, and replace it with some other file, the symbolic link will point to the contents of the new file. You can make a symlink of a directory, and you can make symlinks across filesystems (see Chapter 24 [Disk Storage], page 501).

A *hard link* is another name for an existing file, and is indistinguishable from the file it is linked from. If you alter a file, any hard links to it are also altered; and conversely, altering any hard link will also alter the original file plus any other hard links it may have. So if you make a hard link from file `foo` to file `bar`, and then alter the file `bar`, file `foo` is equally altered.

So where a symlink points to the file it links to, a hard link is another instance of the file. If you change the original file, all of the hard links are also changed. If you change any of the hard links, the original file and all other hard links are all changed. But if you *remove* the original file, any hard links will still contain the contents that the original did.

Unlike symlinks, you cannot make a hard link to a directory, and you cannot make a hard link across filesystems.

Each file on the system has at least one hard link, which is the original file name itself. Directories always have at least *two* hard links—the directory name itself (which appears in its parent directory) and the special file `.` inside the directory. Likewise, when you make a new subdirectory, the parent directory gains a new hard link for the special file `..` inside the new subdirectory.

If you remove a hard link, you will not remove the file it is linked to, nor any other hard links that point to it; conversely, you will not remove any of a file’s hard links by removing the file itself.

### METHOD #1

Use `ln` (“link”) to make a link to a file. Give as arguments the name of the existing file to link to and the name to use for the link. By default, `ln` makes hard links.
