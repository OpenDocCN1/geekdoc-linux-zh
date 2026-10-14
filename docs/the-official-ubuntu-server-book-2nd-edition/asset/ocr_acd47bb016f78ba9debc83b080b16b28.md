Of course, dd can use any file as its input and output file, so instead of imaging to another drive, you could image to a file. This is particularly handy for forensics, when you might have a number of file system images stored on a single large USB drive. Assuming you have mounted your USB drive at /media/disk1, here is how you could image /dev/sda to a file on that drive:

```
$ sudo dd if=/dev/sda of=/media/disk1/sda-image.img
```

To restore from this image, you would just reverse the two arguments. Here are the commands to restore the two previous examples:

```
$ sudo dd if=/dev/sdb of=/dev/sda
$ sudo dd if=/media/disk1/sda-image.img of=/dev/sda
```

You can also image individual partitions. This can be useful since you can easily mount the images loopback and read through them. First let's image a partition on /dev/sda:

```
$ sudo dd if=/dev/sda1 of=/media/disk1/sda1-image.img
```

Now you can create a directory, /mnt/temp, and use the loop mount option to mount this image:

```
$ sudo mkdir /mnt/temp
$ sudo mount -o loop /media/disk1/sda1-image.img /mnt/temp
```

This is handy when you need to recover only a few files from an image. You can browse /mnt/temp like any other file system and copy individual files or entire directories from it. To copy this image back to the original drive, reverse the arguments once again:

```
$ sudo dd if=/media/disk1/sda1-image.img of=/dev/sda1
```

Another useful trick is imaging over the network. The fact is that with some servers you might not have a separate disk attached that can hold an image. One method might be to set up a remote NFS server with plenty of storage. Then you could mount the NFS share on the local system and