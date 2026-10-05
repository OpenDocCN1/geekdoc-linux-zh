# DIRECTORY ACCESS PERMISSIONS

Access permissions have slightly different meanings when they are used with directories. Although the three types of users can read from or write to a directory, the directory cannot be executed. Execute permission is redefined for a directory: It means that you can cd into the directory and/or examine files that you have permission to read from the directory. It has nothing to do with executing a file.

When you only execute permission for a directory, you can use ls to list a file in the directory if you know its name. You cannot use ls without an argument to list the entire contents of the directory. In the following exchange, Zach first verifies that he is logged in. He then checks the permissions on Max's info directory. You can view the access permissions associated with a directory by running ls -d (directory) and -l (long) options:

```
$ who am i
z pts/7 Aug 21 10:02
$ ls -l /home/max/info
drwx------ 2 max pubs 512 2010-08-21 09:31 /home/max/info
$ ls -l /home/max/info
ls: /home/max/info: Permission denied
```

The d at the left of the line that ls indicates that /home/max/info is a directory. Max has read, write, and execute permissions; members of the group have no access permissions, and other users have execute permission only, indicated by the x at the right end of the permissions. Because Zach does not have permission for the directory, the ls -l command returns an error.

When Zach specifies the names of files he wants information about, he is not reading new information but rather searching for specific information, he is allowed to do with access to the directory. Max has read permission for notes so he has no problem using cat to display the file. He cannot display financial because he does not have read permission for it:

```
$ ls -l /home/max/financial /home/max/notes
-rw-r---- 1 max pubs 34 2010-08-21 09:31 /home/max/info/financial
-rw-r--r-- 1 max pubs 30 2010-08-21 09:32 /home/max/info/notes
$ cat /home/max/info/notes
cat: /home/max/info/financial: Permission denied
```

Next Max gives others access to his info directory:

```
$ chmod o+r /home/max/info
```

When Zach checks his permissions on info, he finds that he has both read and execute access to the directory. Now ls -l works fine without arguments, but he still cannot read financial. (This restriction is an issue of file permissions, directory permissions.) Finally, Zach tries to create a file newfile using touch.