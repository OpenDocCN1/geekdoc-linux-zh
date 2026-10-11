
- f. Enter `exit` twice to close the second terminal window.
- g. Switch to the terminal session where `tail` is running and press `CTRL-C` to break out of `tail`.
- 11. Switch back to your regular user account by entering `exit`.
- 12. Delete the `MyFiles` directory in your home directory by entering `rm -r ~/MyFiles`.
- 13. Enter `ls` and verify that the directory and its contents are gone.
- 14. Make a copy of your home directory files and subdirectories in `/tmp` by entering `cp -R ~/ /tmp/`.
- 15. View the contents of `/tmp` by entering `ls /tmp/`. Verify that your home directory was copied.
- 16. Work with symbolic links by doing the following:
  - a. Create a symbolic link from a directory named `docs` in your home directory to the `/usr/share/doc` directory by entering `ln -s /usr/share/doc/ ~/docs`.
  - b. Enter `ls -l`. Verify that the `docs` file points to `/usr/share/doc/`.
  - c. Enter `cd docs`.
  - d. Enter `pwd`. What directory are you in?
  - e. Enter `ls`. You should see the contents of the `/usr/share/doc/` directory even though you are still in `~/docs`.

## Finding Content Within Files

Earlier in this chapter, we discussed shell commands that can be used to search for files in the file system. However, Linux also provides a utility called `grep` that you can use to search for specific content *within* a file. The `grep` utility is extremely useful; in fact, I dare say that most Linux admins use it on a daily basis. Using `grep`, you can search through a file for a particular text string. This can come in handy when you want to search a very large log file for a specific message or when you need to find a specific directive within a configuration file. You can even use `grep` to search through multiple files at once to locate a particular expression.

To use `grep`, you enter `grep search_expression file_name` at the shell prompt. For example, let’s suppose you want to search through your `/var/log/messages` file for any log entries related to the VNC service running on your Linux system. You would enter `grep vnc /var/log/messages`. The `grep` utility would then display each line from the file that contained your search term, as shown here:

```text
fs2:~ # grep vnc /var/log/messages
Feb 1 13:47:25 fs2 xinetd[7134]: Reading included configuration file:
/etc/xinetd.d/vnc [file=/etc/xinetd.d/vnc] [line=15]
fs2:~ #
```

Likewise, if you needed to find a line in your /etc/ntp.conf file that contains the directive "server", you could enter `grep server /etc/ntp.conf` at the shell prompt. This is shown in the next example:

```text
fs2:~: $ grep server /etc/ntp.conf
# server 127.127.0.0 mode 5 prefer
server 127.127.1.0
## # ntpct addserver cyourserver
server bigben.cac.washington.edu iburst
# key (7) for accessing server variables
# controlkey 15
# key (6) for accessing server variables
fs2:~: $
```

When working with grep at the command line, you can use the following options:

- **-i** Ignores case when searching for the search text.
- **-l** Displays only the names of the files that contain matching text. It doesn’t display the actual matching line of text.
- **-n** Displays matching line numbers.
- **-r** Searches recursively through subdirectories of the path specified.
- **-v** Displays all lines that do not contain the search string.

The grep utility works great when you need to search for a specific text string within a file. However, there may be times when you need to search for more complex patterns. In this situation, you can use the egrep command instead.

> **NOTE** The egrep command is the same as using the grep -E command.

The key advantage of egrep is that it can search files for extended *regular expressions*. Regular expressions are strings consisting of *metacharacters* and *literals*.

> **NOTE** Literals are regular characters (A–Z, a–z) and numerals.

*Metacharacters* are characters that do not represent themselves but instead represent other characters. They can also be used to specify a character’s location within a text string. Some commonly used regular expressions are listed in Table 4-6. See the regex(7) man page for more information.

In addition to egrep, you can also use the fgrep (fixed-string grep) utility to search for content within files.

> **NOTE** Running fgrep is the same as running grep -F.

| Metacharacter | Function | Example |
| :--- | :--- | :--- |
| * | Matches any number of any characters. | Myfile* would match Myfile1, Myfile2, Myfiles, Myfiles23, etc. |
| . | Matches a single character | Myfile. would match Myfile1, Myfile2, and Myfiles, but would not match Myfiles23. |
| ^ | Matches an expression if it appears at the beginning of a line. | ^server would match any instance of "server" as long as it appears at the beginning of a line. |
| $ | Matches an expression if it appears at the end of a line. | server$ would match any instance of "server" as long as it appears at the end of a line. |
| \| | Matches the expressions on either side of the pipe character. | Server\|server would match either "Server" or "server". |
| [nnn] | Matches any one character between the braces. | [xyz] would match any one of "x", "y", or "z". |
| [^nnn] | Matches an expression that does not contain any one of the characters specified. | [^aei] would not match the characters "a", "e", or "i". |
| [n-n] | Matches any single character in the range. | [1-5] would match any number between 1 and 5. |

### Table 4-6 Regular Expressions

The grep utility searches files for lines that match a fixed string. Unlike egrep, it does not perform searches for regular expressions. Instead, fgrep uses direct string comparisons to find matching lines of text in the input. The syntax is fgrep pattern filename. For example, running the fgrep *.c command searches for the string "server" in all files in the current directory whose filename has a ".c" extension.

Let's practice using Linux search tools in the following exercise.

## Exercise 4-4: Using grep

In this exercise, you will practice using Linux search tools. Complete the following:

- 1. With your Linux system running and authenticated as a regular user, switch to root by entering su - followed by your root user's password at the shell prompt.
- 2. Locate references to the initab file in your system log file by entering grep initab /var/log/messages. What can you learn about this file from the output of grep?
- 3. Use egrep to find information about the init process in your system log file by entering egrep init* /var/log/messages at the shell prompt.
- 4. Use egrep again to find information about all the Ethernet interfaces installed in your system by entering egrep eth[0-3] /var/log/messages at the shell prompt.
- 5. Find all lines in your system log file that end with "Enabled" by entering grep Enabled$ /var/log/messages at the shell prompt.

You are now a file system pro! You have to be humble when you know this much!

## Chapter 4: Managing Linux Files and Directories

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_164_0.png)

**TIP** The /etc/updatedb.conf file is used to configure the behavior of the updatedb utility. You can set the PRUNEFS variable in this file to the file system type(s) you don't want updatedb to scan. You can also set the PRUNEPATHS variable in this file to a list of directories in your file system you want updatedb to skip when scanning.

## Chapter Review

In this chapter, I reviewed a variety of topics related to managing the Linux file system. I began this chapter by introducing you to the Linux file system. I first differentiated between a general file system and a specific disk file system such as Reiser or ext4. I then pointed out that the role of the Linux file system is to organize data such that it can be easily located and retrieved as well as reliably preserved.

I then related that Linux uses a hierarchical file system. The topmost directory of this hierarchy is the root directory (//). We discussed the role of the various standard directories used in a typical Linux system as specified in the Filesystem Hierarchy Standard (FHS). These include

- /bin
- /boot
- /dev
- /etc
- /home
- /lib
- /media
- /mnt
- /opt
- /proc
- /root
- /sbin
- /srv
- /sys
- /tmp
- /usr
- /var

I also discussed the four different types of files used on a Linux system: regular files, links, FIFOs, and sockets.

With this background information in hand, I turned our attention to common Linux file system tasks. I emphasized that, while most of these tasks can be performed using graphical utilities, the LPIC-1/CompTIA Linux+ exam expects you to know how to complete them from the shell prompt.
