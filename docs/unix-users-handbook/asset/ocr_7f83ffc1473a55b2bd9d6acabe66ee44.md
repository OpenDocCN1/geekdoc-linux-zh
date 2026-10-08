The *complement* of the umask field is "*anded*" with the default setting to change the **umask**. You can set **umask** by specifying its value. In our earlier example we viewed **umask** two different ways. To set the **umask**, you simply issue **umask** and the desired value. Setting **umask** to 022, for example, removes write permissions of directories for "group" and "other," as shown in Figure 7-6.

![](bbox=[0.05, 0.26, 0.9, 0.6])

**umask 022** changes the directory permissions to 755 in this example.

Similarly, a **umask** of 022 changes the default permission of 666 for files to 644, which is read-only for group and other.