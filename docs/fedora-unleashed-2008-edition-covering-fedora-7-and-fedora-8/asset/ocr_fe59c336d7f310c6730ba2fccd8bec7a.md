# NOTE

You can also use the blank = option with the cdrecord command to erase CD-RW disks. The cdrecord command has fewer options than xisrofs does, but it offers the multi option, which enables you to make multisession CDs. A multisession CD enables you to write a data track, quit, and then add more data to the CD later. A single-session CD can be written to only once; any leftover CD capacity is wasted. Read about other options in the cdrecord man page.

Current capacity for CD media is 700MB of data or 80 minutes of music. (There are 800MB/90 minute CDs, but they are rare.) Some CDs can be overburned; that is, recorded to a capacity in excess of the standard. The cdrecord command is capable of overburning if your CD-RW drive supports it. You can learn more about overburning CDs at http://www.cdmediaworld.com/hardware/cdrom/cd_oversize.shtml/.

# Creating DVDs from the Command Line

There are several competing formats for DVD, and with prices rapidly falling, it is more likely that DVD-writing drives will become commonplace. The formats are as follows:

+   - DVD+R
+   - DVD-R
+   - DVD+RW
+   - DVD-RW

Differences in the + and - formats have mostly to do with how the data is modulated onto the DVD itself, with the + format having an edge in buffer underrun recovery. How this is achieved impacts the playability of the newly created DVD on any DVD player. The DVD+ format also has some advantages in recording on scratched or dirty media. Most drives support the DVD+ format. As with any relatively new technology, your mileage may vary.

We focus on the DVD+RW drives because most drives support that standard. The software supplied with Fedora has support for writing to DVD-R/W (rewritable) media as well. It will be useful for you to review the DVD+RW/+R/-RW for Linux HOWTO at http://fy.chalmers.se/~appro/linux/DVD+RW/ before you attempt to use dvd+rw-tools, which you need to install to enable DVD creation (also known as mastering) as well as the cdtools package. You can ignore the discussion in the HOWTO about kernel patches and compiling the tools.

# TIP

The 4.7GB size of DVD media is measured as 1000 megabytes per gigabyte, instead of the more commonly used 1024 megabytes per gigabyte, so do not be surprised when the actual formatted capacity, about 4.4GB, is less than you anticipated. dvd+rw-tools does not allow you to exceed the capacity of the disk.