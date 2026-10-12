
## cd

cd stands for change directory. You will find this command extremely useful. The three typical ways of using this command are

- `cd ..` Moves one directory up the directory tree.
- `cd -` Moves to your home directory from wherever you currently are. This is the same as issuing cd by itself.
- `cd directory name` Changes to a specific directory. This can be a directory relative to your current location or can be based on the root directory by placing a forward slash (/) before the directory name.

These examples can be combined. For example, suppose you are in the directory /home/dsp1234 and want to go to tng4321's home account. You can perform the following command to move back up the directory one level and then down into the tng4321 directory:

```
cd ../tng4321
```

## chfn

The chfn command changes finger information. You can use this command to enter or update information used by the finger networking tool from the /etc/passwd entry for your Linux system. You can enter full names, offices, and office and home phone numbers. Follow chfn by a user's name:

```
# chfn Willie
```

## chgrp

The chgrp command is used to change the group associated with the permissions of the file or directory. The file's owner (and, of course, root) has the authority to change the group associated with the file. The format for the command is simply this:

```
chgrp <new group> <file>
```

## chmod

The chmod command is used to change the permissions associated with the object (typically a file or directory). What you are really doing is changing the file mode. You can specify the permissions of the object in two ways: by the numeric coding system or by the letter coding system. If you recall, three sets of users are associated with every object: the owner of the object, the group for the object, and everybody else. Using the letter coding system, they are referred to as u for user, g for group, o for other, and a for all. The three basic types of permissions you can change are r for read, w for write, and x for execute. These three permissions can be changed by using the plus (+) and minus (-) signs. For example, you would issue the following command to add read and execute to owner and group of the file test1:

```
chmod ug+rx test1
```

To remove the read and execute permissions from the user and group of the test1 file, you would change the plus (+) sign to a minus (-) sign:

```
chmod ug-rx test1
```

This is referred to as making relative changes to the mode of the file.

When using the numeric coding system, you always have to give the absolute value of the permissions, regardless of their previous permissions. The numeric system is based on three sets of base 2 numbers—one set for each category of user, group, and other. The values are 4, 2, and 1, where 4 equals read, 2 equals write, and 1 equals execute. These values are added together to give the set of permissions for that category. With numeric coding, you always specify all three categories. Therefore, to give read, write, and execute permissions to the owner of the file test1, and no permissions to anyone else, you would use the value 700, like this:

```
chmod 700 test1
```

To make the same file readable and writable by the user, and readable by both the group and others, you would use the following mathematical logic. For the first set of permissions—the user—the value for readable is 4 and the value for writable is 2. The sum of these two is 6. The next set of permissions—the group—only gets readable, so that is 4. The setting for others, as for the group, is 4. Therefore, the command would be as follows:

```
chmod 644 test1
```

The format for the command, using either method, is the same. You issue the chmod command followed by the permissions, either absolute or relative, followed by the objects for which you want the mode changed:

```
chmod <permissions> <file>
```

## chown

This command is used to change the user ID (owner) associated with the permissions of the file or directory. The owner of the file (and, of course, root) has the authority to change the user associated with the file. The format for the command is simply this:

```
chown new user id file
```

## chroot

The `chroot` command makes the `/` directory (called the **root directory**) be something other than `/` on the filesystem. For example, when working with an Internet server, you can set the root directory to equal `/usr/ftp`. Then, anyone who logs on using FTP (which goes to the root directory by default) will actually go to the directory `/usr/ftp`. This protects the rest of your directory structure from being seen or even changed by this anonymous guest to your machine. If someone were to enter `cd /etc`, the ftp program would try to put her in the root directory and then in the etc directory off of that. Because the root directory is `/usr/ftp`, the ftp program will actually put the user in the `/usr/ftp/etc` directory (assuming there is one).

The syntax for the command is this:

```
chroot original_filesystem_location new_filesystem_location
```

## chsh

You can use this program to change the type of shell you use when you log into your Linux system. The shell must be available on the system and must be allowed by the root operator by having its name listed in the `/etc/shells` file. Type the name of a shell, following the `chsh` command:

```
# chsh zsh
```

## control-panel

The `control-panel` command is one of several Red Hat Linux system administration tools. This command is an X11 client (actually a Python language script) used to display several system administration tools, such as timedtool, netcfg, or modemtool.

## cp

The `cp` command is an abbreviation for copy; therefore, this command enables you to copy objects. For example, to copy the file `file1` to `file2`, issue the following command:

```
cp file1 file2
```

As the example shows, the syntax is very simple:

```
cp original_object_name new_object_name
```

## cpio

The `cpio` command copies files in and out of file archives. `cpio` works much like the `tar` (tape archive) command, but with a slightly different syntax. Many Red Hat Linux users are more familiar with the `tar` command.

## crond

This is the cron daemon. This program, started when you first boot Linux, scans the `/etc/crontab` file and the `/var/spool/cron` directory, looking for regularly scheduled jobs entered by the root operator or other system users. It is started when you first boot Linux.

## crontab

The crontab command, not to be confused with the `/etc/crontab` file, is used by your system's users to schedule personal cron events. The cron files are stored under the `/var/spool/cron` directory. System administrators can control whether this facility exists on the system through the `/etc/cron.allow` and `/etc/cron.deny` files. All current jobs are listed when the crontab command is used with the -l option. Use the -e option to create or edit a job, and the -r option to delete a job.

## cu

cu is a communications program used to call up other computers. This program is text-based and is not as user-friendly as the minicom or seyon communications programs for Linux.

## cut

This program cuts specified columns or fields from input text. The cut command, a text filter, can be used to manipulate the output of other text utilities or contents of your files by selectively displaying fields of text.

## dc

dc is a command-line desk calculator. This calculator, which does not have a graphical interface, uses reverse-polish notation to perform calculations entered from the command line or a file.

## dd

The dd command converts file formats. For example, to copy a boot image to a disk (assuming the device name for the disk is /dev/fdo), you issue this command:

```
dd if=file name of=/dev/fdo obs=10k
```

file name might be BOOTOOO1.img, of is the object format (what you are copying to), and obs is the output block size.
