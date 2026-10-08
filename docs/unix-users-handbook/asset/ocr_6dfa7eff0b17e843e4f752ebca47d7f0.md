# **cd** - Change to a new current directory.

Arguments

none Change to home directory. This is defined by the HOME environment variable

.. The two dot notation moves you to the parent directory of your current directory.

path You can specify either an absolute or relative path to change to.

# **pwd** - Present Working Directory, so you know your current location.

Examples

```
```
$ pwd
/home/denise/.netscape-cache
$ cd ..
$ pwd
/home/denise
$ 
```
```

# chmod

The chmod command is used to change the permissions on a file. Let’s start our discussion of **chmod** with the listing of the file sort shown earlier:

```
```
$ ls -l sort
-rwxr-x--x  1 marty    users      120 Jul 26 10:20 sort
```
```