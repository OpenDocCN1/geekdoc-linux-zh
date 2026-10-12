| dump Parameter | Description |
|---|---|
| `-n` | Specifies the dump level, where *n* is a number between 0 and 9. For example, `-0` would perform a full backup. |
| `-b blocksize` | Sets the dump block size to *blocksize*, which is measured in kilobytes. If you are backing up many large files, using a larger block size will increase performance. You may need to carefully adjust this to match the capabilities of your tape system. |
| `-B count` | Specifies a number (*count*) of records per tape to be dumped. If there is more data to dump than there is tape space, **dump** will prompt you to insert a new tape. |
| `-f filename` | Specifies a location (*filename*) for the resulting dump file. You can make the dump file a normal file that resides on another file system, or you can write the dump file to the tape device. The SCSI tape device is `/dev/st0`. |
| `-u` | Updates the `/etc/dumpdates` file after a successful dump. |
| `-d density` | Specifies the *density* of the tape in bits per inch. |
| `-s size` | Specifies the *size* of the tape in feet. |
| `-a` | Bypasses all tape-length calculations and writes until an end-of-media signal is returned. This works best for most modern tape drives and is particularly useful for appending data to existing tapes. This is the default mode. |
| `-z or -j` | Compresses each data block. The `-z` parameter uses zlib compression, while `-j` uses bzip2. Either option can be immediately followed with a number, if you want to specify the compression level, or white space, if you want to accept the default compression level of 2. Your tape drive must be able to support variable-length blocks to be able to use this feature. If your tape system has hardware compression built in, don't use both the hardware compression and this option together, or your files will likely increase in size. |

**Table 21-2** Common Options Used with the dump Command

# Using dump to Back Up an Entire System

The **dump** utility works by making an archive of one file system. If your entire system comprises multiple file systems, you need to run **dump** for every file system. Since **dump** creates its output as a single, large file, you can store multiple dumps to a single tape by using a nonrewinding tape device.

Assuming we're backing up to a SCSI tape device, /dev/st0, we must first decide which file systems we're backing up. This information is in the /etc/fstab file. Obviously, we don't want to back up files such as /dev/cdrom, so we skip those. Depending on our data, we may or may not want to back up certain partitions (such as swap and /tmp).