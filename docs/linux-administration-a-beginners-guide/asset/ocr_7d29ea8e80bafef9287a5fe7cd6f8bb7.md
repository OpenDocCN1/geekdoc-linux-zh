# Using dump

The dump tool is a command-line utility. It takes many parameters, but the most relevant are as shown in Table 23-2.

For example, here is the command to perform a level 0 dump to /dev/st0 of the /dev/rdal file system:

```
```
[root@lord /root]# dump -0 -t /dev/st0 /dev/rdal
```
```

SUPPRESSING THE TAPE SIZE CALCULATION The dump tool requires that it know the size of the tape in units of bits per inch and feet per tape. It uses this information to provide multi-volume backups so that it can prompt the operator to insert the next tape when it is ready. But if you don't know the size of your tape in bits per inch and its length in feet, you may still know the dump will fit on the tape. (For example, you may know that the partition you are dumping is 2 GB and the tape capacity is 5 GB uncompressed.) In this situation, you can do a little trick to keep dump from calculating the tape size. Instead of dumping straight to the device, send the output to the standard output and then use the

| Parameters for the dump Command | Description |
| --- | --- |
| -n | The dump level, where n is a number between 0 and 9. |
| -b blocksize | Sets the dump block size to blocksize, which is measured in kilobytes. If you are backing up many large files, using a larger block size will increase performance. |
| -B count | Specifies a number (count) of records per tape to be dumped. If there is more data to dump than there is tape space, dump will prompt you to insert a new tape. |
| -f filename | Specifies a location (filename) for the resulting dumpfile. You can make the dumpfile a normal file that resides on another file system, or you can write the dumpfile to the tape device. The SCSI tape device is /dev/st0. |
| -u | Update the /etc/dumpdates file after a successful dump. |
| -d density | The density of the tape in bits per inch. |
| -B size | The size of the tape in feet. |

Table 23-2. Parameters for the dump Command