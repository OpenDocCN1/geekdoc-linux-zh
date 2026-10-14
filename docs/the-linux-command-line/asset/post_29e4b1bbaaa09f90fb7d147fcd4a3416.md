
|  | actions. |
|---|---|
| `-mindepth levels` | Set the minimum number of levels that `find` will descend into a directory tree before applying tests and actions. |
| `-mount` | Direct `find` not to traverse directories that are mounted on other file systems. |
| `-noleaf` | Direct `find` not to optimize its search based on the assumption that it is searching a Unix-like file system. This is needed when scanning DOS/Windows file systems and CD-ROMs. |

## Further Reading

- The `locate`, `updatedb`, `find`, and `xargs` programs are all part the GNU Project's *findutils* package. The GNU Project provides a website with extensive on-line documentation, which is quite good and should be read if you are using these programs in high security environments:
- http://www.gnu.org/software/findutils/

## 19 – Archiving And Backup

One of the primary tasks of a computer system’s administrator is keeping the system’s data secure. One way this is done is by performing timely backups of the system’s files. Even if you’re not system administrators, it is often useful to make copies of things and to move large collections of files from place to place and from device to device.

In this chapter, we will look at several common programs that are used to manage collections of files. There are the file compression programs:

- `gzip` – Compress or expand files
- `bzip2` – A block sorting file compressor

The archiving programs:

- `tar` – Tape archiving utility
- `zip` – Package and compress files

And the file synchronization program:

- `rsync` – Remote file and directory synchronization

### Compressing Files

Throughout the history of computing, there has been a struggle to get the most data into the smallest available space, whether that space be a memory, storage devices or network bandwidth. Many of the data services that we take for granted today, such as portable music players, high definition television, or broadband Internet, owe their existence to effective *data compression* techniques.

Data compression is the process of removing *redundancy* from data. Let’s consider an imaginary example. Say we had an entirely black picture file with the dimensions of one hundred pixels by one hundred pixels. In terms of data storage (assuming twenty-four bits, or three bytes per pixel), the image will occupy thirty thousand bytes of storage:

```
100 * 100 * 3 = 30,000
```

An image that is all one color contains entirely redundant data. If we were clever, we could encode the data in such a way that we simply describe the fact that we have a block

of thirty thousand black pixels. So, instead of storing a block of data containing thirty thousand zeros (black is usually represented in image files as zero), we could compress the data into the number 30,000, followed by a zero to represent our data. Such a data compression scheme is called run-length encoding and is one of the most rudimentary compression techniques. Today’s techniques are much more advanced and complex but the basic goal remains the same—get rid of redundant data.

Compression algorithms (the mathematical techniques used to carry out the compression) fall into two general categories, lossless and lossy. Lossless compression preserves all the data contained in the original. This means that when a file is restored from a compressed version, the restored file is exactly the same as the original, uncompressed version. Lossy compression, on the other hand, removes data as the compression is performed, to allow more compression to be applied. When a lossy file is restored, it does not match the original version; rather, it is a close approximation. Examples of lossy compression are JPEG (for images) and MP3 (for music.) In our discussion, we will look exclusively at lossless compression, since most data on computers cannot tolerate any data loss.

### gzip

The gzip program is used to compress one or more files. When executed, it replaces the original file with a compressed version of the original. The corresponding gunzip program is used to restore compressed files to their original, uncompressed form. Here is an example:

```
[me@linuxbox ~]$ ls -l /etc > foo.txt
[me@linuxbox ~]$ ls -l foo.*
-rw-r--r-- 1 me me 15738 2008-10-14 07:15 foo.txt
[me@linuxbox ~]$ gzip foo.txt
[me@linuxbox ~]$ ls -l foo.*
-rw-r--r-- 1 me me 3230 2008-10-14 07:15 foo.txt.gz
[me@linuxbox ~]$ gunzip foo.txt
[me@linuxbox ~]$ ls -l foo.*
-rw-r--r-- 1 me me 15738 2008-10-14 07:15 foo.txt
```

In this example, we create a text file named foo.txt from a directory listing. Next, we run gzip, which replaces the original file with a compressed version named foo.txt.gz. In the directory listing of foo.*, we see that the original file has been replaced with the compressed version, and that the compressed version about one-fifth the size of the original. We can also see that the compressed file has the same permissions and time stamp as the original.

Next, we run the gunzip program to uncompress the file. Afterward, we can see that
