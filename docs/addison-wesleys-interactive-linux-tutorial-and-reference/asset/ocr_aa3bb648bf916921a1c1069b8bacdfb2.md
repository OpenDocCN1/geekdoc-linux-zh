Your screen will look similar to Figure 6-22.

```
$ ls -l /home/sam4
drwxr-xr- 1 sam4 users 1024.. accounts
drwxr-xr- 1 sam4 users 1024.. practice
drwxr-xr- 1 sam4 users 1024.. webstuff
$
```

![](bbox=[0.33, 0.28, 0.76, 0.3])

> On some systems, the home account may be in some directory other than **/home**. For example, in the link exercises that you have just completed, you might have to type **/accounts/sam4** or **/users/sam4** to reflect the correct users directory on your system.

Our concern at the moment is the file mode, represented by these characters in Figure 6-22: **rwxr-xr-**. We presented an overview of the file mode in the previous module, *Linux Directories*, of the CBT course, and we will go into the file mode in depth in the module entitled *Security*.

For our present purposes, we will point out that when you create a link to a file, you are creating a link *to* a file that is *in* a directory. There are specific permissions required for both the file and the directory if you are to be able to both create the link *and* read the file. We will show you what the permissions must be and how to change them if necessary. But we will refer you to the *Security* module of the *Linux Made Easy CBT* and the corresponding Security chapter in this guide for detailed explanations about file mode and permissions.