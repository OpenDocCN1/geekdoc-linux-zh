
# ash

ash is a simple shell with features much like the sh or Bourne Again SHell. The ash shell is run by the symbolic link bsh, which is found under the /bin directory.

# at

at runs a program at a specified time. You can use the at command to schedule a task or job to run at a time you specify on the command line or in a file.

# atq

Use atq to list the queue of waiting jobs. The atq command prints a list of waiting jobs or events for the at command (usually found under /var/spool/at directory).

# atrm

Use atrm to remove a specified job. The atrm command removes one or several jobs waiting in the queue. The atrm command can be used by users or the root operator to delete pending events (stop at commands from running).

# bash

bash is the GNU Bourne Again SHell. The default shell for SuSE Linux, bash has many features, such as command-line editing, built-help, and command history. The bash shell can also be run by the symbolic link sh, which is found under the /bin directory.

# batch

The batch command runs jobs according to load average. This program is used to run events when the computer reaches a certain load average, as determined by real-time values found in the loadavg file in the /proc directory. batch also has other options; read the command manual pages for details.

# bc

A calculator language, bc is an interpreter and language for building calculator programs and tools. You can use this interpreter and language to program custom calculators.

# bg

The bg command is used to force a suspended process to run in the background. For example, say you have started a command in the foreground (without using the & after the command) and realize it is going to take a while, but you still need your shell. You can use Ctrl+Z to place the current process on hold. Then you can either leave it on hold—just as if you called your telephone company—or you can type bg to place that process in the background and free your shell to allow you to execute other commands (the command can be brought back to the foreground with fg).

# bind

Used in ksh, the bind command enables the user to change the behavior of key combinations for the purpose of command-line editing. Many people bind the up-, left-, and right-arrow keys so they work the way they would in the Bourne Again Shell (bash). The syntax used for the command is:

```
bind <key sequence> <command>
```

The following examples are the bind commands to create bindings for scrolling up and down the history list and for moving left and right along the command line:

```
bind '[[prefix-2
bind 'XA=up-history
bind 'XB=down-history
bind 'XC=forward-char
bind 'XD=backward-char
```

![](img/cbac72550c7126a22162e94d91a0c360_1032_0.png)

# cat

cat concatenates the standard input to the standard output. The cat command generally requires something to display and has the following format:

```
cat <filename>
```

# cd

cd stands for "change directory." You will find this command extremely useful. The three typical ways of using this command are:

```
cd ..    Moves one directory up the directory tree.
cd ~     Moves to your home directory from wherever you are currently.
           This is the same as issuing cd by itself.
```

cd directory name Changes to a specific directory. This can be a directory relative to your current location or based on the root directory by placing a forward slash (/) before the directory name.

These examples can be combined. For example, suppose you are in the /home/dsp1234 directory and you want to go to tng4321's home account. You can perform the following command to move back up the directory one level and then move down into the tng4321 directory:

```
cd ..//tng4321
```

# chfn

The chfn command changes finger information. You can use this command to enter or update information used by the finger networking tool from the /etc/passwd entry for your Linux system. You can enter full names, offices, and home phone numbers. Follow chfn with a user's name:

```
# chfn willie
```

# chgrp

The chgrp command is used to change the group associated with the permissions of the file or directory. The owner of the file (and, of course, root) has the authority to change the group associated with the file. The format for the command is simple:

```
chgrp <new group> <file>
```

# chmod

The chmod command is used to change the permissions associated with the object (typically a file or directory).

# chown

The chown command is used to change the user ID (owner) associated with the permissions of the file or directory. The owner of the file (and, of course, root) has the authority to change the user associated with the file. The format for the command is as follows:

```
chown <new userid> <file>
```

# chroot

The chroot command makes / directory (called the root directory) something other than / the filesystem when running a specified command. For example, when using the ftp command, you can set the root directory to equal /usr/ftp. Anyone who logs on using FTP (which goes to the root directory by default) will actually go to the directory /usr/ftp. This protects the rest of your directory structure from being seen or even changed by this anonymous guest to your machine. If someone were to enter cd/etc, the ftp program would try to put him or her in the root directory and then in the etc directory off of that. Because the root directory is /usr/ftp, the ftp program will actually put the user in the /usr/ftp/etc directory (assuming there is one).

The syntax for the command follows:

```
chroot <new filesystem location> <command>
```

# chsh

You can use this program to change the type of shell you use when you log in to your Linux system. The shell must be available on the system and must be allowed by the root operator by its name listed in the /etc/shells file. Type the name of a shell, following the chsh command:

```
# chsh zsh
```

# cp

The cp command is an abbreviation for copy; therefore, this command enables you to copy objects. For example, to copy the file file1 to file2, issue the following command:

```
# cp file1 file2
```

As the example shows, the syntax is very simple:

```
cp <original object name> <new object name>
```

# cpio

The cpio command copies files in and out of file archives. cpio works like the tar (tape archive) command, but with a slightly different syntax. Many SuSE Linux users are more familiar with the tar command.

# cron

This is the cron daemon. This program, started when you first boot Linux, scans the /etc/crontab file and the /var/cron/tabs directory.

# crontab

The crontab command, not to be confused with the /etc/crontab file, is used by your system's users to schedule personal cron events. The cron events are stored in a directory with the user's name under the /var/cron/tabs directory. By default, SuSE Linux allows users to create cron jobs. All current jobs are listed when the crontab command is used with the -l option. Use the -e to create or edit a job and the -r option to delete a job.

![](img/cbac72550c7126a22162e94d91a0c360_1034_0.png)

# cu

cu is a communications program used to call up other computers. This program is text-based and is not as user-friendly as the minicom communications program for Linux.

# cut

This program cuts specified columns or fields from input text. The cut command, a text filter, can be used to manipulate the output of other text utilities or contents of your files by selectively displaying fields of text.

# dc

dc is a command-line desk calculator. This calculator, which does not have a graphical interface, uses reverse-polish notation to perform calculations entered from the command line or a file.

# dd

The dd converts file formats. For example, to copy a boot image to a disk (assuming the device name for the disk is /dev/fd0), issue the following command:

```
dd if=<filename> of=/dev/fd0 bs=18k
```

where filename might be BOOT0001.img; of is the object format (what you are copying to); and bs is the output block size.

# df

Use the df command to show the amount of free disk space on any currently mounted filesystem. This information is useful in determining whether you have available storage for programs or data.

# dir

dir lists the contents of directories. This command has many of the same command-line options as the ls command.

# display

This program requires X11 and is part of the ImageMagick package. This is a menu-driven application you can use to create, edit, print, and save graphics during your X11
