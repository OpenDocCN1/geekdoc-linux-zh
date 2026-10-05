# Do not use SPACES within filenames

caution Although you can use SPACES within filenames, it is a poor idea. Because a SPACE is a special character, you must quote it on a command line. Quoting a character on a command line can be difficult for a novice user and cumbersome for an experienced user. Use periods or underscores instead of SPACES: `joe.05.04.26_new_stuff`.

If you are working with a filename that includes a SPACE, as a file from another operating system, you must quote the SPACE on the command line by preceding it with a backslash or by placing quotation marks on either side of the filename. The two following commands send the file name to the printer.

```
```
$ 1 pr\ file
$ 1 "my file"
```
```

# FILENAME EXTENSIONS

A filename extension is the part of the filename following an extended period. The filenames listed in Table 6-1, filename extensions help describe the contents of the file. Some programs, such as the C programming language compiler, default to specific filename extensions; in most cases, filename extensions are optional. Extensions freely make filenames easy to understand. If you like, you can use periods within the same filename—for example, `notes.4.10.01` or `files.tar.gz`.

**Table 6-1** Filename extensions

| Filename extension | Meaning of extension |
|---|---|n| compute.c | A C programming source file |
| compute.o | The object code file for compute.c |
| compute | The executable file for compute.c |
| memo.0410.txt | A text file |
| memo.pdf | A PDF file; view with xpdf or kpdf under a GUI |
| memo.ps | A PostScript file; view with gs or kpdf under a GUI |
| memo.Z | A file compressed with compress (page 176); use uncompress or gunzip (page 175) to decompress |
| memo.tgz or memo.tar.gz | A tar (page 176) archive of files compressed with gzip (page 175) |
| memo.gz | A file compressed with gzip (page 175); view with zcat and decompress with gunzip (both on page 175) |
| memo.bz2 | A file compressed with bzip2 (page 174); view with bzcat and decompress with bzip2 (both on page 175) |
| memo.html | A file meant to be viewed as a Web browser, such as Firefox |
| photo.gif, photo.jpg, photo.jpeg, photo.bmp, photo.tif, or photo.tiff | A file containing graphical information, such as a picture |