+   - The GUI LVM tool is an alternative for those who don't remember all of the commands required to manage logical volumes.

# Volume Encryption with the Linux Unified Key Setup

+   - The passphrases that can be used with LUKS can be considerably more secure than regular passwords.
+   - Volumes can be LUKS-encrypted during the installation process.
+   - LUKS encryption after installation depends on the dm_crypt module and commands in the cryptsetup-luks package.
+   - The safety of encrypted volumes can be enhanced with random data, added with either the badblocks command from the /dev/urandom random number generator.
+   - The cryptsetup luksFormat /dev/sda1 command sets up a passphrase on the given partition. Once configured, you can format the /dev/mapper device that's created.

# Filesystem Management

+   - Standard filesystems are mounted as defined in /etc/fstab.
+   - Filesystem volumes are now identified by their UUIDs; for a list, run the blkid command.
+   - The mount command can either use the settings in /etc/fstab or mount filesystem volumes directly.
+   - It's also possible to configure mounts of shared network directories from NFS and Samba servers in /etc/fstab.
+   - With the right commands, you can convert an ext2 formatted filesystem to ext3; and then convert an ext3 formatted filesystem to ext4.

# The Automounter

+   - With the automounter, you can configure automatic mounts of removable media and shared network drives.
+   - Key automounter configuration files are auto.master, auto.misc, and auto.net, in the /etc directory.
+   - It's possible to configure an /etc/auto.home file to make home directories available from a remote shared network server.