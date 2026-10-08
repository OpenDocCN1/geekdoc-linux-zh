cracking it. Since this is a virtual machine that people can’t access without accessing your host operating system, password authentication on this virtual machine is less important, but still, choose wisely.

Click **Continue**, and you will be asked to set your timezone. Do so and then continue.

The next screen asks about partition disks. Choose **Guided – use entire disk**, and Kali will detect your hard drives and set up a partitioner automatically.

Kali will then warn you that all data on the disk you select will be erased… but don’t worry! This is a virtual disk, and the disk is new and empty, so this won’t actually do anything. Click **Continue**.

Kali will now ask you if you want all files in one partition (a partition is just what it sounds like—a portion or segment of your hard drive) or if you want to have separate partitions. If this was a production system, you probably would select separate partitions for /home, /Var and /tmp, but considering that we will be using this as a learning system in a virtual environment, you should simply select **All files in one partition**.

Now you be will asked whether to write your changes to disk. Select **Finish Partitioning and write changes to disk**. Kali will prompt you once more to see if you want to write the changes to disk; select **Yes** and click **Continue**.