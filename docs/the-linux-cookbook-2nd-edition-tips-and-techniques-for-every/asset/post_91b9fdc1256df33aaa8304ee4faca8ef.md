/usr/src Program source code for software compiled on the system.

/usr/tmp Another directory for temporary files.

/var Variable data files, such as spool queues and log files.

For more information on the directory structure of Linux-based systems, see the Filesystem Hierarchy Standard [http://www.pathname.com/fhs/].

On Debian systems, you can also view this information in the compressed files in the /usr/doc/debian-policy/fsstnd/ directory (see Recipe 9.1 [Perusing Text], page 211).

## 5.1 Naming Files and Directories

File names can consist of any combination of upper- and lowercase letters, numbers, periods (.), hyphens (-), and underscores (_).¹ File names are also case-sensitive—foo, Foo, and FOO are all different file names, and they can all exist at the same time in a directory (files of identical name cannot). By convention, file names are almost always all lowercase letters.

Linux does not force you to use file extensions, but it is convenient and useful to give files proper extensions, since they will help you to identify file types at a glance.

There is no special requirement for extensions; the dot is just an old convention—you could use any system you like for any of your files:

```
Penny_Parker-20031103.letter
```

Files don’t have to have any extensions at all, like myfile, and you can have files with multiple extensions, too, like long.file.with.many.extensions. A JPEG-format image file, for example, does not have to have a .jpg or .jpeg extension, and program files do not need a special extension to make them work.

Extensions are particularly useful if you’re sending files to users on other computers, particularly systems that require extensions—send a file in Microsoft Word format to a Windows user without giving it a .doc extension first, and you’re likely to be told the file doesn’t work.

1 Technically, there are other characters that you can use—but doing so may get you into trouble later on.

The file name before any file extensions, but without the path, is called the base file name. For example, the base file name of /home/lisa/house.jpeg is house, without the dot or trailing .jpeg, and without the path.

For a list of commonly used file extensions and their meanings, see Appendix B [Conventional File Name Extensions], page 723.

The following sections show how to make new files. To rename an existing file, just move it to a file with the new name—see Recipe 5.5 [Moving Files and Directories], page 144.

### 5.1.1 Making an Empty File

You may sometimes want to create a new, empty file as a kind of “placeholder.” To do so, give the name that you want to use for the file as an argument to touch.

⇒ Here are some ways to use this.

- To create the file a_fresh_start in the current directory, type:
  $ touch a_fresh_start [RET]

- To create the file another_empty_file in the work/completed subdirectory of the current directory, type:
  $ touch work/completed/another_empty_file [RET]

This tool “touches” the files you give as arguments. If a file does not exist, it creates it; if the file already exists, it changes the modification timestamp on the file to the current date and time, just as if you had used the file.

NOTES: Often, you make a file when you edit it, such as with a text or image or sound editor; in that case, you don’t need to make the file first.

### 5.1.2 Making a Directory

Use mkdir (“make directory”) to make a new directory, giving the path name of the new directory as an argument. Directory names follow the same conventions as other files—that is, no spaces, slashes, or other unusual characters are recommended.

⇒ Here are some ways to use this.

- To make a new directory called work in the current working directory, type:
  $ mkdir work [RET]

- To make a new directory called work in the /tmp directory, type:
  $ mkdir /tmp/work [RET]

### 5.1.3 Making a Directory Tree

Use mkdir with the -p option to make a subdirectory and any of its parents that do not already exist. This is useful when you want to make a fairly complex directory tree from scratch and don’t want to have to make each directory individually.

⇒ To make the work/completed/2001 directory—a subdirectory of the completed directory, which in turn is a subdirectory of the work directory in the current directory, type:

```
$ mkdir -p work/completed/2001 [RET]
```

This makes a 2001 subdirectory in the directory called completed, which in turn is in a directory called work in the current directory; if the completed or the work directories do not already exist, they are made as well. If you know that work and completed both exist, the previous command works fine without the -p option.

### 5.1.4 Using a File with Spaces in Its Name

While a space character is not forbidden in naming files, it does make them difficult to use. Sometimes you might get one made on a system running MacOS, where space characters are common in file names. If a directory or file has a space in its name, there are two methods for specifying the name on the command line.

To reference a file with a space character in its name, quote the name (see Recipe 3.1.3 [Quoting Reserved Characters], page 56). The following methods are variations on this.

### METHOD #1

To use a file with space in its name, enclose the file in single-quote characters (').

⇒ To list the contents of the directory named Top Secret, type:

```
$ ls 'Top Secret' [RET]
```

You can also use double quote characters (") to quote; if a file name contains one kind of quote in its name, use the other.

⇒ To list the contents of the directory named McHale's Restaurant, type:

```
$ ls "McHale's Restaurant" [RET]
```
