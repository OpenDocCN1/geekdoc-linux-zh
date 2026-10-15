```
$ ls -F
weather reports/ letters/
```

The ls command also takes as an argument any directory name or directory pathname. This enables you to list the files in any directory without first having to change to that directory. In the next example, the ls command takes as its argument the name of a directory, reports. Then the ls command is executed again, only this time the absolute pathname of reports is used.

```
$ ls reports
monday tuesday
$ ls /home/chris/reports
monday tuesday
$
```

# Moving Through Directories

The cd command takes as its argument the name of the directory to which you want to change. The name of the directory can be the name of a subdirectory in your working directory or the full pathname of any directory on the system. If you want to change back to your home directory, you only need to enter the cd command by itself, without a filename argument.

```
$ cd props
$ pwd
/home/dylan/props
```

# Referencing the Parent Directory

A directory always has a parent (except, of course, for the root). For example, in the preceding listing, the parent for thankyou is the letters directory. When a directory is created, two entries are made: one represented with a dot (.), and the other represented by double dots (..). The dot represents the pathnames of the directory, and the double dots represent the pathname of its parent directory. Double dots, used as an argument in a command, reference a parent directory. The single dot references the directory itself.

You can use the single dot to reference your working directory, instead of using its pathname. For example, to copy a file to the working directory retaining the same name, the dot can be used in place of the working directory's pathname. In this sense, the dot is another name for the working directory. In the next example, the user copies the weather file from the chris directory to the reports directory. The reports directory is the working directory and can be represented with the single dot.

```
$ cd reports
$ cp /home/chris/weather .
```

The .. symbol is often used to reference files in the parent directory. In the next example, the cat command displays the weather file in the parent directory. The pathname for the file is the .. symbol followed by a slash and the filename.

```
$ cat ../weather
raining and warm
```