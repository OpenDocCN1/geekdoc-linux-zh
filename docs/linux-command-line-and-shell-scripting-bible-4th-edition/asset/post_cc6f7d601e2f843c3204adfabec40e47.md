
[christine@localhost ~]$ cd ../../etc
[christine@localhost etc]$ pwd
/etc
[christine@localhost etc]$

Of course, in a case like this, you actually have to do more typing rather than just typing the absolute directory reference, `/etc`. Thus, use a relative directory reference only if it makes sense to do so.

> **NOTE**
>
> It’s helpful to have a long informative shell CLI prompt, as used in this chapter section. However, for clarity purposes, a simple `$` prompt is used in the rest of the book’s examples.

Now that you know how to traverse the directory system and confirm your present working directory, you can start to explore what’s contained within the various directories. The next section takes you through the process of looking at files within the directory structure.

## Listing Files and Directories

To see what files are available on the system, use the `list` command (`ls`). This section describes the `ls` command and options available to format the information it can display.

### Displaying a basic listing

The `ls` command at its most basic form displays the files and directories located in your current directory:

```
$ ls
 Desktop    Downloads   my_script   Public      test_file
 Documents  Music       Pictures    Templates   Videos
$
```

Notice that the `ls` command produces the listing in alphabetical order (in columns rather than rows). If you’re using a terminal emulator that supports color, the `ls` command may also show different types of entries in different colors. The `LS_COLORS` environment variable controls this feature. (Environment variables are covered in **Chapter 6**. Different Linux distributions set this environment variable depending on the capabilities of the terminal emulator.)

If you don't have a color terminal emulator, you can use the `-F` parameter with the `ls` command to easily distinguish files from directories. Using the `-F` parameter produces the following output:

```
$ ls -F
Desktop/   Downloads/  my_script*  Public/    test_file
Documents/ Music/      Pictures/   Templates/ Videos/
$
```

The `-F` parameter flags the directories with a forward slash (*/*), to help identify them in the listing. Similarly, it marks executable files (like the `my_script` file in the preceding code) with an asterisk (*), to help you more easily find files that can be run on the system.

The basic `ls` command can be somewhat misleading. It shows the files and directories contained in the current directory, but not necessarily all of them. Linux often uses *hidden files* to store configuration information. In Linux, hidden files are files with filenames starting with a period (.). These files don't appear in the default `ls` listing. Thus, they are called hidden files.

To display hidden files along with normal files and directories, use the `-a` parameter. Here is an example of using the `-a` parameter with the `ls` command:

```
$ ls -a
.  .bash_profile   Desktop  .ICEauthority
.. my_script       Templates  .bashrc   Documents  .local
.bash_history      Pictures test_file   .cache   Downloads  .mozilla   .pki
.bash_logout .config .esd_auth Music
Public
$
```

All the files beginning with a period, hidden files, are now shown. Notice that four files begin with `.bash`. These are hidden files that are used by the Bash shell environment and are covered in detail in Chapter 6.

The `-R` parameter is another option the `ls` command can use. Called the recursive option, it shows files that are contained within subdirectories in the current directory. If you have lots of subdirectories, this can be quite a long listing. Here's a simple example of what the -R parameter produces. The `-F` option was tacked on to help you see the file types:

```
$ ls -F -R
 .:
 Desktop/    Downloads/  my_script*  Public/     test_file
 Documents/  Music/      Pictures/   Templates/  Videos/
 
 ./Desktop:
 
 ./Documents:
 
 ./Downloads:
 
 ./Music:
 I LoveLinux.mp3*
 
 ./Pictures:
 
 ./Public:
 
 ./Templates:
 
 ./Videos:
 $
```

Notice that the `-R` parameter shows the contents of the current directory, which are the files from a user's home directory shown in earlier examples. It also shows each subdirectory in the user's home directory and their contents. The only subdirectory containing a file is the Music subdirectory, and it contains the executable file `ILoveLinux.mp3`.

> **TIP**

**Option parameters don't have to be entered separately as shown in the previous example: ls -F -R. They can often be combined as follows: ls -FR.**

In the previous example, there were no subdirectories within subdirectories. If there had been further subdirectories, the -R parameter would have continued to traverse those as well. As you can imagine, for large directory structures, this can become quite a long listing.

### Displaying a long listing

In the basic listings, the ls command doesn't produce much information about each file. For listing additional information, another popular parameter is -l. The -l parameter produces a long listing format, providing more information about each file in the directory:

```
$ ls -l
   total 8
   drwxr-xr-x.  2 christine christine     6 Feb 20 14:23 Desktop
   drwxr-xr-x.  2 christine christine     6 Feb 20 14:23 Documents
   drwxr-xr-x.  2 christine christine     6 Feb 20 14:23 Downloads
   drwxr-xr-x.  2 christine christine    28 Feb 29 15:42 Music
   -rwxrw-r--.  1 christine christine   74 Feb 29 15:49 my_script
   drwxr-xr-x.  2 christine christine     6 Feb 20 14:23 Pictures
   drwxr-xr-x.  2 christine christine     6 Feb 20 14:23 Public
   drwxr-xr-x.  2 christine christine     6 Feb 20 14:23 Templates
   -rw-rw-r--.  1 christine christine   74 Feb 29 15:50 test_file
   drwxr-xr-x.  2 christine christine     6 Feb 20 14:23 Videos
   $
```

The long listing format lists each file and directory on a single line. Along with the filename, the listing shows additional useful information. The first line in the output shows the total number of allocated blocks for the files within the directory (8). After that, each line contains the following information about each file (or directory):

- The file type — such as directory (d), file (-), linked file (l), character device (c), or block device (b)
- The file permissions (see Chapter 7)
- The number of file hard links (see the section “Linking Files” in this chapter).
- The file owner username
- The file primary group name
- The file byte size
- The last time the file was modified
- The filename or directory name

The -l parameter is a powerful tool to have. Armed with this parameter, you can see most of the information you need for any file or directory.

> **TIP**
>
> If you want to view the long listing for only one file, simply tack on the file's name to your `ls -l` command. However, if you want to see such a listing for a directory, and not its contents, you'll not only need to add its name to the command, but add the -d switch, as in: `ls -ld` Directory-Name.

The `ls` command has lots of parameters that can come in handy as you do file management. If you type `man ls` at the shell prompt, you see several pages of available parameters for you to use to modify the `ls` command output.

Don't forget that you can also combine many of the parameters. You can often find a parameter combination that not only displays the desired output, but is also easy to remember, such as `ls -aIf`.

## Filtering listing output

As you've seen in the examples, by default the `ls` command lists all the non-hidden directory files. Sometimes, this can be overkill, especially when you're just looking for information on a few files.

Fortunately, the `ls` command also provides a way for you to define a filter on the command line. It uses the filter to determine which files or directories it should display in the output.

Before using the filter command, let’s create some files to play with via the `touch` command (covered in the next section). If the file already exists, the command won’t hurt the file:

```
$ touch my_script my_scrypt my_file
$ touch fall fell fill full
$ ls
Desktop     Downloads   fell      full      my_file     my_script
Public      test_file
Documents   fall        fill      Music     my_scrypt   Pictures
Templates   Videos
$
```

The filter works as a simple text-matching string. Include the filter after any command line parameters you want to use:

```
$ ls -l my_script
-rwxrwr-r--. 1 christine christine 74 Feb 29 16:12 my_script
$
```

When you specify the name of a specific file as the filter, the `ls` command only shows that file’s information. Sometimes, you might not know the exact filename you’re looking for. The `ls` command also recognizes standard wildcard characters and uses them to match patterns within the filter:

- A question mark (?) to represent one character
- An asterisk (*) to represent any number of characters

The question mark can be used to replace exactly one character anywhere in the filter string. For example:

```
$ ls -l my_scr?pt
-rw-rw-r--. 1 christine christine 0 Feb 29 16:12 my_scrypt
-rwxwr-r--. 1 christine christine 74 Feb 29 16:12 my_script
$
```

The filter `my_scr?pt` matched two files in the directory. Similarly, the asterisk can be used to match zero or more characters:

```
$ ls -l my*
```
