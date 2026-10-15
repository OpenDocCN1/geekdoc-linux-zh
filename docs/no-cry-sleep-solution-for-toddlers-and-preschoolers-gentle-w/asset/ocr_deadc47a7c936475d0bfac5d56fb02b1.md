can be said to have its own unique path. The actual name by which the system identifies a directory always begins with the root directory and consists of all directories nested above that directory.

In Linux, you write a pathname by listing each directory in the path separated by a forward slash. A slash preceding the first directory in the path represents the root. The pathname for the robert directory is /home/robert. The pathname for the reports directory is /home/chris/reports. Pathnames also apply to files. When you create a file within a directory, you give the file a name. The actual name by which the system identifies the file, however, is the filename combined with the path of directories from the root to the file’s directory. In Figure 10-3, the path for the weather file consists of the root, home, and chris directories and the filename weather. The pathname for weather is /home/chris/weather (the root directory is represented by the first slash).

Pathnames may be absolute or relative. An absolute pathname is the complete pathname of a file or directory beginning with the root directory. A relative pathname begins from your working directory: it is the path of a file relative to your working directory. The working directory is the one you are currently operating in. Using the directory structure described in Figure 10-3, if chris is your working directory, the relative pathname for the file monday is reports/monday. The absolute pathname for monday is /home/chris/reports/monday.

The absolute pathname from the root to your home directory could be especially complex and, at times, even subject to change by the system administrator. To make it easier to reference, you can use a special character, the tilde ~, which represents the absolute pathname of your home directory. In the next example, from the thankyou directory, the user references the weather file in the home directory by placing a tilde and slash before weather.

```
$ pwd
/home/chris/letters/thankyou
$ cat ~/weather
raining and warm
$
```

You must specify the rest of the path from your home directory. In the next example, the user references the monday file in the reports directory. The tilde represents the path to the user’s home directory, /home/chris, and then the rest of the path to the monday file is specified.

```
$ cat ~/reports/monday
```

# System Directories

The root directory that begins the Linux file structure contains several system directories. The system directories contain files and programs used to run and maintain the system. Many contain other subdirectories with programs for executing specific features of Linux. For example, the directory /usr/bin contains the various Linux commands that users execute, such as cp and mv. The directory /bin holds interfaces with different system devices, such as the printer or the terminal. Table 10-1 lists the basic system directories.