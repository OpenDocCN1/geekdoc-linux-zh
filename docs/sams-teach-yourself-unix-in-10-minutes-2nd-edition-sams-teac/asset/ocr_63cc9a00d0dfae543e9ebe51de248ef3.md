```
> pwd
/priv/home/rob/temp/newwebsite/
> ls
cgi_bin index.html
images vrml
```

This example is based on the assumption that I switched into the new directory I (newwebsite) before issuing the pwd command. Then, by issuing the ls command, I got the file listing for that directory, which includes a new HTML page I created called index.html. Now, you try it. Attempt to determine where you are currently by checking your working directory, and then list the files and other directories from your current location. As we progress we will learn how to change directories, but for now, remember that this lesson is directed towards the Unix learner. If you know where you are in the Unix operating system, you don't need to issue the pwd command before listing files.

As mentioned earlier, if you are interested in listing files that are in another directory and you don't know how to change into that directory, you can easily solve this problem using the ls <directory name> command. You can use the root directory we just learned about your example. Because your current directory should be your home directory, you can list the files and directories in root by doing the following:

```
ls /
CDROM lib
bin priv
core tmp
dev temp
etc usr
include var
```

In this example, I have verified that all the data listed in the root directory are directories. This information may or may not be common knowledge, so if you are unsure, verify it with a command!

The ls command with the “long” option to ask Unix for more information in the listing. By issuing the command ls -1 <directory name>, you can view example of the root directory in a whole different light: