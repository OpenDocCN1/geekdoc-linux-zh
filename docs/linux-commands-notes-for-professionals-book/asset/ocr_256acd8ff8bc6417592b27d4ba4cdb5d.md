See what files are in your current working directory:

```
ls
```

Create an empty directory called `myFirstDirectory`:

```
mkdir myFirstDirectory
```

Create multi path directory: (creates two directories, src and myFirstDirectory)

```
mkdir -p src/myFirstDirectory
```

Move the file into the directory:

```
mv myFirstFile myFirstDirectory/
```

You can also rename the file:

```
user@linux-computer:~$ mv myFirstFile secondFileName
```

Change the current working directory to `myFirstDirectory`:

```
cd myFirstDirectory
```

Delete a file:

```
rm myFirstFile
```

Move into the parent directory (which is represented as `..`):

```
cd ..
```

Delete an empty directory:

```
rmdir myFirstDirectory
```

Delete a non-empty directory (i.e. contains files and/or other directories):

```
rm -rf myFirstDirectory
```

> *Make note that when deleting directories, that you delete `.` / not `/` that will wipe your whole filesystem.*

# ## Section 1.7: File/Directory details

The `ls` command has several options that can be used together to show more information.

# **Details/Rights**

The `l` option shows the file permissions, size, and last modified date. So if the root directory contained a dir called `test` and a file `someFile` the command: