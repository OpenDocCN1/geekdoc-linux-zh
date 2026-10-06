You can use upper-and/or lowercase letters in filenames. GNU/Linux is case sensitive; thus files named JANUARY, January, and january represent three distinct files.

# Do Not Use SPACES within Filenames // caution

Although you can use SPACES within filenames, it is a poor idea. Because a SPACE is a special character, you must quote it on a command line. Quoting a character on a command line can be difficult for a novice user and cumbersome for an experienced user. Use periods, underscores, or hyphens instead of SPACES: joe.02.04.26,for_sam,new_stuff.

# Filename Extensions

In the filenames listed in Table 4-1, filename extensions help describe the contents of the file. A filename extension is the part of the filename following an embedded period. Some programs, such as the C programming language compiler, depend on specific filename extensions, but in most cases filename extensions are optional. Use freely make filenames easy to understand. If you like, you can use several periods within the same filename: for example, notes.41.01 or files.tar.gz.

# Filename // table 4-1

| compute.c | A C programming language source file |
| compute.o | The object code for the program |
| compute | The same program as an executable file |
| memo.0410 | A text file |
| memo.pdf | A PDF file; view with xpdf |
| memo.ps | A postscript file; view with gs |
| memo.Z | A file compressed with compress (page 73); use uncompress (or gunzip—page 74) to decompress |
| memo.tar.Z | A tar (page 75) archive of files compressed with compress (page 73) |
 memo.gz | A file compressed with gzip (page 73); view with zcat or decompress with gzip (both on page 74) |