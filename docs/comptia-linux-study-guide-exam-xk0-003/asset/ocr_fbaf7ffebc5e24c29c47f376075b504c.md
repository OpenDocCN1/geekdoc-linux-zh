Non-x86 distributions need boot loaders, too, but they’re different from x86 boot loaders in various details. Sometimes a boot loader such as GRUB or LILO is ported or copied on non-x86 distributions. The IA-64 platform uses a boot loader called ELLILO, for instance. Other times, a completely new boot loader is used, such as Yaboot for PowerPC systems.

At a bare minimum, Linux needs a single partition to install and boot. This partition is referred to as the root partition, or /. This partition is so called because it holds the root directory, which lies at the “root” of the directory “tree”—all files on the computer are identified relative to the root directory. The root partition also stores directories, such as /etc and /bin, that fall off the root directory and in which other files reside. Some of these directories can serve as mount points—directories to which Linux attaches other partitions. For instance, you might mount a partition on /home.

One important directory in Linux is /root, which serves as the system administrator’s home directory—the system administrator’s default program settings and so on go here. The /root directory is not to be confused with the root (/) directory.

One partitioning strategy that’s common on high-performance systems is a Redundant Array of Independent Disks (RAID). In a RAID configuration, partitions on separate physical hard disks are combined together to provide faster performance, greater reliability, or both. Some Linux distributions provide RAID options in their initial installation procedures, but others don’t. RAID configuration is fairly advanced and is covered later in “Using RAID.” If you’re new to Linux, it’s best to avoid RAID configurations on your first installation. You might try implementing a RAID configuration on subsequent installations.

# ## Common Optional Partitions

In addition to the root partition, many system administrators like creating other partitions. These are some advantages that come from splitting an installation into multiple partitions rather than leaving it as one monolithic root partition:

**Multiple disks** When you have two or more hard disks, you must create separate partitions—at least one for each disk. For instance, one disk might host the root directory, and the second might hold /home. Also, removable disks (floppies, CD-ROMs, and so on) must be mounted as if they were separate partitions.

**Better security options** By breaking important directories into separate partitions, you can apply different security options to different partitions. For instance, you might make /usr read-only, which reduces the chance of accidental or intentional corruption of important binary files.