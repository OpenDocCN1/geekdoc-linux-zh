# Bad Hard Disk Blocks

Linux volumes are set up in units of memory known as blocks. Depending on your situation, you may have 512, 1024, 2048, or 4096 bytes of information in each block. If you have problems with your hard disk, you may get an error message similar to the following:

```
Read_intr: 0x10 error
```

You can get this error in two situations. Either you have a physical defect on your hard drive, or you're trying to format a volume that's larger than what's physically available on your hard drive.

One way to check for bad blocks on your hard drive is with the badblocks command. It marks and sets aside any blocks that can't be read.

> Note: The badblocks command is similar to Microsoft's chkdsk command. Other commands used to check for bad blocks are mke2fs -c and e2fsck -c.

# Other Installation Issues

There are two other errors that may occur, especially when you're installing Linux over a network. If you see a message like file not found or permission denied while installing Linux, you have a problem with your Linux distribution. You may have a Linux installation CD or download that's missing some files, or it may be set with improper permissions. In either case, you'll need to try downloading the distribution again, try the installation from a different CD, or try a different distribution altogether.

When you're installing Linux over a network, such as through FTP, you need to download a series of files. A common FTP command for downloads is mget, which copies specified files from the current FTP server directory to the current directory on your local computer. The differences between the commands used to download files can create a problem. For example:

```
mget *.*
mget .
```

If you're using the MS-DOS version of FTP, the effect of these commands are identical; they copy all files from the current directory on the FTP server to the current directory on the local computer.

However, these commands have a different effect in Linux. Many Linux files don't have a dot (.) to divide a filename from its extension, such as chapter14.doc. So when you run FTP from Linux and run the mget *.* command, the only files copied are the files set up in the "dot" format.