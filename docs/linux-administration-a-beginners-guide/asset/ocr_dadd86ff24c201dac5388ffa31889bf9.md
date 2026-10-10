# **Linux Administration: A Beginner's Guide**

At a minimum, you need to have two partitions: one for holding all of the files and the other for swap space. Swap space is usually sized to be double the available RAM if there is less than 128MB of RAM, or the exact same amount of RAM if there is more than 128MB. Realistically, you will want to separate partitions for /oss, /var, /home, and /tmp in addition to a root partition. Obviously you can adjust this equation based on the purpose of the server.

# **OTHER PARTITION MANIPULATION TASKS**

Once you have gone through the steps of adding a partition, and you are comfortable with the variables involved (mount points, sizes, types, devices, and so on), the actual process of editing and deleting partitions is quite simple. Editing an entry means changing the exact same entries that you established when you added the partition, and deleting an entry requires only that you confirm you really want to perform the deletion.

One last detail that we have intentionally omitted is the process of adding Network file mounts (NFS). This requires a more complete explanation and is covered in Chapter 8.

# **Formatting Partitions**

This screen will present you with a list of all the newly created partitions (see Figure 2-8). Because we are wiping the disk of previous installations, we want to select all of the partitions to be formatted. (More accurately, Red Hat will be creating a file system on it.)

![](bbox=[0.15, 0.55, 0.85, 0.87])

Figure 2-8. Screen for formatting partitions