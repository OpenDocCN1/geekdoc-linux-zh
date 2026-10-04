# Setting Aside Space (for Fedora Core)

do need to defragment your hard disk to make room for Fedora Core. What defragmenting does is move all the files to the beginning of the partition and pack them tight. The result is free space at the end of the partition, so the partition can be shrunk without destroying any data.

To defragment the hard disk, follow these steps:

+   1. Double-click My Computer from the desktop, right-click the disk icon, and then select Properties from the pop-up menu.

+   2. In the Properties window, click the Tools tab and then click the Defragmentment Now button.

+   3. Wait. Wait and wait.

You hear lots of noise from the disk drive while it moves files around. After a couple of hours, the defragmenting completes.

There are some gotchas with these instructions. First, don't use your PC or other programs while defragmenting the hard disk. Close all programs, including ones in the system tray. One good way to do this is to press Ctrl+Alt+Del (which calls the Task Manager), select program you want to stop, and then click the End Task button.

The second gotcha is that the defragment does not move hidden files — plenty of such files are in your system. You don't see them in the folders because (what?) they are hidden. You may have to manually find the hidden files and see whether you can delete the ones that seem to be junk. (Don't worry, a how-to is coming up.)

![](bbox=[0.113, 0.406, 0.203, 0.492])

You can find all the hidden files in your PC with a simple command. Open a Command Prompt and type the following commands:

```
cd \
ndir /a:s > hidden.txt
```

After the command finishes, you have a list of all hidden files in the text file hidden.txt. Open the file in Microsoft Word or just type edit hidden.txt to view that file in an editor. When I tried this, I noticed a lot of files with names ~WRL0004.TMP — and clearly seemed to be temporary, created by some Microsoft software (probably Word). Why are they hidden? Anyway, I had to change the file attribute using MS-DOS incantations like ATTRIB -H ~WRL0004.TMP and typing ERASE ~WRL0004.TMP to finally delete the file. I had to repeat this command for many junk files. But it's worth taking your time and doing it carefully!

![](bbox=[0.113, 0.568, 0.203, 0.654])