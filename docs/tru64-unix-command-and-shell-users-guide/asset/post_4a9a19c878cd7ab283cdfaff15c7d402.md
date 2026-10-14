
```
$ umask 037
```

This command establishes a permission code of 740 (if the file is executable) and produces the following results:

- You (the owner) are allowed all permissions.
- Members of your group are not allowed write and execute permissions.
- All others are not allowed any permissions.

Further, assume that you have just created a file. By default, your editor always assigns the following default permissions: owners are allowed all permissions, and all others only read and execute permissions. However, since you have previously set a user mask of 037, it further restricts the file permissions. As a result, the owner still has all permissions, but the group cannot execute the file, and all others have no permissions.

## 5.5.1 Setting the umask

You may activate the umask command in two ways:

- Include the umask command in your login script. This is the most common and efficient way to specify your user mask because the specified value is set automatically for you whenever you log in. For a discussion of login scripts, see Chapter 7. For examples of umask commands in login scripts, see Chapter 8.
- Enter the umask command at the shell prompt during a login session. The user mask value you set is in effect for that login session only.

For a more detailed example of how the user mask works in restricting permissions for files you create with a text editor, follow the steps in this procedure:

- 1. Enter the following command to find out what the current value of your user mask is:

```
$ umask
```

If the user mask value is 000, there are no restrictions on the permissions established by file-creating programs. Go to step 3.

If the user mask value is set, write it down. Go to step 2.

- 2. Set the user mask value to 000 so that there will be no restrictions on the permissions established by file-creating programs. Before resetting the user mask, make sure you have written down the current value in case you need to reset it.

Enter the following command:

```
$ umask 000
```

- 3. Create a file, save it, and then exit your editor.
- 4. Display the permissions of the file by using the ls -l command. We will assume that read/write permissions are granted for all users:

```
$ ls -l
-rw-rw-rw- 1 user-name 15 Oct 27 14:42 yourfile
$
```

5. Reset the user mask to 022 by entering the following command:

```
$ umask 022
```

A user mask of 022 establishes the following permission restrictions: owners are allowed all permissions and all others are allowed only read and execute permissions.

- 6. Create another file, save it, and then exit your editor.

7. Display the permissions of the file by entering the ls -l command:

```
$ ls -l
-rw-r--r-- 1 user-name 15 Oct 27 14:45 yourfile2
$
```

The write permissions for the group and all others have been removed in accordance with the user mask value of 022.

8. Reset the user mask to its original value or to another value (if you choose).

### Note

> A user with superuser privileges can override whatever access restrictions you impose on files and directories. For more information on this topic, see Section 5.7.

On occasion, the results you obtain when specifying a user mask may vary from what you intended. If so, see your system administrator.

The operating system provides a default user mask value of 022, which allows the owner all permissions, but prevents members of your group or any other users from writing to your files. However, your system's user mask default may vary.

## 5.6 Changing Your Identity to Access Files

The su command lets you alter your identity during a login session. A reason for altering your identity is to be able to access files that you do not own. To protect system security, you should not assume another identity without the owner's or the system administrator's permission.

The su command lets you log in to another user's account only if you know that user's password. The su command authenticates you and then resets both the process's user ID and the effective user ID to the value of the newly
