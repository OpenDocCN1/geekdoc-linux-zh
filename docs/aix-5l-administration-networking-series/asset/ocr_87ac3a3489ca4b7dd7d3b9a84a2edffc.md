This command assumes the tape drive is /dev/rmt0. The second column in the output is the current tape drive block size. If it is 0, then the tape is set to variable length, which is what we want for this procedure. If the block_size is anything other than zero, then write down the value for future reference. To set the block size to variable length, issue the following command:

```
# chdev -l rmt0 -a block_size=0
```

assuming the tape drive is /dev/rmt0. The next step is to extract the first 128K block of data from the tape. To accomplish this, use the dd command and set the block size to 128K:

```
# dd if=/dev/rmt0 bs=128k of=/tmp/tape.out count=1
```

Using the output file that we created, /tmp/tape.out, we can determine the block size that was used to make the tape by doing a long listing of the file. The size of the file is the tape block size:

```
# ls -l /tmp/tape.out
-rw-r-r-r--  1 root    system    1024  Fed 21 10:08 tape.out
```

In this example, the tape block size is 1024. To find the format of the data on the tape—for example, tar, backup, or cpio—you use the file command.

```
# file /tmp/tape.out
tape.out:        tar archive
```

This archive is a tar archive and was backed up with a tape block size of 1024.

If you changed the tape block size to variable length before, you can now change it the desired tape density using the following command:

```
# chdev -l rmt0 -a block_size=new_value
```

# CHECKLIST

The following is a checklist for the key points in system backup:

+   - The **mkssys** command is used to create a bootable system image of the rootvg volume group. However, this command doesn't back up other volume groups that might exist on your system.

+   - For non-rootvg volume groups, use the **savevg** command to save an entire volume group and its structure in a format that can be easily restored with the **restvg** command.

+   - Use the **backup** and **restore** facility to back up by filename or by i-node.