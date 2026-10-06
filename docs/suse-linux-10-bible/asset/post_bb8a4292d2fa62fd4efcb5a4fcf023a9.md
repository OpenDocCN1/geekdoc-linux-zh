
# Chapter 2 ✦ Linux Fundamentals 57

- cp -a docs.bak -Recursively copies the directory docs beneath the current directory to a new directory docs.bak, while preserving file attributes and copying all files including hidden files whose names start with a d. The -a option implies the -r option, as a convenience.
- cp -i - By default, if you copy a file to a location where a file of the same name exists, the old file will be silently overwritten. The -i option makes the command interactive; in other words it asks before overwriting.
- cp -v - With the (verbose) option, the cp command will tell you what it is doing. A-many Linux commands have a -v option with the same meaning.

## Moving and Renaming Files

The mv (move) command has the both of "move" and of "rename." In the first example that follows, the file awhile will be renamed to the name bfile. In the second example, the file awhile in the current directory will be moved to the directory /tmp.

- mv awhile bfile - Renames the existing file awhile with the new name bfile
- mv awhile /tmp - Moves the file awhile in the current directory to /tmp

## Deleting Files and Directories

The rm (remove) command enables you to delete files and directories. Be warned: the rm is a dangerous command. It doesn't really offer you a second chance. When files are deleted, they're gone. You can use rm -i in the last example that follows. That gives you a second chance to think about it, but as soon as you agree, once again, the file is gone.

> Some people like to create an alias (Chapter 14) that makes the rm command rm -i. We would advise at least to be careful about this: it will lull you into a false sense of security, and when you're working on a system that has not been made, you may regret it.

Doug Gwyn, a well-known Internet personality, once said, "Unix was never designed to keep people from doing stupid things that policy would also keep them from clever things." You can, of course, use rm to delete every file on your system as simply as this: rm -rf /. (You have to be logged in as a user, such as the root user, who has the privileges to do this, but you get the idea.) Some better examples of using the rm command in daily use are:

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_101_0.png)

rm afile — Removes the file afile.
rm * — Removes all (nonhidden) files in the current directory. The rm command will not remove directories unless you specify the -r (recursive) option.
rm -rf doomed — Removes the directory doomed and everything in it.
rm -i a * — Removes all files with names beginning with a in the current directory, asking for confirmation each time.

## Changing Directories

You can use cd (change directory) command to change directories:

- cd — Changes to your home directory
- cd /tmp — Changes to the directory /tmp

On Linux systems, your prompt will tell you what directory you're in (depending on the setting you've used for the PS1 environment variable). However, if you explicitly need to know what directory you're in, you can use the pwd command to identify the working directory for the current process (process working directory, hence pwd).

## Making Directories

You can use the mkdir (make directory) command to make directories for examples:

- mkdir photos — Makes a directory called photos within the current directory.
- mkdir -p this/this/another — Makes the nested subdirectories within the current directory.

## Removing Directories

The command rmdir will remove a directory that is empty.

## Making Links to Files or Directories

In Linux, you can use the ln (link) command to make links to a file or directory. A file can have any number of “hard” links to it. Effectively, if you create a file called afile, and make a link to it called bfile, there are now two names for the same file. If you edit afile, the changes you've made will be in bfile. But if you delete afile, bfile will still exist; it will disappear when there are no links left to it. Hard links can be made only on the same filesystem — you can't create a hard link to a file on another partition because the link operates at the filesystem level, referring to the actual filesystem data structure that holds information about the file. You can create a hard link only to a file, not to a directory.

You can also create a symbolic link to a file. A symbolic link is a special kind of file that redirects usage of the link to the original file. This is somewhat similar to the use of "shortcuts" in Windows. You can also create symbolic links to directories, which can be very useful if you frequently use a subdirectory that is hidden several levels below your home directory. In the example that follows, you will end up with a symbolic link `useful` in the current directory. Thus, the command `cd useful` will have the same effect as `cd docs/linux/suse/useful/.`.

- -s file Makes a "hard" link to file called file
- -s afile Makes a symbolic link to file called linkfile
- -s docs/linux/suse/useful — Makes a symbolic link to the named directory in the current directory

## Concatenating Files

The command `cat` (concatenate) displays files to standard output. If you want to view a file, the easiest thing to do is cat. If you want to combine two files into one, you need to cat them and redirect to a new file. The name of cat command comes from the fact that it allows you to see more of a file at a time. The name of tac command comes from the fact that it displays files in reverse order, starting with the last line and ending with the first. The cat command has a sense of humor. The name of tac command is because it is cat spelled backwards.

## Searching Files with grep

The grep (global regular expression print) command is a very useful tool for finding stuff in files. It can do much more than the examples follow that this pattern indicate. Beyond simply searching for text, it can search for regular expressions, and regular expressions are a subject for a book in themselves.

When administering a system, you often need to look for lines in a file that contain a string. In the first example follows, you simply find the lines in the file that contain the string bible. The examples with tail are examples of piping the output from one command to another: very powerful concept that was also introduced in the section “Advanced Shell Features,” earlier in this chapter. In the first case, you get the output from the tail command, and you just select the lines that contain 404. In the second, select the lines that do not include the string googlebot; the -v option indicates “not.” In the example, the “symbol represents the start of a line, so you see only the lines that do not start with the
