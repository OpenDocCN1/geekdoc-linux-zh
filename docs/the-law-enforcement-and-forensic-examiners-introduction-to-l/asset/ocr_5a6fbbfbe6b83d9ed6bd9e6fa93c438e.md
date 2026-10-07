# A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

![](bbox=[0.353, 0.133, 0.701, 0.342])

Illustration 4: Ouptut of xv ouchy.dat

Close the image with your mouse, or use the ctrl-c key combo from the command line to kill the program.

One neat trick you can do if you have a handful of picture files in a directory you want to view without having to use a separate command for each is to use a bash loop. Scripting and bash programming are outside the scope of this document (for now), but this is a very simple loop that illustrates some powerful command line usage. This can be done all on one line, separating the individual commands with the <enter> makes it a bit more readable.

First, let's cd into the Pics/ directory under /mnt/evid, do a quick ls and see that we have a small directory with a few picture files (you can check this with file *). We then type our loop:

```
barry@forensic1:/mnt/evid$ cd Pics

barry@forensic1:/mnt/evid/Pics$ ls
C800x600.jpg* bike2.jpg* matrix3.jpg*
Stoppie.gif* bike3.jpg* muleweele.gif*

barry@forensic1:/mnt/evid/Pics$ for in ./* <enter>
> do
> xv pic <enter>
> done <enter>
```

The first line of a bash loop above means "for file in the current directory (.,/*), assign each file the variable name pic as we move through the loop". The second line is simply the bash keyword do. The third line executes xv the value of the pic variable ($pic) at each iteration of the loop, followed by the bash keyword done to close the loop. As you run the