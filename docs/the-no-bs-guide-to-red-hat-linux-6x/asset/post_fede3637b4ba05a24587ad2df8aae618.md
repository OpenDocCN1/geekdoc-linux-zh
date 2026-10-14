
## THE GZIP AND GUNZIP COMMANDS

The gzip program compresses a single file. One important thing to remember about gzip is that, unlike tar, it replaces your original file with a compressed version. (The amount of compression varies with the type of data, but a typical text file will be reduced by 70 to 80 percent.) Say you enter this command:

```
gzip cheap.suit
```

You’ll end up with a compressed file named cheap.suit.gz, and cheap.suit will be deleted.
To decompress the cheap.suit.gz file, enter this:

```
gunzip cheap.suit.gz
```

You’ll get the original cheap.suit file back, and cheap.suit.gz will be deleted.
You can tell gzip to use different levels of compression with the -n flag, where n is a number from 1 to 9. The -1 flag means “fast but less efficient” compression, and -9 means “slow but most efficient” compression. Values of n between 1 and 9 will trade off speed and efficiency, and the default is -6. If you want to get the best possible compression and you don’t mind waiting a little longer, use the -9 flag, like this:

```
gzip -9 cheap.suit
```

One other useful option is the -r flag, which tells gzip and gunzip to recursively compress or decompress all files in the current directory and any subdirectories. (Even with the -r flag, gzip still compresses one file at a time.) Here are some examples:

- gzip -r somedir    Zip all files in the somedir directory.
- gunzip -r somedir    Unzip all files in the somedir directory.

## HANDLING COMPRESSED ARCHIVES

It’s common to apply gzip to a tar file, which is why you see files with names like something.tar.gz on Linux systems. When you want to extract the contents of a gzipped tar file, you have several choices. The first is to use gunzip followed by tar, like this:

```
gunzip something.tar.gz
tar xvf something.tar
```

Or you could do it all in one command, like this:

```
gunzip -c something.tar.gz | tar xvf -
```

The -c flag tells gunzip to decompress the file, but instead of creating a something.tar file, it pipes the decompressed data directly to the tar command. The tar command on the right side of the pipeline looks a little strange, too—instead of a file name after the xvf, there’s just a dash. The dash tells tar that the input is not an actual file on disk, but rather a stream of data from the pipeline. (Note that the gunzip input file is not deleted when you use the -c flag.) Here’s a third method of extracting the contents of a compressed tar file that’s even easier. Remember the z flag with the tar command? You can use it to decompress and unbundle a tar file, like this:

```
tar xvfz something.tar.gz
```

The end result is exactly the same (the files that were in the compressed tar file are now in your current directory), but this is much easier than issuing multiple commands or writing a messy-looking gunzip-tar pipeline. Note that this command will work on all Linux systems, but the z flag for tar is not always available on other flavors of Unix. (However, you can download and compile the source code for the GNU version of the tar command. See the note near the beginning of this chapter about getting the source code for the GNU utilities.)

## THE COMPRESS, UNCOMPRESS, AND ZCAT COMMANDS

The compress and uncompress programs work just like gzip and gunzip, but they use an older and less efficient compression technique. If you’re using Linux, you shouldn’t have to bother with compress and uncompress at all. Even if you come across a file created with compress (something with a .Z suffix), you can decompress it with gunzip, because gunzip understands both formats. Still, just for completeness, here’s how to use the compress and uncompress programs:

compress some.file    Create compressed some.file.Z
uncompress some.file    Create decompressed some.file

The zcat program is another Linux antique. It does the same thing as uncompress with the -c flag (decompresses and writes output to the pipeline), so the following two commands would be equivalent:

```
uncompress -c something.tar.X | tar xvf -
zcat something.tar.X | tar xvf -
```

You should have to use these commands only if you're running some version of Unix besides Linux. (Even then, many Unix systems will have the GNU versions of gzip, gunzip, and tar available.)

## THE ZMORE AND ZLESS COMMANDS

The zmore command is a handy utility that lets you view gzipped files one screen at a time (much like the more command) without first decompressing them. The zmore command pauses after each screenful, printing --More-- at the bottom of the screen. You can press ENTER to display one more line, or press the spacebar to view the next screen of data.

The zless command works the same way, except the decompressed output is displayed by the less command for additional viewing flexibility. Keep in mind that zmore and zless do not modify the input file.

## THE ZIP AND UNZIP COMMANDS

The zip and unzip programs work almost exactly like their cousins PKZIP and PKUNZIP in the DOS environment. You can squash a bunch of files together into a zip file like this:

```
zip squash.zip file1 file2 file3
```

Then you can extract the original files like this:

```
unzip squash.zip
```

Most of the flags are the same as for PKZIP and PKUNZIP, but there are a few differences, so you might like to view the help with zip -h or unzip -h if you need anything fancier than the basic commands shown here.
