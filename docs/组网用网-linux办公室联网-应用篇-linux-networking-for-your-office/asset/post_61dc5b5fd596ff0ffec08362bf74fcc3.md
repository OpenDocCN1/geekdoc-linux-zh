
![](img/5d4d3092919d1d16884788127447cc6d_342_0.png)

## FIGURE 13.1
KDAT uses tar at its core, but also places its own information on the tape to index the tape's contents.

## Controlling the Tape Device

If all you want to do is create backups on a tape, tar or some other simple backup package, in conjunction with an auto-rewinding tape device, might be sufficient. Chances are good, however, that you need finer control over your tape device. For instance, you might want to do a complete system backup once each week and do incremental backups of only new or changed files once each day. The full backup might consume an entire tape, whereas the incremental backups don't, so to save money, you might want to place all the incremental backups on a single tape. To do so, however, you must skip past the first day's incremental backup, and that's an operation that tar can't do by itself.

To accomplish this goal, you need to use the tape control utility mt. The basic syntax for mt is

```
mt [-f device] operation [count] [arguments]
```

The device is the tape device, operation is the operation to be performed, count is the number of times the operation is to be performed, and arguments are any arguments the operation takes. Specific operations include the following:

- fsf—Skips forward count files.
- bsf—Skips backward count files.
- asf—Positions the tape at the start of file number count.
- eod or eof—Positions the tape at the end of existing data.
- retension—Re-tensions the tape. This option is useful for improving tape reliability, especially if a tape hasn't been used in a while.
- erase—Erases the tape.
- status—Displays information about the tape drive.
- load—Loads a tape into the drive. This command isn’t needed for all drives.
- offline—Takes the tape drive offline and rewinds the tape.
- compression—Sets the compression option for most tape drives that feature hardware compression. Use a value of 1 to enable compression, or 0 to disable it. Many drives that support hardware compression have jumpers to set the default. The compression option overrides the jumper setting. Some drives, particularly Exabyte units, use specific setdensity settings rather than compression to enable data compression. Consult your drive’s documentation or do a Web search to determine what settings you need.

In addition to these operations, mt supports many others, some of which are variants on these that position the tape slightly differently. You might want to experiment with the mt commands, especially as you develop your own backup scripts, to determine precisely what count value to give to any given operation to obtain the desired result.

### NOTE

> To tar and most other tape utilities, a file is an entire archive file, not a file on disk. For instance, if you back up the /home directory to tape using tar, that entire backup is one file as far as mt is concerned.

Let’s check out an example of using these commands. Suppose that you want to back up two directories, /home/francine and /home/gertrude. You want to keep them on the same tape but in separate tar files. You could do so by issuing the following commands:

```
mt -f /dev/nst0 load
tar cvf /dev/nst0 /home/francine
tar cvf /dev/nst0 /home/gertrude
mt -f /dev/nst0 offline
```

Suppose that the next day, Gertrude comes to you and says that she accidentally deleted the file bug-list.txt from her home directory. You could restore that file by issuing the following commands:

```
cd /
mt -f /dev/nst0 load
mt -f /dev/nst0 fsf 1
tar xvf /dev/nst0 home/gertrude/bug-list.txt
mt -f /dev/nst0 offline
```

The fsf command skips past the /home/francine backup file, allowing tar to access the /home/gertrude backup. You could use similar mt commands to skip past previous days’ backups in an automatic backup script.

### Note

> Tape restores are discussed in more detail later in this chapter, in the section "Restoring files," so don’t pay too much attention to the details of the tar command in the preceding example.

## Backing Up to CD-R or CD-RW

CD-R and CD-RW (CD-rewritable) backups work very differently from tape backups, because the tools are entirely different. You can’t write directly to a CD-R drive in the way you can write directly to a tape drive; instead, you must use a CD-R program to do the job. The most common CD-R program for Linux is cdrecord, though the older cdrwite is still useful in some situations. Various GUI front ends to these programs, such as X-CD-Roast (shown in Figure 13.2, http://www.fh-muenchen.de/home/ze/r2/services/projects/xcdroast/e_overview.html) can help you create a CD-ROM, but as with tape backups, they can become awkward when performing scheduled backup operations. This is especially true for CD-R GUIs because these programs aren’t designed with backup in mind, but for burning CDs for other purposes.

### Note

> CD-R is a write-once technology, whereas CD-RW is a rewritable technology. Both use the same Linux software to create CDs. I use the term CD-R to refer to both technologies in this chapter, for brevity’s sake.

Because CD-R technology requires a constant and steady stream of data, Linux CD-R software has traditionally required that you first create a single image file containing the data to be burned to disc. The cdrecord program can then write the data from that single file without having to construct the CD filesystem at the same time it’s writing data to the CD. There are efforts under way to develop software that would obviate the need to create an intermediate image file, but what I describe here uses the old style with an intermediate image file.
