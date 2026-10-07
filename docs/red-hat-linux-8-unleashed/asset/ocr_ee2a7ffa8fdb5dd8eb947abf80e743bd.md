A heavily used system, the files being backed up can change during the backup, and the restored files might be in an unstable condition. LVM can also make snapshots of the logical volume that can then be mounted and backed up.

Red Hat now supports an implementation of LVM, and includes a set of more than a dozen LVM software tools for creation, modification, and maintenance of volume groups. For more information, read the LVM homepage at http://www.sistina.com/products_lvm.htm, which offers information, help, and downloadable files via FTP.

# Filesystem Manipulation

Different people have various learning styles. For those of you who prefer examples rather than lectures, there are a few practical examples in which you learn to create a filesystem within a file and mount it using the loopback filesystem—a special filesystem that allows us to accomplish this useful feat. You can use the filesystem you create to experiment with and practice almost all the commands found in this chapter with no fear of damaging your system.

# Creating a Filesystem for Testing

Because most of us don't have a spare computer or hard drive on which to experiment and practice, we can make one of our by creating an image file containing the filesystem of our choice and using the loopback filesystem to mount it. That way, we don't run the risk of accidentally wreaking havoc on the system itself. Although you could also use a floppy drive for these exercises, their small size limits your flexibility.

Step 1—Make a Blank Image File

Use the dd command to create a file with a block size of 1024 bytes (a megabyte) and create a file that is 10MB in size. (You need to have enough space on your hard drive to hold a file this big, so adjust the size accordingly.) We want 10,000KB (1024-byte) blocks, so we select a floppy count of 10000.

If we wanted a floppy-sized image, we would have selected a block size of 512 and a count of 2880 for a 1.4MB floppy or 5760 for a 2.88MB floppy. Here's how to do that:

```
# dd if=/dev/zero of=/rhlest.img bs=1024 count=10000
```

We see the computer respond with the following:

```
10000+0 records in
10000+0 records out
```

If we check our new file with the file command, we see this:

```
# file /tmp/rhlutest.img
/tmp/rhlutest.img: data
```