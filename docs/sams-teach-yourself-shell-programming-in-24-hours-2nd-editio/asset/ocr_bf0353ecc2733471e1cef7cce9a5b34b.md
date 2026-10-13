```
$ pwd
/home/ranga
```

Here, we tried to change into the directory final_exam_answers, a directory that did not exist, thus cd reported an error. The final pwd command shows that the working directory did not change.

# Listing Files and Directories

In Chapter 3, "Working with Files," you looked at using the ls command to list the files in the current directory. Now let's look at using the ls command to list the files in any directory.

# Listing Directories

To list the files in a directory, you can use the following syntax:

```
ls dir
```

Here, dir is the absolute or relative pathname of the directory whose contents you want listed.

For example, both of the following commands will list the contents of the directory /usr/local (assuming that the working directory is /home/ranga):

```
$ ls /usr/local
$ ls ../.. /usr/local
```

On my system, the listing resembles

```
X11    bin    gimp    jikes    sbin
ace    doc    include    lib    share
ataik  etc    info    man    turboj-1.1.0
```

The listing on your system might look quite different.

You can use any of the options you covered in Chapter 3 to change the output. For example, the command

```
$ ls -aF /usr/local
```

produces the output

```
../    stalk/    gimp/    lib/    turboj-1.1.0/
./    bin/    include/    man/
X11/    doc/    info/    sbin/
ace/    etc/    jikes/    share/
```

You can also specify more than one directory as an argument. For example,

```
$ ls /home /usr/local
```