
@sf (WWW): ftp://ftp.wa.omron.co.jp/pub/unix-faq/docs
@sf (WWW): http://ds1.org/comp/tinyutils/

## 6.6.2 A Safe Way to Remove a File

Once a file is removed, it is permanently deleted and there is no command you can use to restore it; you cannot "undelete" it. (Although if you can unmount the filesystem that contained the file immediately after you deleted the file, a wizard might be able to help reconstruct the lost file by using grep to search the filesystem device file.)

A safer way to remove files is to use del, which is simply an alias to rm with the `-i` option. This specifies for rm to run in interactive mode and confirm the deletion of each file. It may be good practice to get in the habit of using del all the time, so that you don't make an accidental slip and rm an important file.

NOTE: Question 3.6 in the Unix FAQ (see `/usr/doc/FAQ/unix-faq-part3`) discusses this issue, and gives a shell script called can that you can use in place of rm---it puts files in a "trashcan" directory instead of removing them; you then periodically empty out the trashcan with rm.

## 6.7 Giving a File More than One Name

Links are special files that point to other files; when you act on a file that is a link, you act on the file it points to. There are two kinds of links: hard links and symbolic links. A hard link is another name for an existing file; there is no difference between the link and the original file. So if you make a hard link from file `foo` to file `bar`, and then remove file `bar`, file `foo` is also removed. Each file has at least one hard link, which is the original file name itself. Directories always have at least two hard links---the directory name itself (which appears in its parent directory) and the special file `.` inside the directory. Likewise, when you make a new subdirectory, the parent directory gains a new hard link for the special file `..` inside the new subdirectory.

A symbolic link (sometimes called a "symlink" or "soft link") passes most operations---such as reading and writing---to the file it points to, just as a hard link does. However, if you remove a symlink, you remove only the symlink itself, and not the original file.

Use ln ("link") to make links between files. Give as arguments the name of the source file to link from and the name of the new file to link to. By default, ln makes hard links.

- To create a hard link from `seattle` to `emerald-city`, type:

    ```
    $ ln seattle emerald-city RET
    ```

This command makes a hard link from an existing file, `seattle`, to a new file, `emerald-city`. You can read and edit file `emerald-city` just as you would `seattle`; any changes you make to `emerald-city` are also written to `seattle` (and vice versa). If you remove the file `emerald-city`, file `seattle` is also removed.

To create a symlink instead of a hard link, use the `-s` option.

- To create a symbolic link from `seattle` to `emerald-city`, type:

    ```
    $ ln -s seattle emerald-city RET
    ```

After running this command, you can read and edit `emerald-city`; any changes you make to `emerald-city` will be written to `seattle` (and vice versa). But if you remove the file `emerald-city`, the file `seattle` will not be removed.

## 6.8 Specifying File Names with Patterns

The shell provides a way to construct patterns, called file name expansions, that specify a group of files. You can use them when specifying file and directory names as arguments to any tool or application.

The following table lists the various file expansion characters and their meaning.

| CHARACTER | DESCRIPTION |
| --- | --- |
| * | The asterisk matches a series of zero or more characters, and is sometimes called the "wildcard" character. For example, * alone matches all file names, a* matches all file names that consist of an `a` character followed by zero or more characters, and a*b matches all file names that begin with an `a` character and end with a `b` character, with any (or no) characters in between. |
| ? | The question mark matches exactly one character. Therefore, ? alone matches all file names with exactly one character, ?? matches all file names with exactly two characters, and a? matches any file name that begins with an `a` character and has exactly one character following it. |
| [list] | Square brackets match one character in list. For example, [ab] matches exactly two file names: `a` and `b`. The pattern c[i o] matches `ci` and `co`, but no other file names. |
| ~ | The tilde character expands to your home directory. For example, if your username is joe and therefore your home directory is `/home/joe`, then `~` expands to `/home/joe`. You can follow the tilde with a path to specify a file in your home directory—for example, `~/work` expands to `/home/joe/work`. |
