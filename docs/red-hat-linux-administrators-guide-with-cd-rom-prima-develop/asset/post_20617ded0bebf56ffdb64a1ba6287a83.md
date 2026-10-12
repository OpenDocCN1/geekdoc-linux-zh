
their software development. Hundreds of HowTo pages and explanations are available at http://www.linux.com. One major resource is the Linux Documentation Project, which keeps not only nearly every man page imaginable, but also dozens of white papers or more technical explanations of how Linux operates. It also serves as a repository for more sophisticated clarifications. Often these pages include gems of knowledge that can help beginning Linux users. It is not necessarily true that the writers of code can best explain how something works. It is often the users who provide the best documentation.

## Creating Directories for New Code

After downloading the source code into a temporary directory on your machine, you can begin uncompressed the files into the directory of your choice. Where you unzip and untar the files is not so important since their location will only hold all the source code and the newly created binaries. You may not necessarily choose to keep the executables in this location but place them instead into a common location where other binaries are stored, such as `/usr/local/bin`. Where you place the binary itself on the system is the more crucial factor. For now, you should place the source code used for compilation purposes within a reserved directory—somelace where the partition has sufficient room for extra files. Several administrators prefer using the `/usr/local/src` as a temporary directory for installing and compiling source code. I prefer creating my own directory in the `/usr/local` directory. Something such as `/usr/local/gnu` works just as well as any default location. You can change or modify this site to suit your own tastes.

Some programs need to be installed in a specific directory. The Linux kernel, for example, should always be unzipped and untarred in the `/usr/src` directory. When fully expanded, the kernel creates its own `linux/` directory, overwriting the older one. If you are creating a new Linux kernel, be sure to move or rename the older `linux/` directory in `/usr/src`; otherwise you may encounter problems when it comes time to compile and install the new kernel. Also check for symbolic links such as a Linux link pointing to the older Linux source directory. Remove any links before uncompressing the newer source code. You can find more information about compiling a new Linux kernel from source in Chapter 14.

Some people like to unzip all their files within their own `/home/` directory. For instance, I might like to place all the source code for every new program that I download into `/home/kerry` and have unique directories for each program.

Though this makes the new code easily accessible, it also creates a jumbled mess in your home directory. I prefer instead reserving this space for my own text documents and not for program source code. Sometimes a program directory might share the same name as a data directory that you are using in your home location.

To keep things separate and to avoid any confusion, do not compile in your `/home` location. If you must compile in your home directory, due to permission issues or for convenience, it is a good idea either to create a subdirectory to keep things organized or to delete the raw source code once the program is installed. Usually new users should create a unique directory just for source code. Here you can install and compile to your heart's content. Placing this directory in `/usr/local` is often a good choice since the data are kept on a distinct partition, away from other data. Most programs that you compile from source usually install the binaries in `/usr/local/bin`, also on the same directory tree. Some Linux users prefer placing everything in `/usr/local/*`, but this directory can also get clogged up with miscellaneous files from other installs. If the programs that you are installing are part of the GNU project for free software, you might create your own directory location, such as `/usr/local/gnu`. Then you will know this directory's locations and can grant yourself the correct permissions to place and compile source code there.

To create your own directory for compiling code, you can follow these steps:

- 1. Decide where you want to place a temp directory.
- 2. Change directories to the default location, by entering `cd /usr/local`.
- 3. Make the new directory of your choice, by entering `mkdir gnu/`.
- 4. Grant ownership to the correct user and group. Under Red Hat, these will most likely be your own username for both variables. For example, I would enter `chown -R kerry gnu/` and `chgrp -R kerry gnu/`.
- 5. Change to your new directory and place the tarred and zipped file there.

Once you have decided where to place your source, you are now ready to unzip and untar the code. Most programs are archived by using the tar command; however, there are varying methods of compressing the files. Some might be tarred only or have just the .tar extension. As Chapter 9, “Fixing Mistakes,” explained, most programmers opt to use the GNU zip utility. This gives the file a .gz extension along with the .tar extension.

### Note

Over time, some of the files might become antiquated and you may want either to update their directories or delete them altogether. Most good programmers plan to place their updates in the same location as their earlier releases. Before removing any source directory, be sure to check the README or INSTALL files and verify what the changes are between the two releases. If the latest release or the changelog file has no special comments, you should be able to delete the older directory without much difficulty. Once you untar, unar, compile, then install the new release, the most recent release overwrites all the older binaries in their default location.

The following example shows how a programmer might tar and compress a developmental program, in this case a window manager package:

```
WinMaker-0.63.0.tar.gz
```

You are not limited to using all lowercase or all uppercase letters, nor must you use only one period in the entire expression. You can use a mixture of upper- and lowercase letters, combined with numbers, punctuation marks and other non-alphanumeric characters. The only limit is keeping the filename to 256 characters.

Other programmers might choose to use the compress command with their finished product, which would give the filename a .Z extension. Others might combine both tar and zip utilities and give the file a .tgz extension. Though the compression routines differ, uncompressing them and untarring them is done with gunzip.

When you untar most compressed programs, the untar and unzip routine will create a unique directory, usually with the same name and release number as the compressed program. Issuing a generic untar and unzip command should be create a new directory with the relevant files located inside. Sloppy programmers will simply unzip all the files into the current directory without creating a new, distinctive directory. As a result, such programmers ultimately will waste a lot of time and effort cleaning up. Check the contents of a file before uncompressing by using the t option. This lists the contents of an archive before the files are extracted. There are several ways this option can be applied.

```
tar -ztvf <filename> | less
gunzip -c <filename> | tar tvf - | more
```

Either of these commands or a variation on each will display the archived contents of a tarred and zipped file before uncompressing.

A standardized command for both untarring and unzipping the source is as follows:

```
gunzip -c WindowMaker-0.63.0.tar.gz | tar xvf -
```

Some of the more recent programs are compressed with the bzip2 command. To untar and unzip such source, you must substitute the gunzip command with bunzip2:

```
bunzip2 -c WindowMaker-0.63.0.tar.gz | tar xvf -
```

You can substitute any other *.targz, *.tar.bz2, *.tggz, or *.Z filename in place of Window Maker. This window manager is just one that I chose to use as an example.

For more information regarding compression utilities, consult Chapter 9.

These types of commands are not required to unzip the program. There are several other ways to open a similar file. You can gunzip it first, then untar the file. This is sometimes a more roundabout method, but it accomplishes the same thing.

```
unzip WindowMaker-0.63.0.tar.gz
tar -xvf WindowMaker-0.63.0.tar
```

A distinct disadvantage of this method is that when the file becomes uncompressed, it occupies more space on the system while extracting the files and it is no longer zipped. A gzip command is required to recompress it.

Another method frequently used is simply to add the -z option to the tar command. This unzips the file at the same time it is untarred.

```
tar -xvzf WindowMaker-0.63.0.tar.gz
```

Many people prefer this option since it is a shorter, fairly straightforward command. One option used with this command is -v, which prints out the results of the decompression in verbose mode. This option allows you to see the directories exactly as they are created and the location of the files. The -x option simply stands for extract rather than create. You use this option when archiving the files. The -p option is used to retain the same permissions after extraction as before compression.
