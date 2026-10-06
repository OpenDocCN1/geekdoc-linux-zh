# Chapter 1 A Quick Review of the Basics

Let's see how symbolic links work with the previous example:

```
$ rm wb
$ ls -l
total 4
-rwxr-xr-x 1 pat DP3822 1358 Jan 15 11:01 lcat
-rwxr-xr-x 1 pat DP3822 504 Apr 21 18:30 xtr
$ ls -s /users/steve/wb/ .symwb
$ ls -1
total 5
-rwxr-xr-x 1 pat DP3822 1358 Jan 15 11:01 lcat
-rwxr-xr-x 1 pat DP3822 15 Jul 20 15:22 symwb -> /users/steve/wb
-rwxr-xr-x 1 pat DP3822 504 Apr 21 18:30 xtr
$
```

Note that pat is listed as the owner of symwb, the file type as the first character in the ls output is 1, which indicates a symbolic link. The size of the symbolic link is 15 (the file actually contains the string /users/steve/wb), but if we attempt to access the contents of the file, we are presented with the contents of file it linked to, /users/steve/wb:

```
$ wc symwb
5 9 89 symwb
$
```

The -l option to the ls command was used with the -1 option to get a detailed list of information on the file symbolic link points to:

```
$ ls -L1
total 5
-rwxr-xr-x 1 pat DP3822 1358 Jan 15 11:01 lcat
-rwxr-xr-x 2 steve DP3725 89 Jun 25 23:30 wb
-rwxr-xr-x 1 pat DP3822 504 Apr 21 18:30 xtr
$
```

Removing the file that a symbolic link points to invalidates the symbolic links are maintained as filenames, but it doesn't remove it:

```
$ rm /users/steve/wb
$ ls -1
total 5
-rwxr-xr-x 1 pat DP3822 1358 Jan 15 11:01 lcat
-rwxr-xr-x 1 pat DP3822 15 Jul 20 15:22 wb -> /users/steve/wb
-rwxr-xr-x 1 pat DP3822 504 Apr 21 18:30 xtr
$ wc wb
$
```

> Assume pat can remove this file

Cannot open wb: No such file or directory
$