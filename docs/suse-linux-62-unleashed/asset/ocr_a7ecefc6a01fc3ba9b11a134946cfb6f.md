# Boot Management CHAPTER 3 47

# Note

SUSE Linux offers you a chance to install LILO during initial Linux installation or upgrade. You'll also have the chance to create a boot disk right before the LILO installation process—do it! Even if you don't use the disk, you'll benefit from having a little insurance in cases ever go awry. If you don't install LILO, you'll definitely need the disk.

LILO is installed after you have partitioned your hard drives and after Linux and associated software has been copied to your hard drive. LILO is generally used to boot Linux in one of three traditional ways:

+   * From your hard drive's master boot record (MBR)
* From the superblock of your root Linux partition on your hard drive
* From a floppy disk

The following section shows you list of LILO's configuration parameters and its command-line arguments, and it points out some special features as well.

# Installing and Configuring LILO

Although LILO is easy to install using the lilo command (located under the /bin directory), you should first take the time to read its documentation, which you'll find under this book's CD-ROM docs/loadin directory, or under the /usr/doc/packages/lilo directory after installation. LILO's documentation contains details of its features and provides important tips and workarounds for special problems, such as installing boot loaders on large-capacity hard drives or booting from other operating systems.

# Caution

Before trying anything with LILO, you should have an emergency boot disk (see /usr/doc/howto/en/Bootdisk-HOWTO for more info). Having a system that won't boot is not much fun, and if you don't have a boot disk, you might think there is no possible way to get back in and change things. Spending a few minutes making yourself a boot disk can save you a big headache down the road.

![](bbox=[0.885, 0.445, 0.975, 0.565])