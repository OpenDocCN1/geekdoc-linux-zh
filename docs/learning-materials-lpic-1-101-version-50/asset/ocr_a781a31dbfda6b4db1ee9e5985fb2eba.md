# Explorational Exercises

+   1. Consider you have an ext4 filesystem on /dev/sda1 with the following parameters, obtained with tune2fs:

```
```
Mount count:                    8
Maximum mount count:             -1
```
```

What will happen at the next boot if the command tune2fs -c 9 /dev/sda1 is issued?

+   2. Consider the following output of du -h:

```
```
$ du -h
216K    ./.somedir/anotherdir
224K    ./.somedir
232K    .
```
```

How much space is occupied by just the files on the current directory? How could we rewrite the command to show this information more clearly?

+   3. What would happen to the ext2 filesystem /dev/sdb1 if the command below is issued?

```
```
# tune2fs -J /dev/sdb1 -J device=/dev/sdc1 -i 30d
```
```

+   4. How can we check for errors on a XFS filesystem on /dev/sda1 that has a log section on /dev/sdc1, without actually making any repairs?

+   5. What is the difference between the -T and -t parameters for df?