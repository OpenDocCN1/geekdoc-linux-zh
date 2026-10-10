Many items in NOTES refer to a mysterious thing called LINT. This is an old, deprecated (pre-5.0) way of looking at what is now the NOTES file. LINT was named after the lint command— a C-code debugging utility that's named for the fact that it validates the code you run it on by removing excess lint and fuzz from it. This piece of naming trivia is weird but true (and also not particularly useful or important). One of the long-running ideals (or myths) about FreeBSD is that it offers the capability to build a kernel based on the LINT file, incorporating every possible supported option and driver. This capability is almost certainly not possible, because many of the kernel options are mutually exclusive or unstable. FreeBSD does, however, provide the capability to generate an old-style LINT file by running make LINT from within the directory. This strips out all comments and hint. lines, and creates a kernel config file that you can theoretically use to build a really huge, all-encompassing kernel that probably won't have a chance of booting or even compiling.

# Creating a Custom Kernel Configuration File

Here's where we actually begin the process of creating a new kernel. Remember that you don't want to modify the GENERIC file itself; it gets updated with the system sources every time you synchronize or upgrade. Therefore, to make sure your changes don't get overwritten, make a copy of GENERIC to use as your custom kernel config. The name for the copy should be a single word in all caps, according to tradition. The custom kernel for this example is called CUSTOM:

```
# cp GENERIC CUSTOM
```

You can now modify the CUSTOM file all you like. The first thing you should do is go through it and change every mention of GENERIC to CUSTOM (or whatever name you chose). You also should remove redundant entries for cpu and, if necessary, modify the value of maxusers (see the following note). Here is a block from a customized kernel config on a Pentium III-class machine operating as a high-profile server:

```
machine I386
cpu I686_CPU
ident CUSTOM
maxusers 64
```

> **NOTE**
> 
> Don't be fooled by the maxusers setting: It doesn't actually limit the number of current logins the system will support. (That limit is controlled by the device pty <num> line.) What maxusers does is much more subtle: A number of internal table sizes are derived from it, such as the maximum number of processes allowed (16 times the maxusers setting, plus 20) and several others. Set maxusers to approximately what you expect the average number of users to be, but don't set it lower than 4 because you'll run out of processes quicker than you expect.