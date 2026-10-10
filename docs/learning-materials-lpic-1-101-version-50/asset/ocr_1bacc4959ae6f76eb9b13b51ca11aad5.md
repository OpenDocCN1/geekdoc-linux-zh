# # Answers to Explorational Exerceses

+   1. Consider the following entry in /etc/fstab: /dev/sdc1 /backup ext4 noatime,nouser,async. Can a user mount this filesystem with the command mount /backup? Why?
+   No, the parameter nouser will not allow ordinary users to mount this filesystem.

+   2. Consider a remote filesystem mounted at /mnt/server, which has become unreachable due to a loss of network connectivity. How could you force it to be unmounted, or mounted as read-only if this is not possible?
+   Pass the -f and -r parameters to unmount. The command would be umount -f -r /mnt/server. Remember that you can group parameters, so umount -fr /mnt/server would also work.

+   3. Write an /etc/fstab entry that would mount an btrfs volume with the label Backup on /mnt/backup, with default options and without allowing the execution of binaries from it.
+   The line should be LABEL=Backup /mnt/backup btrfs defaults,noexec

+   4. Consider the following systemd mount unit:
+   ```ini
+   [Unit]
+   Description=External data disk
+   
+   [Mount]
+   What=/dev/disk/by-uuid/56C11DCC5D2E1334
+   Where=/mnt/external
+   Type=ntfs
+   Options=defaults
+   
+   [Install]
+   WantedBy=multi-user.target
+   ```
+   * What would be an equivalent /etc/fstab entry for this filesystem?
+   The entry would be: UUID=56C11DCC5D2E1334 /mnt/external ntfs defaults

+   5. What should be the file name for the unit above, so it can be used by systemd? Where should it be placed?