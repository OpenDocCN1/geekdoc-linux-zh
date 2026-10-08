
## 8. Create a New Directory

Type **mkdir dept_4550** and press **Enter** to make a new directory called dept_4550.

9. Type **ls** and press **Enter**. You see the dept_4550 directory in the listing.

10. Type **cd dept_4550** and press **Enter** to change to the new directory. Now you can use the cat command to create the file phones2, which contains the same fields as the phones1 file.

11. Type these commands, pressing **Enter** at the end of each line:

```text
cat > phones2
219:432:4591:Moore:Sarah
219:432:4567:Polk:John
219:432:4501:Robinson:Lisa
```

12. Press **Ctrl+D**.

You created two new directories using the mkdir command and then created two files of phone number information using the cat command.

> **Note:** You can delete empty directories by using the remove directory (rmdir) command. First, use the cd command to change to the parent directory of the subdirectory you want to delete. For example, if you want to delete the old directory in /home/old, first change to the home directory. Then type rmdir directory, as in rmdir old, and press Enter.

## Copying Files

You use the UNIX copy command, `cp`, to copy files from one directory to another. The -i option warns you that the cp command will overwrite the destination file. You can also use the dot notation (current directory) as shorthand to specify the destination of a cp command.

After you create the phone file, Rolfe wants you to create a new central directory for Dominion called corp_db and then copy the phones1 file into it. You can use the tilde character (~) to represent the location of your home directory.

To copy the phones1 file into a new directory, corp_db:

1. Type **cd** and then press **Enter** to return to the /home directory.
2. Type **mkdir corp_db** and press **Enter** to make a new directory.
3. Type **cd corp_db** and press **Enter** to change to the new directory.
4. To copy the phones1 file from the dept_4540 directory to the current directory, type **cp ~/dept_4540/phones1 .** and press **Enter**.
5. To copy the phones2 file from the dept_4550 directory to the current directory, type **cp ~/dept_4550/phones2 .** and press **Enter**.

Now the Dominion central database contains two files. You can use the cat command to combine the two files and redirect (>) the output to the `corp_phones` file, which lists all phone number information for the company.

**To concatenate two files to one:**

1. Type `cat phones1 phones2 > corp_phones` and press **Enter** to add the contents of the two phone files to one new file called `corp_phones`.
2. Type `more corp_phones` and press **Enter** to view the new file’s contents. As you recall from Chapter 1, the `more` command, which lets you display files one screen at a time, is especially useful for reading long files.

> **Note:** To delete files you do not need, use the `remove (rm)` command. First, use the `cd` command to change to the directory containing the file you want to delete. Then *type* `rm` *filename*. For example, to delete the file *old* in the current directory, type `rm old`. You may or may not receive a warning before the file is deleted. Be sure you want to remove a file permanently before using this command. You will learn more about the `rm` command in Chapter 4.

## Setting File Permissions

Because UNIX is a multi-user system, users can set permissions for files they own so that others can read, write, or execute their files. A file’s owner is the person who created it. The permissions the owner sets are listed as part of the file description. Figure 2-7 shows directory listings that describe file types.

| File type | Meaning |
|---|---|
| - | Normal file |
| d | Subdirectory |
| l | Symbolic link |
| b | Block device file |
| c | Character device file |

```text
Excerpt from ls -1 /etc

drwxr-xr-x  12  root  root    1024  Feb 6  1996  x11
-rw-r--r--   1  root  root      10  Oct 15 19:11  adjtime
drwxr-xr-x   1  root  root    1024  Feb 27  2000  cron.daily
```

```text
Excerpt from ls -1 /home/jean/source

-rw-rw-r--   1  jean  jean     387  Dec 12  23:11  phones.502
```

**Figure 2-7:** File types described in directory listings

Notice the long listing of the two directories. (Remember that the directory is just another file.) The earlier section, “Listing Directory Contents,” describes the information presented in a long listing. Now you can look closer at the file permissions. For the first file described, the column on the far left shows the string of letters drwxr-xr-x. You already know the first character indicates the file type. The characters that follow are divided into three sections of file permission specifiers. There are three specifiers in each section, as illustrated in Figure 2-8.

![](img/6d8286a85e2d8ad63e16f1801102da59_74_0.png)

**Figure 2-8:** Example of file type and file permissions for a file

The first section of file permission specifiers indicates the owner’s permissions. The owner, like all users, belongs to a group of users. The second section indicates the group’s permissions. This specification applies to all users other than the owner who are members of the owner’s group. The third section indicates all others’ permissions. This specification applies to all users who are not the owner and not in the owner’s group. In each section, the first character indicates read permissions. If an “r” appears there, that category of users has permission to read the file. The second character indicates write permission. If a “w” appears there, that category of user has permission to write to the file. The third character indicates execute permission. If an “x” appears there, that category of user has permission to execute the file. If a dash (-) appears in any of these character positions, that type of permission is denied.

> **Note:** If a user is granted read permission for a directory, the user can see a list of its contents. Write permission for a directory means the user can rename and delete files in the directory. Execute permission for a directory means the user can make the directory the current working directory.

From left to right, the letters rwxr-xr-x mean:

- r: File’s owner has read permission
- w: File’s owner has write permission
- x: File’s owner has execute permission (can run the file as a program)
- r: Group has read permission
- -: Group does not have write permission
- x: Group has execute permission
- r: Others have read permission
- -: Others do not have write permission
- x: Others have execute permission

You can change the pattern of permission settings by using the chmod command. For example, setting others' permissions to --- removes all permissions for others. They cannot read, write, or execute the file. In the first line of Figure 2-7, notice that the owner has read, write, and execute (rwx) permissions for the file X11. The r-x indicates that the group of users that shares the same group id as the owner has only read and execute permissions. The system administrator assigns group ids when he or she adds a new user account. Group ids give a group of users equal access to files that they all share. Others are all other users who are not associated with the owner's group by a group id, but have read and execute permissions.

Use the UNIX chmod command to set file permissions. In its simplest form, the chmod command takes as arguments a symbolic string followed by one or more file names. The symbolic string specifies permissions that should be granted or denied to categories of users. Here is an example: ugo+rwx. In the string, the characters ugo stand for user (same as owner), group, and others. These categories of users will be affected by the chmod command. The next character, the + sign, indicates that permissions are being granted. The last set of characters, in this case rwx, indicates the permissions being granted. The symbolic string ugo+rwx indicates that read, write, and execute permissions are being granted to the owner, group, and others. Here is an example of how the symbolic string is used in a command, to modify the access permissions of myfile:

```bash
chmod ugo+rwx myfile
```

Here is a command that grants group read permission to the file customers:

```bash
chmod g+r customers
```

It is also possible to deny permissions with a symbolic string. The following command denies the group and others write and execute permissions for the file account_info.

```bash
chmod go-wx account_info
```

See Appendix B, “The UNIX Command Syntax Guide to the Linux Shell and Utility Programs,” for a brief description of the chmod command.

Rolfe wants all users to have access to the corp_phones file. To make that possible, he asks you to change the file permissions. First, permit access to your home directory. Next, allow access to the corp_db directory, and then set the permissions for everyone to read the corp_phones file. You can use the chmod command with the x argument to grant access to directories.
