
## Uncompressing Files with uncompress

Compressing a file is handy for reducing the amount of disk space it uses, but you can’t do much with a compressed file—directly. At least. You’ll need to uncompress it first. As Code Listing 13.9 shows, you do so using the uncompress command.

### To uncompress a file with uncompress:

- uncompress labrea.tar.Z
At the shell prompt, type uncompress followed by the full filename of the file to uncompress. The compressed file is replaced by the uncompressed file, which is named like the original, but without the .Z (see Code Listing 13.9).

### Tips

- Remember that uncompressed files take up more space—sometimes a lot more space—than compressed files. You might want to check your storage quota with your ISP before you uncompress a file to make sure that you don’t exceed your limit. As Chapter 7 explains, you can often check your quota by typing quota -v at the shell prompt.

- You can add the -c flag to uncompress to leave the original file untouched and send the uncompressed version to standard output. For example, you might use uncompress -c torred.tar.Z > torred.tar. See Chapter 1 for more information on redirecting output, as is shown here.

- You can also use gunzip to uncompress compressed files. Check out Unzipping a gzip File with gunzip later in this chapter.

```
[ejr@hobbes compression]$ ls -l *
-rw-r--r-- 1 ejr users 297027 Jul 27 10:06 labrea.tar.Z
[ejr@hobbes compression]$ uncompress labrea.tar.Z
[ejr@hobbes compression]$ ls -l *
-rw-r--r-- 1 ejr users 501760 Jul 27 10:06 labrea.tar
[ejr@hobbes compression]$
```

Code Listing 13.9 You can uncompress files with a single swift command and possibly double your disk usage at the same time, as shown here.

## Zipping a File or Directory with gzip

If you want to compress only a single file or directory, you might choose gzip, rather than compress. gzip is more efficient, so you wind up with smaller files than you do with compress. As Code Listing 13.10 shows, you use gzip much the same way that you use compress.

### To zip a file or directory with gzip:

1. ls -l z*
At the shell prompt, use ls -l to confirm the name of the file or directory you want to zip. In this example, we're looking for z (as in zipadeedoodah) files.

2. gzip zipadeedoodah.tar
Type gzip followed by the name of the file or directory to gzip. The zipped file will replace the unzipped version and will have a new .gz extension.

### Tips

- You can tar a group of files and then compress the single file using gzip.

- If you want to keep a copy of the original, unzipped file, try gzip -c filetogzip > compressed.gz

- If the compressed files will be accessed by someone using Windows, you should consider using zip, which is discussed later in this chapter. Although gzip is more convenient in the Unix world, gzip is not the same as good old Pkzip or .zip files used in DOS and Windows.

```
[ejr@hobbes compression]$ ls -l z*
-rw-r--r-- 1 ejr users  507760 Jul 27 10:22 zipadeedoodah.tar
[ejr@hobbes compression]$ gzip zipadeedoodah.tar
[ejr@hobbes compression]$ ls -l z*
-rw-r--r-- 1 ejr users  239815 Jul 27 10:22 zipadeedoodah.tar.gz
[ejr@hobbes compression]$
```

Code Listing 13.10 Use gzip to zip up those bulky tar files.

## Unzipping a gzip File with gunzip

To access gzipped files, you'll need to unzip them. You do so using gunzip, as Code Listing 13.11 shows.

### To unzip a gzip file with gunzip:

1. `ls -l *.gz`
At the shell prompt, verify the name of the gzipped file with `ls *.gz` (Code Listing 13.11).

2. `gunzip zipadeedoodah.gz`
Enter gunzip and the name of the file to unzip. gunzip will uncompress the file(s) and return you to the shell prompt.

### Tips

- When you're unzipping files with gunzip, you're not required to enter the file extension. `gunzip zipadeedoodah` would work just as well as `gunzip zipadeedoodah.gz`.

- You might encounter gzipped files with a `.tgz` (targed, gzipped), `.tar.gz`, or just `.gz` extension. It'll handle any of those gracefully.

- Some systems don't recognize the gunzip command, so you might need to use `gzip -d` to uncompress the files.

- If you have a compressed file that you know is text—`oldfunnysayingsfromthenet.gz`, for example—you can uncompress it (without deleting the original file) and view it with a single command: `gzcat oldfunnysayingsfromthenet | more`.

- `gunzip` understands how to uncompress most (compressed) files, including those compressed with `compress` or `.zip` files from DOS/Windows systems.

```
[ejr@hobbes compression]$ ls -l *.gz
-rw-r--r--  1 ejr  users  53678 Jul 23 06:42 bigfile.gz
-rw-r--r--  1 ejr  users  53678 Jul 23 10:16 bigfile.new.gz
-rw-r--r--  1 ejr  users  239819 Jul 27 10:22 zipadeedoodah.tar.gz
[ejr@hobbes compression]$ gunzip zipadeedoodah.tar
[ejr@hobbes compression]$ ls -l *
-rw-r--r--  1 ejr  users  501760 Jul 27 10:22 zipadeedoodah.tar
[ejr@hobbes compression]$ ls -l *.gz
-rw-r--r--  1 ejr  users  53678 Jul 23 06:42 bigfile.gz
-rw-r--r--  1 ejr  users  53678 Jul 23 10:16 bigfile.new.gz
[ejr@hobbes compression]$
```

**Code Listing 13.11** Use gunzip to uncompress gzipped files.
