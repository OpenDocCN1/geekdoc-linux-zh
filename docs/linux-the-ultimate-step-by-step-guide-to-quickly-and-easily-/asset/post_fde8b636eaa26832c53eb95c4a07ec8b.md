
# Looking at the Contents of Directories with “ls”

Now that you know how to display the directory that you are in, we can show you how to look at the contents of a directory.

Currently, your home directory does contain much, so we will go to another, more populated directory to explore. Type the following command in your terminal to change directory (we will explain the details of moving directories in the next section). Afterward, we will use `pwd` to confirm that we successfully moved:

```bash
cd /usr/share
pwd
/usr/share
```

Now that we are in a new directory, let us look at what’s inside. To do this, we can use the `ls` command:

```bash
ls
adduser    groff     pam-configs
applications grub    perl
apport     grub-gfxpayload-lists perl5
apps       hal       pixmaps
apt        i18n      pkgconfig
aptitude   icons     polkit-1
apt-xapian-index info  popularity-contest
```

As you can see, there are *many* items in this directory. We can add some optional flags to the command to modify the default behavior. For instance, to list all of the contents in an extended form, we can use the `-l` flag (for “long” output):

```bash
ls -l
total 440
drwxr-xr-x  2 root root  4096 Apr 17  2014 adduser
drwxr-xr-x  2 root root  4096 Sep 24 19:11 applications
drwxr-xr-x  6 root root  4096 Oct  9 18:16 apport
drwxr-xr-x  3 root root  4096 Apr 17  2014 apps
drwxr-xr-x  2 root root  4096 Oct  9 18:15 apt
drwxr-xr-x  2 root root  4096 Apr 17  2014 aptitude
drwxr-xr-x  4 root root  4096 Apr 17  2014 apt-xapian-index
drwxr-xr-x  2 root root  4096 Apr 17  2014 awk
```

This view gives us plenty of information, most of which looks rather unusual. The first block describes the file type (if the first column is a “d” the item is a directory, if it is a “-”, it is a normal file) and permissions. Each subsequent column, separated by white space, describes the number of hard links, the owner, group owner, item size, last modification time, and the name of the item. We will describe some of these at another time, but for now, just know that you can view this information with the `-l` flag of `ls`.

To get a listing of all files, including *hidden* files and directories, you can add the `-a` flag. Since there are no real hidden files in the `/usr/share` directory, let’s go back to our home directory and try that command. You can get back to the home directory by typing `cd` with no arguments:

```bash
cd
ls -a
. .. .bash_logout .bashrc .profile
```

As you can see, there are three hidden files in this demonstration, along with `.` and `..`, which are special indicators. You will find that often, configuration files are stored as hidden files.

The dot and double dot entries, are built-in methods of referring to related directories. The single dot indicates the current directory, and the double dot indicates this directory’s parent directory. This will come in handy in the next section.

# Moving Around the Filesystem with “cd”

We have already changed directories twice to demonstrate some properties of `ls`. Let’s take a better look at the command here.

Begin by going back to the `/usr/share` directory by typing this:

```bash
cd /usr/share
```

This is an example of changing a directory by giving an absolute path. In Linux, every file and directory is under the top-most directory, which is called the “root” directory, but referred to by a single leading slash “/”. An absolute path indicates the location of a directory in relation to this top-level directory. This lets us refer to directories in an unambiguous way from any place in the filesystem. Every absolute path must begin with a slash.

The alternative is to use relative paths. Relative paths refer to directories in relation to the *current* directory. For directories close to the current directory in the hierarchy, this is usually easier and shorter. Any directory within the current directory can be referenced by name without a leading slash. We can change to the locale directory within /usr/share from our current location by typing:

```bash
cd locale
```

We can likewise change multiple directory levels with relative paths by providing the portion of the path that comes after the current directory’s path. From here, we can get to the LC_MESSAGES directory within the en directory by typing:

```bash
cd en/LC_MESSAGES
```

To move up one directory level, we use the special double dot indicator we talked about earlier. For instance, we are now in the /usr/share/locale/en/LC_MESSAGES directory. To move up one level, we can type:

```bash
cd ..
```

This takes us to the /usr/share/locale/en directory.

A shortcut that you saw earlier that will always take you back to your home directory is to use cd without providing a directory:

```bash
cd
pwd
/home/demo
```

# Viewing Files

In the last section, we learned how to navigate the filesystem. In this section, we will discuss different ways to view files. In contrast to some operating systems, Linux and other Unix-like operating systems rely on plain text files for vast portions of the system. The main way that we will view files is with the less command. This is what we call a “pager”, because it allows us to scroll through pages of a file. While the previous commands immediately executed and returned you to the command line, less is an application that will continue to run and occupy the screen until you exit.

We will open the /etc/services file, which is a configuration file that contains the systems services information:

```bash
less /etc/services
```

The file will be opened in less, allowing you to see the portion of the document that fits in the terminal window:

```
# Network services, Internet style
#
# Note that it is presently the policy of IANA to assign a single well-known port number for both TCP and UDP; hence, officially ports have two entries
#
# even if the protocol doesn't support UDP operations.
#
# Updated from http://www.iana.org/assignments/port-numbers and other
#
# sources like http://www.freebsd.org/cgi/cvsweb.cgi/src/etc/services .
#
# New ports will be added on request if they have been officially assigned
#
# by IANA and used in the real-world or are needed by a debian package.
#
# If you need a huge list of used numbers please install the nmap package.

tcpmux			1/tcp				# TCP port service multiplexer
echo			7/tcp
```

To scroll, you can use the up and down arrow keys on your keyboard. To page down one whole screens-worth of information, you can use either the space bar, the “Page Down” button on your keyboard, or the **CTRL-f** shortcut.

To scroll back up, you can use either the “Page Up” button, or the **CTRL-b** keyboard shortcut. To search for some text in the document, you can type a forward slash “/” followed by the search term. For instance, to search for “mail”, we would type: /mail  This will search forward through the document and stop at the first result. To get to another result, you can type the lower-case **n** key:

```
n
```

To move backwards to the previous result, use a capital **N** instead:

```
N
```

When you wish to exit the `less` program, you can type **q** to quit:

```
q
```

While we focused on the `less` tool in this section, there are many other ways of viewing a file. The `cat` command displays a file’s contents and returns you to the prompt immediately. The `head` command, by default, shows the first 10 lines of a file. Likewise, the `tail` command shows the last 10 lines. These commands display file contents in a way that is useful for “piping” to other programs. We will discuss this concept in a future guide.

Feel free to see how these commands display the `/etc/services` file differently.

# File and Directory Manipulation

We learned in the last section how to view a file. In this section, we will demonstrate how to create and manipulate files and directories.

# Create a File with “touch”
