
2 bits to be on, or rw (read and write). If you see a file that is set to 666, that equates to all three trios having the same permissions—read and write.

> Watch for questions that try to trick you with a user who's both the user owner and a member of the group owner, but the correct permissions for executing or changing the file aren't in a single trio. You can't mix the trios, even if your profile encompasses several of the trios.

For example, say a user named fred is the user owner of the file object `/home/fred/22AcaciaAvenue.mp3` and is also a member of the group owner of that object. The file's listing has the following permissions set:

```
-rw-r-xr-x 2 fred users 0 Jan 26 13:08 22AcaciaAvenue.mp3
```

fred's permissions might seem to span the various trios, but because fred is the user owner, he matched the first trio and stopped there.

## Manipulating Permissions

`chmod` is the command to use when modifying or altering an object's permission trio bits. Only the root and object owners can alter permissions.

The two modes of manipulating the permissions for an object are numeric and symbolic. Both modes have their place, and if there were only one mode, someone would have to invent the other, just for variety.

### Numeric Mode

Numeric permissions are the most often used, and they appear on the exam with greater frequency than the symbolic style. As a rule, I recommend using the numeric mode to set or force permissions on an object. For example, if you are told that the current permissions for an object are 644 and you are asked to ensure that all users have read and write access to that object, you can assume that the numeric style is correct, as shown here:

```
chmod 666 file
```

The `chmod` command works great on groups of files, too:

```
chmod 644 /home/lukec/*.txt
```

It even works on directories and their contents. For example, say the user `bertrand` has a home directory he inherited from someone else and a few files are not set properly to be readable only by him. He asks you to set all the files in his home directory to 640 for security's sake and to give him read/write access to them. You might use the command:

```
chmod -R 640 /home/bertrand/*
```

Take a moment to understand why this command works the way it does. The `chmod` command has an `-R` recursive option that affects the object named and all its child objects. However, `bertrand` didn't ask you to change his home directory and all the contents, but just the contents, which is why the slash and asterisk characters are on the end of the target. This command acts on the entire *contents* of `bertrand`'s home directory but leaves the directory alone.

The `chmod` command has surprisingly few options:

- `-c`—Reports only changed files
- `-v`—Reports all files
- `-n`—Changes symbolic links, not the original file
- `-f`—Suppresses error messages
- `-R`—Operates recursively through directories

![img](img/49f4f38f3aec011238fa50f89e643db3_197_0.png)

> The `chmod` command's recursive option is an uppercase `R`, not a lowercase `r` as in some other commands. Familiarize yourself with the case of the various command options, and you will be fine.

### Symbolic Mode

When using `chmod` with symbolic values, keep in mind that you can force the permissions like the numeric mode, but a much longer command results. The primary reason to use symbolic mode is to affect, or alter, permissions rather than to set or overwrite them.

The symbolic mode uses a letter to identify the trios (user `u`; group `g`; other `o`; and all `a`), a qualifier (`+`, `-`, or `=`), and then the permissions being altered or set (`r` = read; `w` = write; and `x` = execute).

To use the symbolic values to set permissions, you can do them all at once, like so:

```
chmod a=rwx file
```

This produces permission trios that are set to `-rwxrwxrwx`.

Or you can use each one of the identifiers with its qualifier and permissions separated by commas:

```
chmod u=rw,g=rx,a=
```

This produces a file that has its permissions set to `-rw-r-x___`.

## TIP

This method of using the symbolic mode is viewed as unwieldy and somewhat inelegant for constant use. Use symbolic mode when you want to tune up the permissions, not set them initially.

To change just the user owner’s permissions to rwx, you would use the following command:

```
chmod u=rwx mystuff
```

To change the group owner’s permissions to r-x, you would use the command shown here:

```
chmod g=r+x mystuff
```

To change the other or everyone permissions to r, you would use this command:

```
chmod o=r mystuff
```

## ALERT

On the exam the idea is to get the question answered, so if it’s a multiple-choice question and you’re sure something will work on the command line, that’s probably the answer. Watch out for the fill-in-the-blank answers because you don’t get any partial credit. What’s typed is checked against a table of possible correct answers, but it must be executable on the command line and work to be right.

Setting a file to be executable, without knowing its other permissions, can be done several ways.

For example, if you know a file exists but don’t know the permissions and you are told to make sure it’s executable by all permission trios, you would use the following command:

```
chmod a+x file1
```

Alternatively, you can leave the `a` off and get all the trios by default:

```
chmod +x file1
```

## User and Group Ownership

To set the stage for the `chown` and `chgrp` commands, let’s review how users and groups are set to function on a Linux machine. Changing user owner and group owner for objects can be frustrating unless you understand some ground rules about how Linux sets the ownership for objects:

- A user has two types of groups associated with her: The primary group is the one whose GID appears in the user’s `/etc/passwd` entry.
- Users can be members of other groups via entries in the `/etc/group` file. These group memberships are called *secondary groups*.
- If a user has a group set as her primary group, she doesn't have to be physically listed as a group member in the `/etc/group` file. The primary group setting acts as a full membership option, too.
- When a user creates an object, her primary group GID/name is set as the group owner by default.
- Changing a user's primary group doesn't automatically update any of the owned objects and can cause problems if that user isn't a member of the new group owner for the object.

### Changing Ownership

The `chown` command is used to set the user owner, group owner, or a combination of the two with one command.

The format for the `chown` command is:
`chown [options] user:group object`

The `chown` command accepts both of the following commands as valid:

```
chown snuffy:users file1
chown snuffy.users file1
```

In addition, you can use the following syntax with `chown`:

- `owner`—Changes only the owner
- `owner:group`—Changes both the owner and group
- `owner:`—Changes the owner and sets the group to the login or primary group of the user
- `:group`—Changes only the group and leaves the owner unaffected

Let's say that the user `snuffy` has the primary group of `users` and a secondary group membership of `accounting`. By default, every object `snuffy` creates on the system will have `snuffy` as the user owner and `users` as the group owner. This can cause problems in shared directories, and it often does. (Later in the chapter, we'll discuss the SUID or SGID, which can make shared directories more palatable.)

If snuffy visits a shared directory whose ownership is set to root/accounting and creates a file named `snuffysexpenses.txt`, that file will be inaccessible to any of the other users who share that directory unless they are also members of the group `users`. Say the user `martha` does expenses and needs to have ownership of the file.

To change the file snuffy created to be owned by `martha/accounting`, you would use this command:

```
chown martha:accounting snuffysexpenses.txt
```

Let's say that now the file needs to be owned by another user who cuts the checks, `fluchre`, so you can just change the user owner without having to bother with the group, which will be unaffected:

```
chown fluchre snuffysexpenses.txt
```

If, for some reason, you decide that an entire directory tree of files needs to have its ownership changed, you can do so at one time with the following command:

```
chown -R root:accounting /accounting
```

### Changing Group Ownership

When just the group owner needs to be changed, the simplest method is to use the `chgrp` command. The syntax of the command is very straightforward:

```
chgrp newgrp file1
```

Changing a large set of files to another group owner requires the use of the `-R` recursive option:

```
chgrp -R newgrp /data/*
```

The previous command changes just the contents of the `/data` directory to the group owner `newgrp` but leaves the user owner alone.

Options for the `chgrp` command include:

- `-c`—Shows a line of output only for changed objects
- `-h`—Changes symbolic links, not the original file
- `-R`—Recursively affects the target and all children
- `-v`—Shows a line of output for every object, regardless of the actions performed on the object
