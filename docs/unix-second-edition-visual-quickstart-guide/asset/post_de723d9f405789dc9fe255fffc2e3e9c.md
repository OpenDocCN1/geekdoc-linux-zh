
## To archive a directory with tar:

- 1. ls -l
  For starters, type ls -l at the shell prompt to verify the name of the directory you're going to tar.

- 2. tar -cf tarredfilename.tar Feather
  Type tar followed by
  ▲ The -cf flags (to create a file)
  ▲ The name you want the tarred (archived) file to have (tarredfilename.tar in this example)
  ▲ The name (or names) of the directory or files to tar (Feather, here)

### Tips

- ■ See the section called Combining Commands later in this chapter for timesaving ideas for combining and compressing files all in one fell swoop.

- ■ Some versions of tar also support gzip, so you can use tar -czf tarredfilename.tgz Feather to tar and gzip all at once.

- ■ You can add the v flag to the tar command flags (-vcf) to get a verbose description of what's being tarred.

- ■ If you want to sound like a real Unix geek, refer to tarred files as "tarballs."

## Unarchiving Files with tar

You’ll also use tar to unarchive files, where you take all of the individual files out of the single tarred file—like dumping the bunch of toys out of the toy box—as shown in Code Listing 13.6.

### To unarchive files with tar:

- tar -xf labrea.tar
  At the shell prompt, type tar -xf (here, x means extract) followed by the name of the tarred file you want to unarchive. The bunch of once-tarred files will be separated into the original files or directories, as shown in Code Listing 13.6.

### To unarchive selected files with tar:

- tar -xf labrea.tar "*mammoth*"
  You can also extract only specified files from a tar file. You might do this to restore just a couple of files from a backup archive, for example. This command extracts all files that have mammoth in their names from the labrea.tar file and places them back where they belong (Code Listing 13.7).

### Tips

- Consider moving tarred files into a temporary directory before you unarchive them. When you unarchive, tar overwrites any files with the same names as files that are extracted. Using a temporary directory will prevent this.
- Use tar -tf filename to list the files (to check your work, perhaps, or find a backup file) without actually unarchiving the files.

```
[ejr@hobbes compression]$ tar -xf labrea.tar
[ejr@hobbes compression]$ ls -l labrea/
total 483
-rw-r--r-- 1 ejr users 53678 Jul 27 18:05
-> bigfile.gz
-rw-r--r-- 1 ejr users 128886 Jul 27
-> 10:06 mammoth.jpg
-rw-r--r-- 1 ejr users 177607 Jul 27
-> 10:05 house.uue
-rw-r--r-- 1 ejr users 128886 Jul 27
-> 10:06 rowboat.jpg
[ejr@hobbes compression]$
```

Code Listing 13.6 Untarring files reconstructs the original directory structure.

```
[ejr@hobbes compression]$ tar -xf labrea.tar
-> "*mammoth*"
[ejr@hobbes compression]$ ls -l labrea/*
-rw-r--r-- 1 ejr users 128886 Jul 27
-> 10:06 labrea/mammoth.jpg
[ejr@hobbes compression]$
```

Code Listing 13.7 Unarchive just a single file to replace a missing or corrupt file.

## Compressing Files with compress

Compressing a file just means making it smaller so that it takes up less hard-disk space. It's like filling a toy box, closing the lid, then sitting on it to mush the contents so that they fit into a smaller space. Any time you create a file that you'll be sending via FTP or that people will access through the Web, you'll want to compress the file so that it takes less time to send and download. As Code Listing 13.8 shows, you compress files using the compress command.

```
[ejr@hobbes compression]$ ls -l *
-r--r--r-- 1 ejr users 501760 Jul 27
-> 10:06 labrea.tar
[ejr@hobbes compression]$ compress labrea.tar
[ejr@hobbes compression]$ ls -l *
-r--r--r-- 1 ejr users 297027 Jul 27
-> 10:06 labrea.tar.Z
[ejr@hobbes compression]$
```

Code Listing 13.8 Listing files before and after compressing them lets you see how much smaller the new file is.

### To compress a file with compress:

- compress labrea.tar

At the shell prompt, type compress followed by the filename. Here, we're compressing a tarred file, which contains multiple files. As you can see in Code Listing 13.8, the compressed file has a new extension (.Z) that shows that it's compressed, and it replaces the original, uncompressed file.

### Tips

- You can compress only one file at a time. If you have multiple files you want to compress, consider archiving them first using tar, and then compressing the single archived file. See the section called Archiving with tar earlier in this chapter.

- You can add the -c flag to compress to leave the original file untouched and send the compressed version to standard output (where you'll probably specify a name and save it to a file). For example, you might use compress -c labrea.tar > labrea.tar.Z. See Chapter 1 for some mighty interesting information on redirecting output, as is shown here.
