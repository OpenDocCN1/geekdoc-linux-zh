
## 3.15.5 Multiple File Systems: Mounting

Section 3.3 introduced the concept of file system mounting. In UNIX, unlike DOS or Windows, all files on all volumes are part of a single directory hierarchy; this is achieved by mounting one file system onto another. What exactly do we mean by mounting one file system onto another? To make it clear, suppose that we have a root file system that looks in part like the one in Figure 3.7.

![](img/edd55012c780b4e999320d08ab27959e_168_0.png)

Figure 3.7: Root file system before mount

It has a subdirectory named data with two subdirectories named a and c. Notice that c is not empty. Suppose this file system is located on one internal disk of the computer, and suppose that there is a second internal disk that contains its own file system, as shown in Figure 3.8. The second disk is represented by a device special file named `/dev/hdb`. There is a file system on this second disk, whose root has two subdirectories named staff and students, and students has subdirectories grad and undergrad. To make the files in this second file system available to the users of the system, it has to be mounted on a mount point. A mount point is a directory in the root file system that will be replaced by the root of the mounted file system.

![](img/edd55012c780b4e999320d08ab27959e_168_1.png)

Figure 3.8: File system `/dev/hdb`

If the directory `/data/c` is a mount point for the `/dev/hdb` file system, then we say that `/dev/hdb` is mounted on `/data/c`. The following mount command will mount the `/dev/hdb` file system on `/data/c`. It does not matter that c contains files already; the mount merely hides them while it is there. They would disappear from view until the file system was unmounted, when they would reappear.

```
```sh
$ mount /dev/hdb /data/c
```
```

After this command, the root file system will be as in Figure 3.9.

![](img/edd55012c780b4e999320d08ab27959e_169_0.png)

Figure 3.9: Root system after mount of /dev/hdb

The absolute pathname of the grad directory would then be /data/c/students/grad.

In reality, we would have to specify the type of file system written on /dev/hdb, unless it is the default file system, and only the superuser is allowed to run the mount command, with a few exceptions, such as mounting removable storage devices such as CD-ROMs, DVDs, and USB devices.

When a directory becomes a mount point, the kernel restructures the directory hierarchy. The directory contents are not lost; they are masked by the root directory of the mounted file system. The kernel records in a list of mount points that this file system is mounted on this directory. Different versions of UNIX implement mounting in different ways. This relevant part of this discussion is that operations that traverse the tree can identify mount points because they are directories that are the roots of different file systems than their parents.

## 3.15.6 Duplicate I-node Numbers and Cross-Device Links

The advantage of mounting is that it simplifies the user's conceptualization and navigation of the file hierarchy. It is a single hierarchy. One problem that the kernel must deal with is that there may be many files with the same i-number, since i-numbers are unique only within a single file system. In fact, the root of every file system has i-number 2, and its "." entry is also 2, so there will be many i-nodes with i-number 2. The kernel is able to distinguish i-nodes because i-nodes are also known by the name of the device on which they are located. On all modern UNIX systems, the i-node contains a member that stores the name of the device on which it is located. It is like having a dog tag on a dog; if the dog gets lost, someone can look at it and know where it came from. (I'll admit i-nodes can't wander around, but a process looking at a memory copy of an i-node may need to know which device it got it from.) So i-nodes are more accurately represented by (i-number, device number) pairs.

To pursue this line of thought, suppose there is a file in the root file system with i-number 52. Suppose it has a hard link named /data/a/doc1. Suppose also that, referring to the figure above, /dev/hdb has a file /students/undergrad/hwkl with i-number 52. If UNIX allowed the creation of a hard link across the two file systems with the call

```
link("/data/a/doc1", "/data/c/students/grad/doc1")
```
