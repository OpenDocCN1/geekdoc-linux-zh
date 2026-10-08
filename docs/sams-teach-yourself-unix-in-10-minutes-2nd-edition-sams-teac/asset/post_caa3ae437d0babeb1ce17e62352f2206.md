
## Compression and Archiving Tools

What Can bzip2 Do for You? Also appearing recently is the bzip2 compression utility, despite being the newer kid on the block, looks very promising for tight compression. You can learn more about this tool at the bzip2 website at http://www.bzip.org/.

bzip2 is a freely available, high-quality data compression. The current version is 1.0.3, released February 15, 2005, so it's still being updated as the writing of this book.

It typically compresses files to within 10% to 15% of the best available techniques, while still being twice as fast at compression and six times faster at decompression. This being said, it would make sense if you need to have this higher rate of compression, you should use this utility. Many users still use gzip.

The syntax and options for bzip2 have intentionally been made similar to gzip, so if you encounter this program as it grows in popularity, you won't have too much trouble figuring it out. Compression with bzip2 follows the gzip format bzip2 <filename>, which produces the compressed file <filename.bz2>. Decompression is simply bunzip2 <filename.bz2>.

Since this utility is not common to see or use, if you encounter bzip2 and need to do more than trivial compressions or decompressions, it is recommended that you consult your local man pages for current information.

Creating files using the zip format (which uses the suffix .z in Unix) for distribution to other Unix users is generally not a good idea, as zip and unzip are not always available to Unix users. These utilities are freeware, so get your system administrator to install them if you need to access to them.

## Lesson 10

If your target, however, is users of Macintosh or Windows computers, zip is a file format that they can most likely read. Both the zip and unzip programs have a number of potentially useful options, a list of which can be displayed by issuing either command followed by the option -h.

In this section of the lesson, we have covered how to compress data, and we lightly touched on the use of the tar command. In the next section, we will dig deeper into the tar command and cover its use.

## The tar Command

If you spend much time using Unix systems, you're bound to run into tar files. The tar command is a convenient and commonly used tool for personal archiving and distribution of files. It is imperative that you are familiar with tar if you are studying Unix beyond the level of this book. As mentioned before, tar stands for Tape Archive, although this is used more often for standard packaging. It was originally designed for file backup, but today can be used with other storage media.

What is packaging? Well, let's say you needed to send someone a program you created. You would most likely just have one file, but multiple files. You may want to create a single file that basically encompasses all the rest of the files or directories you are looking to package. The purpose of assembling a collection of files into one combined file is for easier archiving, storage, and sending condensed versions of data to others. When run it produces files with a .tar extension. When combined with gzip, for data compression, the resulting file extensions may be .tgz, .tar.gz, or .tar.Z as mentioned earlier.

The tar command in its simplest form creates or unpacks archive files. When creating an archive, provide tar with a filename for the archive and a list of files that you want to archive. The tar program will collect all the files you specify and put them into one single file—this is commonly called a tarball.

When unpacking archives, provide tar with the name of a tar file and extracts the contents of the file into the current directory, or a directory you specify with the exact same filenames, paths, and contents that existed on the system where it was tarred.

```
tar -xvf storage030105.tar
```

After a list of everything in the file is shown by the verbose option, you will have extracted this file (and all its contents) identically into the current directory you are in now. Sometimes you may want to view what is in a tar file before extract it. Type `tar -tvf <tarfile.tar>` before unpacking it if you are not sure what may be in a file you are ready to extract. The -t option is the list option, and ask tar to tell you the contents of the file rather than unpack it. This is helpful if you want to quickly see what is inside.

## Using uuencode/uudecode

To send your files to another person through a tool such as FTP (stands for Transfer Protocol and efficiently transfers files from a source to a destination) or through email, you may need to adjust things. For instance, you may need to send an email to a Macintosh user who uses Binhex. This is just another encoding scheme. Because of this, you may have to change the specification of the data you send in your email attachment. This is not common for users who are accustomed to using Windows, although within Windows also uses uuencode. Long story short, it is imperative as a Unix user that you know how to adjust this because you may have to specify it with Unix.

![](img/9552a570ce35faac09a770fd5ff1ede3_152_0.png)

> UU-what? uuencode stands for a set of algorithms for converting files into a series of 7-bit ASCII characters that can be transmitted over the Internet. Originally, uuencode stood for Unix-to-Unix encode, but it has become a universal protocol used to transfer files between different platforms such as Unix, Windows, and Macintosh. Uencoding is especially popular for sending email attachments. Nearly all email applications support uencoding for sending attachments and udecoding for receiving attachments.

## Compression and Archiving Tools 135

The uuencode program accepts any file as input, and it produces an encoding of the file that can be included in an email message. To a person, the contents of this file look like random characters; on the receiving end, however, the user can use the uuencode command to extract the original file. Let's look at how that does work:

To use the uuencode command, you need to follow these steps:

- 1. Select a file to uuencode.
- 2. Issue the uuencode command as uuencode <filename> <callmethis> > .uue. (You need to type that before the <filename>.uue argument.)

Your computer will produce a file named <filename>.uue, which contains the uuencoded version of the file. For example, if you have a file named test and want to uuencode it, you can type the following:

```
uuencode testsend > testsend.uue
```

Your computer produces a file named test.uue, which decoded will be named testsend and contains the contents of your testsend. Now you can copy and paste, or whatever you need to do to insert the file you just created into an email message and send it whenever you want.

Of course, if you receive a uuencoded file, you need to know how to decode the file. Decoding a uuencoded file is also extremely simple; issue the uuencode command as uuencode <filename>.uue. Your machine will produce a file in the current directory identical to the one originallyencoded.

## Summary

In this lesson we covered how to archive and compress files and other data on your Unix system. This wraps up the file management portion of this book. In our next lesson, we will start to learn more about your shell, and in particular, the processes running on your Unix system. Here's a look at what was learned in this lesson:

- The three common compression utilities on Unix systems are the omnipresent compress, the newer and smarter gzip, and the cross-platform zip programs. A relatively new addition to the Unix compression scene is bzip2, which appears to produce better compression than compress or gzip.
- When you need to provide a collection of files to other users, or simply archive a set of files for future use, you can use tar to create tar files that contain all your files in one convenient package.
- If you need to send a file to someone through email, you can create an email-able encoding of the file by using the uuencode command.
- Don't be alarmed if you uldecode a file and can't immediately find it. The real filename is stored in plain text at the beginning of the file.
