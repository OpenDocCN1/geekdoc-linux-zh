
## 7.10 Vital Statistics for Common Backup Devices

| Device | Cost of Drive | Cost of Media | Uncompressed Capacity | Speed | Access Type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Tape | $200–$4,000 | $0.15–$1.00/GB | 24–800GB | 1–120MB/s | Sequential |
| Hard disks | $10–$100 (for removable mounting kit or external enclosure) | $0.15–$0.50/GB (including mounting frame) | 80–2000GB | 20–100MB/s | Random |
| Optical discs | $25–$350 | $0.04–$0.50/GB | 650MB–50GB | 1–72MB/s | Random |

The types of devices that appear in Table 7.10 are those most often used for completely backing up Linux systems. Removable disks (such as USB flash drives or Zip disks) are often used for backing up a few files. Tapes are the traditional backup medium of choice, since they’ve historically been inexpensive on a per-gigabyte basis. Hard disks and optical discs are now cost-competitive with tape, though. Removable hard disks may provide greater capacity and convenience. These drives may be installed either in special internal drive frames that permit easy swapping or in external drive enclosures that plug into the computer via SCSI, FireWire, or USB ports. Optical discs, depending on the exact format used (CD-R, recordable DVD, or Blu-ray), may be even less expensive but are somewhat lacking in capacity compared to hard disks or tapes.

You may want to design a backup system that uses multiple backup types. For instance, you might perform full backups to a removable hard disk and then perform daily incremental backups onto optical discs. Such a plan can take advantage of the best features of each backup medium.

> If you restrict computers’ main installation partitions to about 8GB, those entire partitions will most likely fit, when compressed, on standard single-layer recordable DVDs. This can simplify backup and recovery efforts.

It’s generally wise to keep multiple backups and to store some of them away from the computers they’re meant to protect. Such off-site storage protects your data in case of fire, vandalism, or other major physical traumas. Keeping several backups makes it more likely you’ll be able to recover something, even if it’s an older backup, should your most recent backup medium fail.

If you decide to use hard disks in removable mounts as a backup medium, you’ll need ordinary internal drives and mounting hardware. The hardware comes in two parts: a mounting bay that fits in the computer and a frame in which you mount the hard drive. To use the system, you slide the frame with hard drive into the mounting bay. You can get by with one of each component, but it's best to buy one frame for each hard drive, which effectively raises the media cost. From a Linux software point of view, removable hard disk systems work like regular hard disks or other removable disk systems, like Zip disks. The disks are likely to be partitioned, and the partitions are likely to hold ordinary Linux filesystems.

Tapes are accessed via special tape device files, such as `/dev/st0` or `/dev/nst0` (for devices that use SCSI drivers) or `/dev/ht0` or `/dev/nht0` (for devices that use PATA drivers). Many backup programs, such as `tar`, can access the tape device file directly.

Optical discs require special programs to write, but they can be mounted much like hard disks. The programs used to write to optical discs are described in the upcoming section "Writing to Optical Discs."

## Common Backup Programs

Linux supports several backup programs. Some are tools designed to back up individual files, directories, or computers. Others build on these simpler tools to provide network backup facilities. Basic backup programs include `tar` (described earlier in this chapter in "Handling Tarballs"), `dump`, and `cpio`. ARKEIA (http://www.arkeia.com) and BRU (http://www.tol1sgroup.com) are two commercial backup packages that provide explicit network support and GUI front-ends. AMANDA (http://www.amanda.org) is a network-capable scripting package that helps `tar` or `dump` perform a backup of an entire network. When dealing with tapes, the `mt` program is useful for controlling the tape hardware. This section provides a look at the `cpio`, `dump`, `restore`, and `mt` tools for performing backups.

### The cpio Utility

The `cpio` program is similar in principle to `tar`; it creates an archive file that contains copies of the original files. You can create a `cpio` archive on your hard disk or direct `cpio` to create the archive directly on a tape device. The `cpio` utility has three operating modes:

- **Copy-out mode**: This mode, activated by using the `-o` or `--create` option, creates an archive and copies files into it.
- **Copy-in mode**: You activate copy-in mode by using the `-i` or `--extract` option. This mode extracts data from an existing archive. If you provide a filename or a pattern to match, `cpio` will extract only the files whose names match the pattern you provide.
- **Copy-pass mode**: This mode is activated by the `-p` or `--pass-through` option. It combines the copy-out and copy-in modes, enabling you to copy a directory tree from one location to another.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_365_0.png)

The names for the copy-out and copy-in modes are confusing.

In addition to the options used to select the mode, `cpio` accepts many other options, the most important of which are summarized in Table 7.11. To back up a computer, you'll combine the `--create` (or `-o`) option with one or more of the options in Table 7.11; to restore data, you'll do the same but use `--extract` (or `-i`). In either case, `cpio` acts on file-names that you type at the console. In practice, you'll probably use the redirection operator (`<`) to pass a filename list to the program.

#### Table 7.11 Options for use with cpio

| Option | Abbreviation | Description |
| :--- | :--- | :--- |
| `--reset-access-time` | `-a` | Resets the access time after reading a file so that it doesn't appear to have been read. |
| `--append` | `-A` | Appends data to an existing archive. |
| `--pattern-file=filename` | `-E filename` | Uses the contents of *filename* as a list of files to be extracted in copy-in mode. |
| `--file=filename` | `-F filename` | Uses *filename* as the `cpio` archive file; if this parameter is omitted, `cpio` uses standard input or output. |
| `--format=format` | `-H format` | Uses a specified format for the archive file. Common values for *format* include `bin` (the default, an old binary format), `crc` (a newer binary format with a checksum), and `tar` (the format used by `tar`). |
| N/A | `-I filename` | Uses the specified *filename* instead of standard input. (Unlike `-F`, this option does not redirect output data.) |
| `--no-absolute-filenames` | N/A | In copy-in mode, extracts files relative to the current directory, even if filenames in the archive contain full directory paths. |
| N/A | `-O filename` | Uses the specified *filename* instead of standard output. (Unlike `-F`, this option does not redirect input data.) |
| `--list` | `-t` | Displays a table of contents for the input. |
| `--unconditional` | `-u` | Replaces all files, without first asking for verification. |
| `--verbose` | `-v` | Displays filenames as they're added to or extracted from the archive. When used with `-t`, displays additional listing information (similar to `ls -l`). |

### Using cpio or tar to Back Up a Computer

The `cpio` and `tar` commands are generally considered the lowest common denominator backup programs. Tapes created with `cpio` or `tar` can be read on non-Linux systems—something that’s often not true of `dump` archives, whose format is tied to specific filesystems. For this reason, `dump` must explicitly support whatever filesystem you intend to back up. In mid-2009, `dump` supports Linux’s ext2fs, ext3fs, ext4fs, and an XFS-specific `dump` variant is also available, but versions that support other filesystems, such as ReiserFS and JFS, are not yet available.

To compress data, `cpio` and `tar` both rely on an external program, such as `gzip` or `bzip2`, to compress an entire archive. Alternatively, most tape drives support compression in their hardware. Therefore, if your tape drive supports compression, you should *not* compress a `cpio` or `tar` backup. Let the tape drive do that job.

To back up a computer with `cpio`, a command like the following will do the job:

```bash
# find / | cpio -o /dev/st0
```

Because `cpio` expects a list of files on standard input, this command uses the `find` command and a pipe to feed this information to `cpio`. The `-o` option then tells `cpio` to create an archive, and `-F` specifies where it should be created—in this case, it uses `/dev/st0` to create the archive on the tape device.

> Both the `find` command and pipes were described in more detail in Chapter 2, “Using Text-Mode Commands.”

This command, though, has some negative effects. Most notably, it backs up everything, including the contents of the `/proc` filesystem and any mounted removable disks that might be present. You can use the `-xdev` option to `find` to have that program omit mounted directories from its search, but this means you’ll have to explicitly list each partition you want to have backed up. For instance, you might use a command like the following to back up the `/home`, root (`/`), `/boot`, and `/var` partitions:

```bash
# find /home / /boot /var -xdev | cpio -o /dev/st0
```

> Because tape is a sequential-access medium, the system will restore items in the order in which they were backed up. Therefore, for the fastest partial restores, list the filesystems that you most expect to have to restore first. In this example, `/home` is listed first because users sometimes delete files accidentally. Backing up `/home` first, therefore, results in quicker restoration of such files.

The procedure for backing up with `tar` is similar; however, `tar` doesn’t need a list of files piped to it; you provide a list of files or directories on the command line:

```bash
# tar cvpf /dev/st0 --one-file-system /home / /boot /var
```
