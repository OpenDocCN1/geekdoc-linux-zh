
## head and tail

The head and tail commands are separate commands that work in essentially the same way. By default, the head filename command looks at the first 10 lines of a file; the tail filename command looks at the last 10 lines of a file. You can specify the number of lines shown with the -nxy switch. Just remember to avoid the space when specifying the number of lines; for example, the tail -n15 /etc/passwd command lists the last 15 lines of the /etc/passwd file.

The tail command can be especially useful for problems in progress. For example, if there's an ongoing problem, the following command monitors the noted file for login attempts:

```
# tail -f /var/log/secure
```

## Commands to Process Text Streams

A text stream is the movement of data. For example, the cat filename command streams the data from the filename file to the screen. When these files get large, it's convenient to have commands that can filter and otherwise process these streams of text.

To that end, Linux includes simple commands to help you search, check, or sort the contents of a file. And there are special files that contain others; some of these container files are known colloquially as tarballs.

![](img/9139201cfcaf4292284a0eed074928e5_152_0.png)

> Tarballs are a common way to distribute Linux packages. They are normally distributed in a compressed format, with a .tar.gz or .tgz file extension, consolidated as a package in a single file. In this respect, they are similar to Microsoft-style compressed zip files.

## sort

You can sort the contents of a file in a number of ways. By default, the sort command sorts the contents in alphabetical order depending on the first letter in each line. For example, the sort /etc/passwd command would sort all users (including those associated with specific services and such) by username.

## grep and egrep

The grep command uses a search term to look through a file. It returns the full line that contains the search term. For example, grep 'Michael Jang' /etc/passwd looks for the name of this author in the /etc/passwd file.

The egrep command is more forgiving; it allows you to use some unusual characters in your search, including +, ?, |, (, and ). While it's possible to set up grep to search for these characters with the help of the backslash, the command can be awkward.

## diff

One useful option to find the difference between files is the diff command. If you've just used a tool such as the Network Connections tool described later in this chapter, it'll modify a file such as ifcfg-eth0 in the /etc/sysconfig/network-scripts directory.

If you've backed up that ifcfg-eth0 file, the diff command can identify the differences between the two files. For example, the following command identifies the differences between the ifcfg-eth0 file in the /root and the /etc/sysconfig/network-scripts directories:

```
# diff /root/ifcfg-eth0 /etc/sysconfig/network-scripts/ifcfg-eth0
```

So if you've backed up the ifcfg-eth0 file to the /root directory, the command shown can help identify changes made by configuration tools.

## wc

The wc command, short for word count, can return the number of lines, words, and characters in a file. The wc options are straightforward; for example, wc -w filename returns the number of words in that file.

## sed

The sed command, short for stream editor, allows you to search for and change specified words or even text streams in a file. For example, the following command changes the first instance of the word "Windows" with "Linux" in each line of the file opesys, and writes the result to the file newopsys:

```
# sed 's/Windows/Linux' opesys > newopsys
```

However, this may not be enough. If there's more than one instance of "Windows" in a line in the opsys file, it does not change the second instance of that word. But you can fix this by adding a "global" suffix:

```
# sed 's/Windows/Linux/g' opsys > newopsys
```

The following example would make sure that all Samba shares configured with the writable = yes directive are reversed:

```
# sed 's/writable = yes/writable = no/g' /etc/samba/smb.conf > ~/smb.conf
```

Of course, you should then review the results in the /root/smb.conf file before overwriting the original /etc/samba/smb.conf file.

## awk

The awk command, named for its developers (Aho, Weinberger, and Kernighan), is more of a database manipulation utility. It can identify lines with a keyword, and read out the text from a specified column in that line. A common example is with the /etc/passwd file. For example, the following command will read out the username of every user with a listing of "mike":

```
# awk '/mike/ {print $1}' /etc/passwd
```

## Edit Text Files at the Console

The original version of the RHCSA objectives specified the use of the vim editor. Strictly speaking, it doesn't matter what text editor you use to edit text files. However, I believe that you need to know how to use the vim editor, and apparently some at Red Hat agree. The vim editor is short for vi, improved. When installed, you can also start the vim editor with the vi command. Hereafter, I refer to that text editor as vi.

I believe every administrator needs at least a basic knowledge of vi. While emacs may be more popular and flexible, vi may help you save a broken system. If you ever have to restore a critical configuration file using emergency boot media, vi may be the only editor that you'll have available.

While RHEL 6 also includes access to the more intuitive nano editor, a knowledge of vi commands can help you identify key sections of man pages and other text files more quickly. While RHEL rescue media supports more console-based editors, I describe vi here simply because it's the editor I know best.

You should know how to use the two basic modes of vi: command and insert. When you use vi to open a file, it opens in command mode. Some of the commands start insert mode. Opening a file is easy; just use the vi filename command. By default, this starts vi in command mode. An example of vi with the /etc/nsswitch.conf file is shown in Figure 3-4.

The following is only the briefest of introductions to the vi editor. For more information, there are a number of books available, as well as an extensive manual formatted as a HOWTO available from the Linux Documentation Project at www.tldp.org. Alternatively, a tutorial is available through the vimtutor command.

## vi Command Mode

In command mode, you can do everything to a text file except edit it. The options in command mode are broad and varied, and they are the subject of a number of book-length texts. In summary, options in vi command mode fall into seven categories:

- **Open** To open a file in the vi editor from the command line interface, run the vi filename command.
- **Search** For a forward search, start with a backslash (/), followed by the search term. Remember, Linux is case sensitive, so if you're searching for "Michael" in /etc/passwd, use the /Michael (not /michael) command. For a reverse search, start with a question mark (?).

![](img/9139201cfcaf4292284a0eed074928e5_155_0.png)

- **Write** To save your changes, use the w command. You can combine commands; for example, :wq writes the file and exits vi.
- **Close** To leave vi, use the :q command.
- **Abandon** If you want to abandon any changes, use the :q! command.
- **Edit** You can use a number of commands to edit files through vi, such as x, which deletes the currently highlighted character, dw, which deletes the currently highlighted word, and dd, which deletes the current line. Remember, p places text from a buffer, and U restores text from a previous change.
- **Insert** A number of commands allow you to start insert mode, including i to start inserting text at the current position of the editor, and o to open up a new line immediately below the current position of the cursor.

## Basic Text Editing

In modern Linux systems, editing files with vi is easy. Just use the normal navigation keys (arrow keys, PAGE UP, and PAGE DOWN), and then one of the basic commands such as i or o to start vi's insert mode, and type your changes directly into the file. When you're finished with insert mode, press the ESC key to return to command mode. You can then save your changes, or abandon them and exit vi.

> There are several specialized variations on the vi command. Three are vipw, vigw, and visudo, which edit /etc/passwd, /etc/group, and /etc/sudoers, respectively. The vipw -s and vigr -s commands edit the /etc/shadow and /etc/gshadow files.

## EXERCISE 3-1

## Using vi to Create a New User

In this exercise, you'll create a new user by editing the /etc/passwd file with the vi text editor. While there are other ways to create new Linux users, this exercise helps you verify your skills with vi and at the command line interface.

1. Open a Linux command line interface. Log in as the root user, and type the vipw command. This command uses the vi editor to open /etc/passwd.
