
### A Longer Look At Long Format

As we saw before, the "-l" option causes ls to display its results in long format. This format contains a great deal of useful information. Here is the Examples directory from an Ubuntu system:

```
-rw-r--r-- 1 root root 3576296 2007-04-03 11:05 Experience ubuntu.ogg
-rw-r--r-- 1 root root 1186219 2007-04-03 11:05 kubuntu-leaflet.png
-rw-r--r-- 1 root root 47584 2007-04-03 11:05 logo-Edubuntu.png
-rw-r--r-- 1 root root 44355 2007-04-03 11:05 logo-Kubuntu.png
-rw-r--r-- 1 root root 34391 2007-04-03 11:05 logo-Ubuntu.png
-rw-r--r-- 1 root root 32059 2007-04-03 11:05 oo-cd-cover.odf
-rw-r--r-- 1 root root 159744 2007-04-03 11:05 oo-derivatives.doc
-rw-r--r-- 1 root root 27837 2007-04-03 11:05 oo-maxwell.odt
-rw-r--r-- 1 root root 98816 2007-04-03 11:05 oo-trig.xls
-rw-r--r-- 1 root root 453764 2007-04-03 11:05 oo-welcome.odt
-rw-r--r-- 1 root root 358374 2007-04-03 11:05 ubuntu Sax.ogg
```

Let's look at the different fields from one of the files and examine their meanings:

**Table 3-2: ls Long Listing Fields**

| Field | Meaning |
| --- | --- |
| -rw-r--r-- | Access rights to the file. The first character indicates the type of file. Among the different types, a leading dash means a regular file, while a "d" indicates a directory. The next three characters are the access rights for the file's owner, the next three are for members of the file's group, and the final three are for everyone else. The full meaning of this is discussed in Chapter 9 – Permissions. |
| 1 | File's number of hard links. See the discussion of links later in this chapter. |
| root | The username of the file's owner. |
| root | The name of the group which owns the file. |
| 32059 | Size of the file in bytes. |
| 2007-04-03 11:05 | Date and time of the file's last modification. |
| oo-cd-cover.odf | Name of the file. |

Code for Information Interchange. This is a simple encoding scheme that was first used on Teletype machines to map keyboard characters to numbers.

Text is a simple one-to-one mapping of characters to numbers. It is very compact. Fifty characters of text translates to fifty bytes of data. It is important to understand that text only contains a simple mapping of characters to numbers. It is not the same as a word processor document such as one created by Microsoft Word or OpenOffice.org Writer. Those files, in contrast to simple ASCII text, contain many non-text elements that are used to describe its structure and formatting.

Plain ASCII text files contain only the characters themselves and a few rudimentary control codes like tabs, carriage returns and line feeds.

Throughout a Linux system, many files are stored in text format and there are many Linux tools that work with text files. Even Windows recognizes the importance of this format. The well-known NOTEPAD.EXE program is an editor for plain ASCII text files.

Why would we want to examine text files? Because many of the files that contain system settings (called *configuration files*) are stored in this format, and being able to read them gives us insight about how the system works. In addition, many of the actual programs that the system uses (called *scripts*) are stored in this format. In later chapters, we will learn how to edit text files in order to modify system settings and write our own scripts, but for now we will just look at their contents.

The *less* command is used like this:

```
less filename
```

Once started, the *less* program allows you to scroll forward and backward through a text file. For example, to examine the file that defines all the system's user accounts, enter the following command:

```
[me@linuxbox ~]$ less /etc/passwd
```

Once the *less* program starts, we can view the contents of the file. If the file is longer than one page, we can scroll up and down. To exit *less*, press the “q” key.

The table below lists the most common keyboard commands used by *less*.

**Table 3-3: less Commands**

| Command | Action |
|---|---|
| Page Up or b | Scroll back one page |
| Page Down or space | Scroll forward one page |
| Up Arrow | Scroll up one line |
| Down Arrow | Scroll down one line |
| G | Move to the end of the text file |
| 1G or g | Move to the beginning of the text file |
| /characters | Search forward to the next occurrence of characters |
| n | Search for the next occurrence of the previous search |
| h | Display help screen |
| q | Quit less |

### Less Is More

The less program was designed as an improved replacement of an earlier Unix program called more. The name “less” is a play on the phrase “less is more”—a motto of modernist architects and designers. less falls into the class of programs called “pagers,” programs that allow the easy viewing of long text documents in a page by page manner. Whereas the more program could only page forward, the less program allows paging both forward and backward and has many other features as well.

### A Guided Tour

The file system layout on your Linux system is much like that found on other Unix-like systems. The design is actually specified in a published standard called the Linux Filesystem Hierarchy Standard. Not all Linux distributions conform to the standard exactly but most come pretty close.

Next, we are going to wander around the file system ourselves to see what makes our Linux system tick. This will give you a chance to practice your navigation skills. One of the things we will discover is that many of the interesting files are in plain human-readable text. As we go about our tour, try the following:
