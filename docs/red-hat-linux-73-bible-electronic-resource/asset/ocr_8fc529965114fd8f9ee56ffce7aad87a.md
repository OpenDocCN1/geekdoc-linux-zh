+   1. First, go to your home directory. To do this, simply type `cd`. (For other ways of referring to your home directory, see the sidebar on identifying directories.)
+   2. To make sure that you got to your home directory, type `pwd`. When I do this, I get the following response (yours will reflect your home directory):

```
$ pwd
/home/chris
```

+   3. Create a new directory called `test` in your home directory, as follows:

```
$ mkdir test
```

+   4. Check the permissions of the directory by typing:

```
$ ls -ld test
drwxr-xr-x  2 chris sales  1024  Jan 24 12:17 test
```

Notice that this listing says that `test` is a directory (d), the owner is `chris`, the group is `sales`, and the file was most recently modified on Jan 24 at 12:17 p.m. Suppose that you want to prevent everyone else who uses this computer from using or viewing the files in this directory. The permissions for the directory are `rwxr-xr-x`. I explain what these permissions mean later in this section.

+   5. For now, type the following:

```
$ chmod 700 test
```

This changes the permissions of the directory to give you complete access and everyone else no access at all. (The new permissions should read like `rwx------`.)

+   6. Next, make the `test` directory your current directory as follows:

```
$ cd test
```

# Using metacharacters and operators

To make more efficient use of your shell, the bash shell lets you use certain special characters, referred to as metacharacters and operators. Metacharacters can help you match one or more files without typing each file out completely. Operators let you direct information from one command or file to another command or file.