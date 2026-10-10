# MEMORY HOGS

If you need to see what apps are consuming the most memory on Linux, simply enter:

```
ps aux | sort -rnk 4
```

This sorts the output by system memory use.

![](bbox=[0.08, 0.25, 0.49, 0.42])

# BBS

Back in the days of dial-up connections, the online world was made up of Bulletin Board Systems. These remote servers provided hang-outs for users to chat, swap code, play games and more. Using telnet in Linux, we can still connect to some active BBSes:

```
telnet battletestarbs.dynDNS.org
```

There are countless operational BBSes available, check out [https://www.telnetbbsguide.com/bbs/list/detail/](https://www.telnetbbsguide.com/bbs/list/detail/), for more.

![](bbox=[0.53, 0.3, 0.78, 0.42])

# SHREDDER

When you delete a file, there’s a chance of someone with the right software being able to retrieve it. However, to securely and permanently delete a file, use Shred:

```
shred -zvu NAMEOFFILE.txt
```

Replace NAMEOFFILE with the name of the file to delete.

![](bbox=[0.08, 0.59, 0.49, 0.72])

# DIRECTORY TREES

If you want to create an entire directory (or folder) tree with a single command, you can use:

```
mkdir -p New-Dir/ {subfolder1,subfolder2,subfolder3,subfolder4}
```

This creates a New-Dir with four sub folders within.

![](bbox=[0.53, 0.59, 0.92, 0.72])

# ASCII ART

ASCII art can be quite striking when applied to some images. However, it’s often difficult to get just right. You can create some great ASCII art from the images you have using img2txt:

```
img2txt NAMEOFIMAGEFILE.png
```

Replace NAMEOFIMAGEFILE with the actual name of the image file on your system. if img2txt install not installed, use:

```
sudo apt-get install caca-utils.
```

![](bbox=[0.25, 0.86, 0.49, 0.94])

# FORGOTTEN COMMANDS

It’s not easy trying to remember all the available Linux commands. Thankfully, we can use apropos to help us. Simply use it, along with a description of the command:

```
apropos "copy files"
apropos "rename files"
```

![](bbox=[0.53, 0.86, 0.92, 0.94])