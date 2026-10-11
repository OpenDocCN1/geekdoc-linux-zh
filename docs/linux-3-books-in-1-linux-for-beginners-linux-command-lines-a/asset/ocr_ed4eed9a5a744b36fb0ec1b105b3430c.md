using the following name: # cryptsetup luksOpen /dev/sdb1 my_encrypted_partition.

We will now save the partition using the format ext4. To do this, run the following command: # mkfs.ext4 /dev/mapper/my_encrypted_partition. This will allow you to create a mount point in your partition, which will help you mount the partition encrypted in the partition. You can also use the commands below to determine if the mount operation is successful:

```
# mkdir /mnt/enc
# mount /dev/mapper/my_encrypted_partition /mnt/enc
# mount | grep partition
```

If you are done reading from or writing to the file system you have encrypted, you need to unmount it using the following command: # umount /mnt/enc. Once you do this, you can close the LUKS partition using the following command: # cryptsetup luksClose my_encrypted_partition.

# Testing Encryption

Now that you have encrypted the file, you need to check if the partition or swap you have encrypted is safe.

+   **Step One:** The first thing you need to do is enter the LUKS partition you have created. To do this, run the command: # cryptsetup luksOpen /dev/sdb1 my_encrypted_partition

+   **Step Two:** Now, enter the passphrase you entered to encrypt the file

+   **Step Three:** The next thing to do is to mount the partition using the following command: # mount /dev/mapper/my_encrypted_partition /mnt/enc

+   **Step Four:** You need to create a dummy file in the mount point using the command: # echo “This is Part 3 of a 12-article series about the LFCE certification” > /mnt/enc/testfile.txt

+   **Step Five:** You also need to verify if you can access and use the files you have created in the mount point using the command: # cat /mnt/enc/testfile.txt

+   **Step Six:** To unmount the system, you need to enter the command: # umount /mnt/enc

+   **Step Seven:** Now that this is done, you can close the partition using the