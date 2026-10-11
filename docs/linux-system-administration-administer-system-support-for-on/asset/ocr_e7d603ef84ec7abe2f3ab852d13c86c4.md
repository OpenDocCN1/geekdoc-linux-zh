Default file permissions are **644**. These are set by the `umask`, more on the `umask` in a bit. We can remove all the permissions by issuing `chmod 000` or by the following:

```
$ chmod -rw test
----- 1 stripes users 0 Jul 19 15:09 test
```

If you want to give everyone a certain type of permission, you can use just the commands `+` or `a+x`.

```
$ chmod +x test
$ ls -l test
-x-x-x-x 1 stripes users 0 Jul 19 15:09 test
```

To set other's permissions only to read.

```
$ chmod o=r test
-x-x-xr-- 1 stripes users 0 Jul 19 15:09 test
```

To set the user's permissions to read, write, and execute.

```
$ chmod u=rwx test
$ ls -l test
-rwx-xr-- 1 stripes users 0 Jul 19 15:09 test
```

Be aware that execute does different things to files than directories. If you execute a file, you're assuming the file is either a script or an executable program. It also means you can change to the directory if you have execute permission on it. However, you will not be able to read it without read permissions.

For setting initial permissions, use `umask` in the `.profile` or `.cshrc` file. This will set default file permissions. Because it works in reverse of `chmod`, what you would do is subtract the `umask` bits from the octal permissions you want. When you do this, you'll need to remove the execute permissions from the hexadecimal notation you want. The `umask` only sets read and write bits on directories, not execute bits.

Say you want your files to have the default permission `600`. You would set your `umask` to `077`, like this:

```
$ umask 077
```

A good rule of thumb is to keep the first `umask` number always zero, this way you can have read and write permissions by default to your file. If you want everyone else (being groups and other) to have more permissions, decrease seven. A