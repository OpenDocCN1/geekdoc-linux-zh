
## Symbolic Links

As we look around, we are likely to see a directory listing (for example, /lib) with an entry like this:

```
lrwxrwxrwx 1 root root  11 2018-08-11 07:34 libc.so.6 -> libc-2.6.so
```

Notice how the first letter of the listing is l and the entry seems to have two filenames? This is a special kind of a file called a symbolic link (also known as a soft link or symlink). In most Unix-like systems, it is possible to have a file referenced by multiple names. While the value of this might not be obvious, it is really a useful feature.

Picture this scenario: a program requires the use of a shared resource of some kind contained in a file named “foo,” but “foo” has frequent version changes. It would be good to include the version number in the filename so the administrator or other interested party could see what version of “foo” is installed. This presents a problem. If we change the name of the shared resource, we have to track down every program that might use it and change it to look for a new resource name every time a new version of the resource is installed. That doesn’t sound like fun at all.

Here is where symbolic links save the day. Suppose we install version 2.6 of “foo,” which has the filename “foo-2.6,” and then create a symbolic link simply called “foo” that points to “foo-2.6.” This means that when a program opens the file “foo,” it is actually opening the file “foo-2.6.” Now everybody is happy. The programs that rely on “foo” can find it, and we can still see what actual version is installed. When it is time to upgrade to “foo-2.7,” we just add the file to our system, delete the symbolic link “foo,” and create a new one that points to the new version. Not only does this solve the problem of the version upgrade, it also allows us to keep both versions on our machine. Imagine that “foo-2.7” has a bug (damn those developers!), and we need to revert to the old version. Again, we just delete the symbolic link pointing to the new version and create a new symbolic link pointing to the old version.

The directory listing at the beginning of this section (from the /lib directory of a Fedora system) shows a symbolic link called libc.so.6 that points to a shared library file called *libc-2.6.so*. This means that programs looking for *libc.so.6* will actually get the file *libc-2.6.so*. We will learn how to create symbolic links in the next chapter.

## Hard Links

While we are on the subject of links, we need to mention that there is a second type of link called *hard links*. Hard links also allow files to have multiple names, but they do it in a different way. We’ll talk more about the differences between symbolic and hard links in the next chapter.

## Summing Up

With our tour behind us, we have learned a lot about our system. We’ve seen various files and directories and their contents. One thing you should take away from this is how open the system is. In Linux there are many important files that are plain human-readable text. Unlike many proprietary systems, Linux makes everything available for examination and study.

## 4

## MANIPULATING FILES AND DIRECTORIES

![](img/314a0280bc10c5c0d45be132de172677_63_0.png)

At this point, we are ready for some real work! This chapter will introduce five of the most frequently used Linux commands. The following commands are used for manipulating both files and directories:

- `cp` Copy files and directories
- `mv` Move/rename files and directories
- `mkdir` Create directories
- `rm` Remove files and directories
- `ln` Create hard and symbolic links

Now, to be frank, some of the tasks performed by these commands are more easily done with a graphical file manager. With a file manager, we can drag and drop a file from one directory to another, cut and paste files, delete files, and so on. So why use these old command line programs?

The answer is power and flexibility. While it is easy to perform simple file manipulations with a graphical file manager, complicated tasks can be easier with the command line programs. For example, how could we copy all the HTML files from one directory to another but copy only files that do not exist in the destination directory or are newer
