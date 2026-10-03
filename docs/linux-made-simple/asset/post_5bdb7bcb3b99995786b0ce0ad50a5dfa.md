
## Tar: Archiving your files

Archiving contains many mysteries, such as zips and tarballs, but we are on hand to expand your knowledge of their uses.

Most people reading this are probably pretty familiar with creating, sending or receiving ZIP files. Zip takes a collection of files and stores them in a ZIP archive file, compressing the data in the process. As well as storing the contents of the files, it also stores all their metadata, which is extra information associated with an object. In the case of files, it includes the modification times, their owners and permissions, and, of course, the name of each file. When you unzip an archive, all of this information is extracted, which recreates the original set of files exactly as they were. This is pretty handy.

Archives have several uses, but the most popular include bundling up a set of files for download – a single file is easier to handle and the compression makes it faster to download – and creating backups. As Zip has been around for ages, everyone can use it and all OSes can handle it. Nonetheless, Zip does have a number of drawbacks. The main issue is that its compression is poor by modern standards. Over the past 25 years, compression technology has moved on and even though there have been improvements to Zip, there are better alternatives available. Another disadvantage of Zip is that it is intended for archiving to a file, whereas sometimes we want to send the data to another device or service.

The standard archival program for Unix-like operating systems is Tar, so called because Tar was originally used to store backups on tape drives (Tape ARchive). It works in a different way to Zip because it sends all the archived data to its standard output and doesn’t compress the data by default. This is because many tape drives already had hardware compression built in. The lack of compression code may seem like a disadvantage, but it’s actually a convenience. As Tar is able to pipe its data via an external compression program, it can use any compressor it likes – even one that wasn’t in existence when Tar was developed.

Compression programs work on one file or stream of data and produce one compressed file or stream, so this splits the job into two parts: archival and compression. While this may seem more complex, Tar is capable of handling the details itself. Let’s say we have a directory that is called foo. We want to create an archive of it, which is often referred to as a tarball. We can use one of these options:

```
tar cf foo.tar foo
tar czf foo.tar.gz foo
tar cjf foo.tar.bz2 foo
tar cJf foo.tar.xz foo
```

The c option tells the Tar program that we are creating an archive, while f tells it that we are storing the archive in a file using the given name. Therefore, the first command creates an uncompressed archive that is called foo.tar. The subsequent commands add an extra option that tells Tar which particular type of compression to use: z uses gzip compression, j uses bzip2 compression and J uses xz compression. (Watch the capitalisation!)

There are also long versions of these arguments that make the commands more readable, but most of us are lazy and use the version that is shorter to type. However, we could also have used this command line if we wanted to:

```
tar --create --gzip --file foo.tar.gz foo
```

The file extension is not required, but it’s a convention that makes it easier for people to see what type of archive it is – the system itself needs no such help as it can work all this out for itself. Unpacking an archive is simply a matter of replacing c with x, or --create with --extract. However, you don’t need to give the compression type, as Tar figures it out:

```
tar xf foo.tar.gz
```

Another option you may want to add is v or --verbose, to show you what Tar is doing. If you have been given a tarball, you may want to see what is inside it without unpacking it. If you have created an archive, particularly a backup, you may want to check it’s correct before relying on it. The test option checks the integrity and lists the contents of the archive.

```
tar tvf foo.tar.gz
```

Those are the main Tar options, but the program has many more, such as A or --concatenate to add files to an existing archive instead of creating a new one.

## Pipes and streams

A core part of the philosophy of Unix-like operating systems is for tools to be specialised – each tool should do one job and do it well. That means we need a way to chain programs together to achieve more complex tasks, and this is done with pipes. Every terminal program has streams for standard input, standard output and standard error (usually referred to as stdin, stdout and stderr). Standard input is how the program accepts information and it defaults to the keyboard when running a command from a terminal. Standard output is the output from the command that defaults to printing to the terminal window. Standard error goes to the same place, but all of these can be changed. Consider the example of:

```
tar c foo | sdc >foo.tar.sdc
```

The | character is the pipe and it connects the standard output of one program to the standard input of another. So Tar archives the contents of foo and sends it to stdout, which is then piped to the input of sdc. Most compressors default to working on a file:

```
gzip somefile
```

This compresses a file to somefile.gz. When no file is given, it compresses standard input and sends the result to standard output. The > character performs redirection and diverts standard output from the terminal to a file, so you get a compressed archive in foo.tar.sdc. Standard error is not redirected by >. If something goes wrong, error messages are printed to the terminal – if they were sent to the file, you wouldn’t know something was wrong.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_109_0.png)

Running Tar with the t (test) option not only checks that the archive is correct, but also shows you the full contents – usually enough for you to need to pipe it through a pager such as Less.

## Compression types

There are two types of compression: lossless and lossy. Lossy compression achieves a greater reduction in file sizes by carefully discarding data that doesn’t greatly affect the results. JPEG and MP3 files, for example, use lossy compression. Archiving uses lossless compression and uncompresses the result to get you back exactly where you started. There are a number of lossless compression methods available, here are some of the most common.

- Deflate This is the default compression used by Zip, it is old and not particularly effective, but is fast and well supported.
- Compress This is an old Unix compression program. Its files have a .Z extension, but you are unlikely to see many in the wild. There are also patent issues with it.
- Gzip This Compress replacement is completely open and still in use today. Gzip uses Deflate, but generally produces smaller archives than Zip with its default settings. It does not give the best compression, but it compresses and decompresses quickly, making it a good choice when size is not the most vital consideration.
- Bzip2 This is a more efficient compressor, but at the expense of speed. Compression in particular can be slower, but it produces more compact results.
- xz This more recent program uses the LZMA2 compression algorithm also used by 7-Zip. It is fast – particularly for decompression – and works brilliantly. It is the compressor of choice for many key Linux projects, including Coreutils and the kernel itself.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_110_0.png)

Here is the same archive using different compression programs. The Gzip version is significantly larger, but faster to compress and decompress.

## Future proofing

We mentioned that Tar can handle any new compression format that comes along because it passes compression to another program. There are command line options to do this automatically for gzip, bzip2 and xz, but what if someone comes up with a new compressor? Say something like sdc – super-duper compressor? You could create an uncompressed tarball and then use sdc to compress it, but that’s wasteful and slow, so instead use a pipe:

```
tar c foo | sdc >foo.tar.sdc
```

```
unsdc foo.tar.sdc | tar xv
```

Here, we use only the --create option with Tar. The lack of destination causes Tar to send the archive data to standard output, which is then piped to the sdc compressor program. The second command reverses the process, decompressing the archive and sending it to Tar for extraction.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_110_1.png)

Tar and the compressors have man pages, with many options. You’ll usually only need the ones covered here.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_110_2.png)

Most environments can view the archive contents. Shown above is the result of double-clicking a tarball in LXDE (the preferred desktop for Raspberry Pi).
