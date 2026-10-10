
Some of these problems are very real and serious. Missing libraries, for instance, must be installed. Other problems, like mismatched package names, are artifacts of the packaging system and are likely symptoms of using packages from a variety of sources. Unfortunately, it’s not always easy to tell into which category a conflict fits. When using a package management system, you may be able to use the error message returned by the package system, along with your own experience with and knowledge of specific packages, to make a judgment.

When installing tarballs, and sometimes when compiling a program from source code, you won’t get any error messages during installation; you’ll see problems only when you try to run the program. These messages may relay an inability to locate a library or run a file, or they may cause the program to crash or otherwise misbehave. Conflicts can be particularly insidious with tarballs because you won’t be warned about conflicts, so installing a package can break an existing one, and you might not notice the damage for some time. You can use the `--keep-old-files` qualifier to keep tar from overwriting existing files, though.

## Workarounds to Package Dependency Problems

When you encounter a package dependency or conflict, what can you do about it? There are several approaches to these problems. Some of these approaches work well in some situations but not others, so you should review the possibilities carefully:

-   Forcing the installation One approach is to ignore the issue. Although this sounds risky, in some cases involving failed dependencies, it’s appropriate. For instance, if the dependency is on a package that you installed by compiling the source code yourself, you can safely ignore the dependency. You can use `rpm`'s `--nodeps` option to force installation despite dependency problems, or you can use `--force` to override some other issues. With `dpkg`, `--ignore-depend=package` and `--force-conflicts` have similar effects. Network-enabled meta-packagers make it difficult to use such options and may subsequently complain about any overrides you make.

-   Upgrading or replacing the depended-on package Officially, the proper way to overcome a package dependency problem is to install, upgrade, or replace the depended-on package. If a program requires, say, Qt 4.5 or greater, you should upgrade an older version (such as 4.4) to 4.5. To perform such an upgrade, you’ll need to track down and install the appropriate package. This usually isn’t too difficult if the new package you want comes from a Linux distribution; the appropriate depended-on package should come with the same distribution.

-   Rebuilding the problem package Some dependencies result from the libraries and other support utilities installed on the computer that compiled the package, not from requirements in the underlying source code. If the software is recompiled on a system that has different packages, the dependencies will change. Therefore, rebuilding a package from source code can overcome at least some dependencies. The `rpmbuild` program does this job for RPM systems, but you’ll need to track down a source RPM for the package.

Source packages are also available for Debian systems, but aside from sites devoted to Debian and related distributions, Debian source packages are rare. The sites that do have these packages provide them in forms that typically install easily on appropriate Debian or related systems. For this reason, it's less likely that you'll rebuild a Debian package from source.

-   Locating another version of the problem package Frequently, the simplest way to fix a dependency problem or package conflict is to use a different version of the package you want to install. This could be a newer or older official version (4.2.3 rather than 4.4.7, say), or it might be the same official version but built for your distribution rather than for another distribution.

## Backing Up and Restoring a Computer

Many things can go wrong on a computer that might cause it to lose data. Hard disks can fail, you might accidentally enter some extremely destructive command, a cracker might break into your system, or a user might accidentally delete a file, to name just a few possibilities. To protect against such problems, it's important that you maintain good backups of the computer. To do this, select appropriate backup hardware, choose a backup program, and implement backups on a regular schedule. You should also have a plan in place to recover some or all of your data should the need arise.

### Common Backup Hardware

Just about any device that can store computer data and read it back can be used as a backup medium. The best backup devices are inexpensive, fast, high capacity, and reliable. They don't usually need to be *random-access* devices, though. Random-access devices are capable of quickly accessing any piece of data. Hard disks, USB flash drives, and CD-ROMs are all random-access devices. These devices contrast with *sequential-access* devices, which must read through all intervening data before accessing the sought-after component. Tapes are the most common sequential-access devices. Table 7.10 summarizes critical information about the most common types of backup device. For some, such as tape, there are higher-capacity (and more-expensive) devices for network backups. Numbers are approximate as of mid-2009. Costs are likely to be lower, and capacities higher, in the future.

**TABLE 7.10** Vital Statistics for Common Backup Devices

| Device | Cost of Drive | Cost of Media | Uncompressed Capacity | Speed | Access Type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Tape | $200–$4,000 | $0.15–$1.00/GB | 24–800GB | 1–120MB/s | Sequential |
| Hard disks | $10–$100 (for removable mounting kit or external enclosure) | $0.15–$0.50/GB (including mounting frame) | 80–2000GB | 20–100MB/s | Random |
| Optical discs | $25–$350 | $0.04–$0.50/GB | 650MB–50GB | 1–72MB/s | Random |

The types of devices that appear in Table 7.10 are those most often used for completely backing up Linux systems. Removable disks (such as USB flash drives or Zip disks) are often used for backing up a few files. Tapes are the traditional backup medium of choice, since they’ve historically been inexpensive on a per-gigabyte basis. Hard disks and optical discs are now cost-competitive with tape, though. Removable hard disks may provide greater capacity and convenience. These drives may be installed either in special internal drive frames that permit easy swapping or in external drive enclosures that plug into the computer via SCSI, FireWire, or USB ports. Optical discs, depending on the exact format used (CD-R, recordable DVD, or Blu-ray), may be even less expensive but are somewhat lacking in capacity compared to hard disks or tapes.

You may want to design a backup system that uses multiple backup types. For instance, you might perform full backups to a removable hard disk and then perform daily incremental backups onto optical discs. Such a plan can take advantage of the best features of each backup medium.

> **TIP**
> If you restrict computers’ main installation partitions to about 8GB, those entire partitions will most likely fit, when compressed, on standard single-layer recordable DVDs. This can simplify backup and recovery efforts.

It’s generally wise to keep multiple backups and to store some of them away from the computers they’re meant to protect. Such off-site storage protects your data in case of fire, vandalism, or other major physical traumas. Keeping several backups makes it more likely you’ll be able to recover something, even if it’s an older backup, should your most recent backup medium fail.

If you decide to use hard disks in removable mounts as a backup medium, you’ll need ordinary internal drives and mounting hardware. The hardware comes in two parts: a mounting bay that fits in the computer and a frame in which you mount the hard drive. To use the
