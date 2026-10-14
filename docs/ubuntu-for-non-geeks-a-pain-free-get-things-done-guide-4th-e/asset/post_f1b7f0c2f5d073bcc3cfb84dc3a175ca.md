
To create an archive, you would simply type `tar -cvf`, followed by the name the final tarball will be, and then the name of the folder or file you are trying to archive. For example, let’s say you want to create an archive of your photos folder, and you want to call it `pics4pals`. In this case, you would type the following command and then press ENTER:

```
tar -cvf pics4pals.tar photos
```

As you no doubt noticed, there are some flags after the tar command in that string. The c tells the tar program to create a new archive. The v tells the program to be verbose, or, in other words, to tell you what it is doing in the Terminal as it is doing it. Finally, the f tells the program that what follows is the file information.

If, after creating the archive, you suddenly remember that there is one more file you want to add to the mix, you can use the -r flag to append the archive.

For example, to add a file called `cranky.png` to the archive, you would type the following and then press ENTER:

```
tar -rvf pics4pals.tar cranky.png
```

Of course, chances are that you will be doing more tarball extracting than creating, so you no doubt want to know how to do that. Fortunately, the process is pretty similar to what you use when creating the tarball. The main difference is in the first flag. Rather than using the tar command with the -c flag, you would instead use it with the -x flag, which tells the tar program to extract the specified archive. So if you want to extract a tarball called `spicyfood.tar`, type the following command, and press ENTER:

```
tar -xvf spicyfood.tar
```

What you have been doing thus far is creating and extracting archives, which are basically just collections of files. They are not, however, compressed. In fact, most tarballs you find will be compressed, and you can tell by the ending `tar.gz`. That gz means that the archive was compressed using the gzip program. Extracting a compressed tarball is just as easy as extracting a straight tar archive; all you have to do is add the -z flag, which tells your system to use the gzip program to decompress the archive. For example, if you want to extract a compressed tarball called `gosedown.tar.gz`, type the following command, and press ENTER:

```
tar -xzvf gosedown.tar.gz
```

Well, now that you know how to decompress and extract a gzipped tarball, you probably want to know how to create one. This is, again, little different than creating the tar archive itself; you would just add the -z flag to tell the program to use gzip to compress the folder. For example, to create a compressed version of your Documentia folder, which we’ll call tightdocs.tar.gz, you would type the following and press ENTER:

```
tar -czvf tightdocs.tar.gz Documentia
```

It’s worth mentioning at this point that you may also come across some files compressed with the bzip program. Such files are recognizable by some variation on the .bz or .bz2 file extension. Dealing with these files should pose no problem, because the commands are almost identical to those for gzip. Just substitute -j for -z in the command string.

## Compressing and Extracting Compressed Single Files

If you want to compress or decompress a single file, you don’t really need to use the tar program at all, since its purpose is to create archives consisting of several files. You can instead use the gzip and gunzip commands directly. For example, to compress a file called matilda.png, you would type gzip matilda.png and press ENTER. The matilda.png file would then become matilda.png.gz. To decompress the file, you would type gunzip matilda.png.gz and press ENTER, after which the matilda.png file would be back to normal.

So, can you compress an archive you’ve already created with the tar command? Sure. For example, to compress the spicyfood.tar archive mentioned earlier, you would type gzip spicyfood.tar, and voilà—you’ve got yourself a compressed spicyfood.tar.gz archive. Pretty cool, don’t you think?

## Project 9A: Creating a Plan

Now that you have a bit of command experience, it’s time to get some practice and put all those commands to good use. In this project, you’ll start off easy by creating a .plan file, like the one mentioned earlier in the chapter.

The actual .plan file is a hidden file (as you can see by the dot before its name), which contains the plan or message that you add to that file. That message will appear in the output of someone’s Terminal when they use the finger command to find out more about you. You may not need such a .plan file, but it is an easy enough way to get started working a bit more with commands and the Terminal itself, so let’s give it a try.
