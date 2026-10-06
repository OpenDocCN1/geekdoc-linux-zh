# Deciding Whether to Upgrade in Place or Install from Scratch

The actual procedures for upgrading an operating system are very specific to each individual operating system. However, you will usually use one of the following general methods for upgrading:

+   - Upgrade the operating system in place.
- Install the new operating system from scratch.

An-place operating system upgrade replaces critical system files like the kernel, libraries, and standard UNIX utilities with newer versions. It leaves your data alone, including home directories and configuration files. These advantages would seem to make an “in place” upgrade the most logical choice for an upgrade procedure, but this type of upgrade offers some significant disadvantages as well. More often than not, an in-place upgrade replaces a configuration you didn't mean to replace or causes several of your applications to fail.

You often find that small problems like these occur after an in-place upgrade, making your system's behavior unpredictable or “quirky.” Additionally, you may find that various “relics” of the old operating system remain, especially in old configuration files that may no longer be valid. In-place upgrades not give you the opportunity to partition your disks to accommodate the additional potential storage needs of the new operating system; this problem is discussed in more detail in “Guaranteeing Adequate Disk Space for the Upgrade,” later in this chapter.

The alternative to an in-place upgrade is to install the new operating system from scratch. This is the only method that guarantees a fresh installation of the operating system with no relics or conflicts from past installations. It also allows you to partition your disks to reflect the storage needs of the new operating system (if they have changed at all). These are big advantages, but reloading from scratch also comes with the following disadvantages:

+   - All of your old configurations will be lost.
- Many locally installed applications will have to be reinstalled.
- It will take much longer to perform the upgrade than it would with an in-place upgrade.

# You Can Preserve Data from Some File Systems

Most operating system software will recognize nonsystem file systems and ask if you want them preserved. This is especially useful for file systems dedicated to home directories and software repositories. Even if you choose to preserve some file systems, be sure to make full backups of all of your file systems, just in case something goes wrong and you lose the data on your disk. Installing an operating system is a complex process, and disasters like this happen to everyone at some point.