
the document, or group of documents. This new indexed file, not the original HTML file, is what DocSearch will search and display.

This section will give an overview of the steps involved to register a document and create the indexes that the Documentation Library Service requires.

1. Create the document in HTML format.
2. Create an index of the document.
3. Register the new indexes with the documentation server.

After the indexes are registered, they will be displayed in the Web browser ready for searching and viewing. You can find detailed step-by-step procedures for each of these operations in the online Documentation Library Service chapter “AIX 5L Version 5.1 General Programming Concepts: Writing and Debugging Programs.” Application developers writing documentation will find this chapter especially valuable for creating auto-installed indexes when writing **installp** packages. You can also register your company’s documentation with the online documentation library. This flexibility makes DocSearch a valuable enterprise-wide documentation search engine.

## Common DocSearch and man Page Problems

You may experience one or more errors while using DocSearch. This is a top five list of the most common problems.

**Problem 1** One of the most common problems is domain name resolution. You might have to edit the /etc/hosts file and add a period (.) right behind the short hostname. For example,

`10.10.10.2 booboo.`

**Problem 2** After a 5.1 migration install, you enter **man ls** and find that there is no error or data output. You are experiencing one of the quirks that DocSearch displays. First make sure that the command's files are installed. The following will produce a directory listing of the files:

```
# lsipp -f bos.man.en_US.cmbs
```

This should show you the files that were installed for the **bos.man.en_US.cmbs** files.

If you then **cd to /usr/share/man/info/en_US** and run a long recursive listing (**ls -Rl * | more**) of the directory contents and most of the files are empty, then you have a problem. You have to install/reinstall the following files to correct the problem:

- bos.html.en_US.topnav.navigate - Top Level Navigation
- bos.html.en_US.nav - Online Navigation
- bos.html.en_US.cmbs.cmdbal - AIX Commands Reference 1
- bos.html_en_US.cmds.cmda2 - AIX Commands Reference 2
- bos.html_en_US.cmds.cmda3 - AIX Commands Reference 3
- bos.html_en_US.cmds.cmda4 - AIX Commands Reference 4
- bos.html_en_US.cmds.cmda5 - AIX Commands Reference 5
- bos.html_en_US.cmds.cmda6 - AIX Commands Reference 6

**Problem 3**

You get the following error message: *“Error: Can’t open display: XYZ.”* This means that you are trying to open a window defined by the DISPLAY variable that is incorrect, that the variable is unset, or that you do not have permission to use this display. Issue the following commands in sequence:

```
# xhost -<remote_hostname_or_IP_address>
# export DISPLAY=<local_hostname_or_IP_address>:0.0
# docsearch &
```

**Problem 4**

There is no DocSearch icon on the CDE help subpanel. You have installed DocSearch, and CDE has not discovered the new icon. You need to restart the workspace manager to discover the new icon. Right-click an empty part of the screen. This will bring up the Workspace menu. In the menu, left-click Restart Workspace Manager and then click OK in the pop-up dialog box. Alternatively, you can log out and log back into the system.

**Problem 5**

DocSearch is starting and you receive a message that it cannot find the documentation server. In AIX 5L version 5.1, you have to manually edit the *httpd.conf* file to define the documentation server.

```
# vi /usr/HTTPServer/conf/httpd.conf
```

Search the file for the *ServerName* variable. Uncomment the line and enter the fully qualified hostname of the documentation server:

*ServerName* yogi.mydomain.com

## man pages

The man pages provide reference documentation about AIX commands, files, library subroutines, and system calls. The **man** command does not perform the same kind of pattern search that DocSearch provides, so you will need to know the exact command or filename for which you are seeking information. The syntax for the **man** command follows.

```
# man { command | file | subroutine | system call }
```

For example,

```
# man man
```

will display the online documentation for the **man** command. The **man** command searches and displays documents in the following order:

- Any **nroff** directories (**man?**) in the `/usr/share/man` directory structure.
- The formatted-version directories (**cat?**) in the `/usr/share/man` directory structure.
- If the previous two searches fail, the hypertext (DocSearch) database is searched.
- The hypertext documentation is located in the `/usr/share/man/info` directory structure.

## Installing man Pages on AIX 4.3.3 and 5L Version 5.1

If your system only needs the man pages, then DocSearch may be overkill for you. To install the man pages on both 4.3.3 and 5L, all of the following filesets must be installed:

- bos.html.en_US.topnav.navigate - Top Level Navigation
- bos.html.en_US.nav - Online Navigation
- bos.html.en_US.cmds.cmddal - AIX Commands Reference 1
- bos.html.en_US.cmds.cmsd2 - AIX Commands Reference 2
- bos.html.en_US.cmds.cmsd3 - AIX Commands Reference 3
- bos.html.en_US.cmds.cmsd4 - AIX Commands Reference 4
- bos.html.en_US.cmds.cmsd5 - AIX Commands Reference 5
- bos.html.en_US.cmds.cmsd6 - AIX Commands Reference 6

## Using the man Pages

The **man** command has access to information stored in DocSearch. When invoked, **man** will first search `/usr/man/cat?` directories, then `/usr/man/man?`, and, finally, DocSearch data if it is installed. The commands **man** and **catman** map man page sections 1, 2, and 8 to DocSearch commands documents, sections 2 and 3 to DocSearch subroutines documents, and sections 4, 5, and 7 to DocSearch files documents. You will need to periodically execute **catman -w** to keep the database for the **arprofs** and **whatis** commands up to date.

```
# catman -w
```

From time to time, you may need to add your own custom man page information. This could be a help file explaining billing policies, backup support, locally developed software, and so on. It’s a good idea to keep local man pages separate from vendor-supplied help. This keeps them from getting stepped on during installation, maintenance, and upgrade activities. Commonly used location paths for local man pages are /usr/man/man1 and /usr/local/man/man7. The MANPATH environment variable can be set in /etc/environment to include your local man page path. Users may also use MANPATH to support their own man directories.

Here are some local man page repositories:

- /usr/man/man1
- /usr/local/man/man?
- /usr/local/cat/cat?

When creating new man pages, you can use an existing man page as a template. Try to stay within a common style so that your users know what to expect. Each man page should include a name section identifying the topic or command, a synopsis describing the command and argument options and format, a description section that describes the topic, an options section that details parameter and value information, and a section on known bugs. At the end of the man page, a "see also" section indicating related information and an optional author section identifying the author name and address can be considered.

The following is an example man page style:

```
mycommand(1)
NAME
    mycommand - Does just what I want to do.
SYNOPSIS
    mycommand [will|wont] work
    mycommand is always used as a last resort. It can
    be expected either to work or to fail. mycommand
    contains no surprises at all.
OPTIONS
    will     Completes the work at hand.
    wont     Take a vacation.
BUGS
    mycommand is always error free!
SEE ALSO
    myprogram(1), myshell(1)
AUTHOR
    Me. Who did you think it was?
```

You can include *nroff* tags in the man page to control display format. After the tags are included, you can test them using *nroff* (see Table 2-1).

```
# nroff -man mycommand.1 | more
Here is a sample man page with tags inserted:
.TH mycommand 1
```
