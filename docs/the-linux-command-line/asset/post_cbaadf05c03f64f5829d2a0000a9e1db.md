
over eighty pages long and extremely dense, and its structure makes absolutely no sense to a new user.

On the other hand, it is very accurate and concise, as well as being extremely complete. So check it out if you dare and look forward to the day when you can read it and it all makes sense.

## info – Display A Program's Info Entry

The GNU Project provides an alternative to man pages for their programs, called “info.” Info pages are displayed with a reader program named, appropriately enough, info. Info pages are hyperlinked much like web pages. Here is a sample:

```
File: coreutils.info,  Node: ls invocation,  Next: dir invocation,
Up: Directory listing

10.1 `ls': List directory contents
===================================

The `ls' program lists information about files (of any type,
including directories).  Options and file arguments can be intermixed
arbitrarily, as usual.

    For non-option command-line arguments that are directories, by
default `ls' lists the contents of directories, not recursively, and
omitting files with names beginning with '.'.  For other non-option
arguments, by default `ls' lists just the filename.  If no non-option
argument is specified, `ls' operates on the current directory, acting
as if it had been invoked with a single argument of `.'.

    By default, the output is sorted alphabetically, according to the
--zz-Info: (coreutils.info.gz)ls invocation, 63 lines --Top----------
```

The info program reads info files, which are tree structured into individual nodes, each containing a single topic. Info files contain hyperlinks that can move you from node to node. A hyperlink can be identified by its leading asterisk, and is activated by placing the cursor upon it and pressing the enter key.

To invoke info, type “info” followed optionally by the name of a program. Below is a table of commands used to control the reader while displaying an info page:

Table 6-2: info Commands

| Command | Action |
|---|---|
| ? | Display command help |
| PgUp or Backspace | Display previous page |
| PgDn or Space | Display next page |
| n | Next - Display the next node |
| p | Previous - Display the previous node |
| u | Up - Display the parent node of the currently displayed node, usually a menu. |
| Enter | Follow the hyperlink at the cursor location |
| q | Quit |

Most of the command line programs we have discussed so far are part of the GNU Project’s “coreutils” package, so typing:

```
[me@linuxbox ~]$ info coreutils
```

will display a menu page with hyperlinks to each program contained in the coreutils package.

## README And Other Program Documentation Files

Many software packages installed on your system have documentation files residing in the /usr/share/doc directory. Most of these are stored in plain text format and can be viewed with less. Some of the files are in HTML format and can be viewed with a web browser. We may encounter some files ending with a “.gz” extension. This indicates that they have been compressed with the gzip compression program. The gzip package includes a special version of less called zless that will display the contents of gzip-compressed text files.

## Creating Your Own Commands With alias

Now for our very first experience with programming! We will create a command of our own using the alias command. But before we start, we need to reveal a small command line trick. It's possible to put more than one command on a line by separating each command with a semicolon character. It works like this:

```
command1; command2; command3...
```

Here's the example we will use:

```
[me@linuxbox ~]$ cd /usr; ls; cd -
bin games kerberos lib64 local share tmp
etc include lib libexec sbin src
/home/me
[me@linuxbox ~]$
```

As we can see, we have combined three commands on one line. First we change directory to /usr then list the directory and finally return to the original directory (by using 'cd -') so we end up where we started. Now let's turn this sequence into a new command using alias. The first thing we have to do is dream up a name for our new command. Let's try "test". Before we do that, it would be a good idea to find out if the name "test" is already being used. To find out, we can use the type command again:

```
[me@linuxbox ~]$ type test
test is a shell builtin
```

Oops! The name "test" is already taken. Let's try "foo":

```
[me@linuxbox ~]$ type foo
bash: type: foo: not found
```

Great! "foo" is not taken. So let's create our alias:

```
[me@linuxbox ~]$ alias foo='cd /usr; ls; cd -'
```
