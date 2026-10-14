program to use gzip to compress the folder. For example, to create a compressed version of your Documentia folder, which we’ll call tightdocs.tar.gz, you would type the following and press ENTER:

```
tar -czvf tightdocs.tar.gz Documentia
```

It’s worth mentioning at this point that you may also come across some files compressed with the bzip program. Such files are recognizable by some variation on the .bz or .bz2 file extension. Dealing with these files should pose no problem, because the commands are almost identical to those for gzip. Just substitute -j for -z in the command string.

# Compressing and Extracting Compressed Single Files

If you want to compress or decompress a single file, you don’t really need to use the tar program at all, since its purpose is to create archives consisting of several files. You can instead use the gzip and gunzip commands directly. For example, to compress a file called matilda.png, you would type gzip matilda.png and press ENTER. The matilda.png file would then become matilda.jpg.gz. To decompress the file, you would type gunzip matilda.jpg.gz and press ENTER, after which the matilda.jpg file would be back to normal.

So, can you compress an archive you’ve already created with the tar command? Sure. For example, to compress the spicyfood.tar archive mentioned earlier, you would type gzip spicyfood.tar, and voilà—you’ve got yourself a compressed spicyfood.tar.gz archive. Pretty cool, don’t you think?

# Project 9A: Creating a Plan

Now that you have a bit of command experience, it’s time to get some practice and put all those commands to good use. In this project, you’ll start off easy by creating a .plan file, like the one mentioned earlier in the chapter.

The actual .plan file is a hidden file (as you can see by the dot before its name), which contains the plan or message that you add to that file. That message will appear in the output of someone’s Terminal when they use the finger command to find out more about you. You may not need such a .plan file, but it is an easy enough way to get started working a bit more with commands and the Terminal itself, so let’s give it a try.