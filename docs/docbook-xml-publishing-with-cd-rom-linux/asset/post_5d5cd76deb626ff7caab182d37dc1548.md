
# Revision Control for Loners

If you're going to do a project by yourself, you might want to use revision control anyway. I've found that even for small articles or projects, it's nice to be able to roll back a version or two when I've deleted a paragraph or 10 paragraphs that I later decide to include in the piece. It's much simpler to use a version control system, after you become used to it, than to keep dozens of files in a directory, labeled article1.sgml, article1.sgml.old, article1.sgml.bak, and so forth.

# The GNU Revision Control System (RCS)

The GNU Revision Control System is usually part of a default Linux installation. Odds are, if you have a Linux system, you have it installed already. To find out, type rcs -V at a shell prompt. You should see something like RCS version 5.7. RCS 5.7 is the latest version of RCS available at the time of this writing. If you don't have RCS or want to get a newer version, visit the RCS Web site at http://www.cs.purdue.edu/homes/RCS/. The official page for RCS is at http://www.gnu.org/software/rcs/rcs.html (see Figure 7.1).

![](img/81f56bf497dbf7f7582072400d12cb42_165_0.png)

# The GNU Revision Control System (RCS)

## Installing RCS

RCS is easy to install. Download the tarfile from the RCS home page and unpack it in an appropriate directory by cding to the directory and running the following commands:

```bash
gzip -cd rcs-*.tar.gz | tar -xvf -
```

That will create a directory rcs-XX.XX (where XX is the version number). Next cd into that directory and run ./configure. If you are not root on the system, you might want to run ./configure --prefix=$HOME to build the software install in your home directory. Next run make followed by make install. If you are not installing to your home directory and you are not root, you will have to su before the make step.

If you prefer packaged versions of applications, there are both RPM and Debian packages available for your distribution to download, if you don't have your CDs. For RPM versions, visit http://www.rpmfind.net/ and search for RCS. You will receive a list of RPMs for source, binaries, development, and other platforms (Alpha, Sparc, etc.). You can search for Debian packages at http://www.debian.org/dist/packages. With the packaged versions, you can install it by using the appropriate package manager options.

![](img/81f56bf497dbf7f7582072400d12cb42_166_0.png)

## Basic RCS

RCS is easy to use, especially the basic commands. To start with, cd to the directory you're going to be working in. Usually, I like to maintain a directory for each project I'm working on, under a /Writing directory.

I try to keep one top-level directory, such as /Writing or something equally obvious, so that I know what to tar and gzip when I'm making a backup.

![](img/81f56bf497dbf7f7582072400d12cb42_166_1.png)

After you cp to the proper directory, you create an RCS directory for RCS to store revisions.

Run mkdir RCS, and RCS will use that directory to store any revisions you save in that directory. You must create an RCS directory in any directory containing files that are going to be managed with RCS.

![](img/81f56bf497dbf7f7582072400d12cb42_166_2.png)

## Checking In a File

Now that you have created a directory, go ahead and check in your first file.

To create the first revision of a file, run rcs -i testfile.txt. You should see RCS output as in Figure 7.2.

You are asked to enter a description. Type in a brief description of the file, and press Enter. Then you get the prompt again so, type a period to tell RCS that you're finished with the comment.

Congratulations! You've created the first version of your file.

## Creating a Revision

Now you want to create the first revision of the file. To do that, you use the check-in command for RCS, ci. (Isn't it nice the way UNIX-style commands are short and easy to type?)

Make a test file with a few lines of text in your favorite editor, and save it to the same directory under the name testfile.txt. When you're ready to save the

![](img/81f56bf497dbf7f7582072400d12cb42_167_0.png)

Figure 7.2 RCS output

![](img/81f56bf497dbf7f7582072400d12cb42_168_0.png)

**Figure 7.3** Creating a revision with RCS

first revision, type in ci testfile.txt. You will see RCS output as in Figure 7.3, if everything went smoothly: Notice the testfile.txt file is no longer in the directory. RCS deletes files when they are merged back into revision control. When you check out the file, RCS re-creates the latest version of the file for you, or the version you request. If you do not want RCS to delete your working copy of the file you've just checked in, instead of simply using ci testfile.txt, use ci -l testfile.txt.

![](img/81f56bf497dbf7f7582072400d12cb42_168_1.png)

## Checking Out a File

If you want to edit the testfile.txt, you must check it out of RCS to be able to work with it. To do that, you use the co command. In addition to checking the file out of RCS, you lock it so that no new revisions can be committed until you've checked in your latest revision. At the shell prompt, type in co -r filename.txt. Provided that everything is correct, RCS will give you feedback, as shown in Figure 7.4.

```bash
$ jrouwer@Writing$ co -l testfile.txt
RCS/testfile.lock (locked)
$ jrouwer@Writing$ last
```

![](img/81f56bf497dbf7f7582072400d12cb42_169_0.png)

The co command tells RCS that you want to check out a file, and the -l switch to lock the file in the process. If you check out a file without locking, RCS will complain when you try to check it in. If you're checking out a file only to read, it's okay to do so without locking. That way, if others try to check out the file, they can do so without problem. If the file is locked, they cannot check it out for editing. The reason the file is locked, as we discussed previously, is to prevent anyone else from committing revisions while you are editing the file.

## Rolling Back

If you have committed a few versions of your file and decided that two versions ago was perfect, no problem you can still check out the old version and work with it. For example, if you're at version 1.8 now and you want to work with version 1.5, you use the -r switch with the co command to check out the version of the file. To check version 1.5, type in co -r1.5 filename.txt. Now you have the 1.5 version checked out for reading purposes. To check it out for editing, use the -l switch to lock the file as well. Figure 7.5 shows the difference in RCS output when you lock a file using co. If you check out an older version of the file before you check in the newest, and they are in the same directory, you can end up overwriting the newest revision with the older one. RCS overwrites and deletes files without asking, which is okay if you're using it properly. However, if you're not careful, you can lose work.

![](img/81f56bf497dbf7f7582072400d12cb42_170_1.png)

## Keyword Substitution

RCS can also work a little magic for you when you check out a file and give you some information automatically. All you have to do is insert a keyword into the text, and RCS expands the keyword to contain the information asked for. For instance, if you'd like to know the date and time of each revision, include the $Date keyword. The keywords for RCS are surrounded by the $ character in front and back to prevent any confusion. If RCS sees the word date by itself, it will ignore it but substitute revision notes in place of the keyword when it is expressed like this, $Date$. The following is an example of using the $Date keyword.

```xml
$Date$
<!DOCTYPE chapter PUBLIC "-//OASIS//DTD DocBook V3.1//EN">
<chapter label="7">
<title>Collaborative Work with DocBook</title>
```

RCS supports keywords for the date and time, the username of the person who last revised the document, the filename, the log entry that was typed in the file, and several other options. We see the co for all the possible keywords. Figure 7.6 shows the output of the $Date keyword retrieved from RCS. Because Jade doesn't know anything about RCS keywords, if you parse a document that uses keywords with Jade, it produces errors when it sees something like $date: 2001/01/22 12:48:56 in the header of a DocBook document. This doesn't affect the output, however, so there's nothing to worry. I usually include keywords before the DocBook declaration so that any extended text doesn't make its way into document output.

![](img/81f56bf497dbf7f7582072400d12cb42_171_0.png)

| | |
| :--- | :--- |
| GIT commit:OASIS-docbook.xml |
| Date 2004/06/12 12:21:48 DocBook v1.4 | |
| OASIS/DocBook v1.4 | |
| chapter header with DocBook | |
| <?xml version="1.0" encoding="UTF-8"?> | |
| For example, an author, a section, a paragraph, a list item, a table, and a title. | |
| In this case, the time of this diff of what should be or should be, in the text, this can create new confusion, if not enough, chaos. | |
| I'm not sure if this is the best way, but it's the only way we've found to work for all of the elements. We're going to use the "class" attribute and so on, to keep track of the documents that we're working on. | |

Using DocBook for Collaborative Publishing

DocBook doesn't have any tags for collaboration, so we'll have to look outside DocBook for other Open Source tools. Perhaps you've noticed some really good revision control systems available. In this chapter we'll look at the Revision Control System (RCS), Desync (now Subversion), and CVS. But first thing, right?

There are many other revision control systems available, but RCS and CVS are the most popular ones. If you happen to have a favorited revision control system of your own, do well feel free to use it.

Figure 7.6 Extended RCS keywords
