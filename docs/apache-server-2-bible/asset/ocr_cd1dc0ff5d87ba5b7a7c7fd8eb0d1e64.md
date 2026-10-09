character until you close the file. This gives us a easy source to fill out an out-put file (specified using the of option) called `/mnt/nfs1/512MB.dat`; the `dd` command is told to use a block size (specified using `bs` option) of 16K and write a total of 32,768 blocks (specified using the `count` option). Because 16K/block times 32,768 blocks equals 512MB, you will create the intended file. After this command is executed, it will print a few lines such as the following:

```
```
32768+0 records in
32768+0 records out
1.610u 71.800s 1:58.91  61.7%  0+0k  0+0io 202pf+0w
```
```

Here the `dd` command has read 32,768 records from the `/dev/zero` device and also wrote back the same number of records to the `/mnt/nfs1/512MB.dat` file. The third line states that the copy operation took 1 minute 58.91 seconds. Write this line in a text file as follows:

```
```
Write, 1, 1.610u, 71.800s, 1:58.91, 61.7%
```
```

Here you are noting that this was the first (1) write experiment.

+   6.  To measure the read performance of your current NFS setup, you can simply read the 512MB file you created in step 5 and see how long it takes to read it back. To read it back and to time the read access, run the following command:

```
```
time dd if=/mnt/nfs1/512MB.dat \
     of=/dev/null \
     bs=16k count=32768
```
```

Here the `dd` command is timed again to read the `/mnt/nfs1/512MB.dat` file as input and output the file contents to `/dev/null`, which is the official bottomless bit bucket for Linux. As before, you should record the time used in the same file you wrote down the read performance record. For example, the read test using the above command displayed the following output on my system.

Record the third line as follows:

```
```
Read, 1, 1.970u, 38.970s, 2:10.44, 31.3%
```
```

Here you are noting that this was the first (1) read experiment.

+   7.  Now remove the 512MB.dat file from /mnt/nfs1 and unmount the partition by using the umount /mnt/nfs1 command. The unmounting of the NFS directory ensures that disk caching does not influence your next set of tests.

+   8.  Repeat the write and read back test (steps 5 to 7) at least five times. You should have a set of notes as follows:

```
```
Read,   1. 1.971u, 38.970s,  2:10.44, 31.3%
Read,   2. 1.973u, 38.970s,  2:10.49, 31.3%
Read,   3. 1.970u, 38.971s,  2:10.49, 31.3%
Read,   4. 1.978u, 38.970s,  2:10.49, 31.3%
Read,   5. 1.978u, 38.971s,  2:10.49, 31.3%

Write, 1. 1.610u, 71.800s,  1:58.91, 61.7%
```
```