You will get an output that shows you all the devices mounted on your system, which will show the partitions as:

/dev/sda1

/dev/sda2

Now, plugin the USB drive and run the same command “sudo fdisk -l” again. You will see an additional device this time, which is your USB drive. It will show up as something like

/dev/sdb

with the size of your USB drive next to it.

Proceed to write the image carefully on the USB drive using the command shown below. The example assumes that the name of your Kali Linux ISO file is “kali-linux-2019.1-amd64.iso” and it is in your present working directory. The block size parameter bs can be increased but the ideal value would be ‘bs=512k’.

dd if=kali-linux-2019.1-amd64.iso of=/dev/sdb bs=512k

The writing to the USB drive will take a few minutes, and it is not abnormal for it to take a little more than 10 minutes to finish writing.

The dd command will not show any output until the process is completed. If your USB drive has an LED, you will see it blinking which is an indicator that the disk write is in progress. Once the dd command has been completed, the output will be something like this.

5823+1 records in

5823+1 records out

3053371392 bytes (3.1 GB) copied, 746.211 s, 4.1 MB/s

That is the end of it. You can now use the USB drive to boot into Kali Linux Live or start and installation of Kali Linux on a machine.

# **Creating a Kali Linux Bootable USB Drive on a MAC OS X Operating System**