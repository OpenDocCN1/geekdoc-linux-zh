If you're already jumping ahead to configuration of the encrypted filesystem in the /etc/fstab file, this UUID corresponds to the original partition and is not associated with the encrypted filesystem. To find the UUID associated with this particular encrypted filesystem, run the following command:

```
# dumpe2fs /dev/mapper/test | grep UUID
```

That UUID number can then be used to represent the encrypted volume in /etc/fstab. The following are two ways such a volume could be configured in that file:

```
/dev/mapper/test   /test   ext4   defaults   1 2
UUID=uuidnumber    /test   ext4   defaults   1 2
```

Alternatively, the aforementioned mkfs.ext4 command would change the associated UUID, as confirmed by the output to the blkid command. That UUID in the blkid command output can then be used to represent the noted volume in a similar fashion.

If successful, you'll be prompted for the passphrase for any LUKS-encrypted filesystems that may have been created. One common related error is the unloading of the dm_crypt module during the system reboot process.

# CERTIFICATION OBJECTIVE 6.06

# Filesystem Management

Before you can access the files in a directory, that directory must be mounted on a partition formatted to some readable filesystem. Linux normally automates this process using the /etc/fstab configuration file. When Linux goes through the boot process, directories specified in /etc/fstab are mounted on configured volumes, with the help of the mount command. Of course, you can run that command with any or all appropriate options. So that's an excellent place to start this section.

The remainder of this section focuses on options for /etc/fstab. While it starts with the default using the baseline configuration for the standard virtual machine, it includes options for how you can customize that file for local, remote, and removable filesystems.