# ## Creating DVDs from the Command Line

There are several competing formats for DVD (Digital Versatile Disk), and with prices rapidly falling, it is more likely that DVD-writing drives will become commonplace. The formats are as follows:

+   - DVD+R
+   - DVD-R
+   - DVD+RW
+   - DVD-RW

Differences in the + and − formats have mostly to do with how the data is modulated onto the DVD itself with the + format having an edge in buffer underrun recovery. How this is achieved impacts the playability of the newly created DVD on any DVD player. The DVD+ format also has some advantages in recording on scratched or dirty media. Most drives support the DVD+ format. As with any relatively new technology, your mileage may vary.

We will focus on the DVD+RW drives because most drives sold support that standard. The software supplied with Fedora Core has support for writing to DVD-R/W (re-writable) media as well. It will be useful for you to review the DVD+RW/+R/-R[W] for Linux HOWTO at http://fy.chalmers.se/~appro/linux/DVD+RW/ before attempting to use the dvd+rw-tools that you will need to install to enable DVD creation (also known as “mastering”) as well as the cdrtools package. You can ignore the discussion in the HOWTO about kernel patches, compiling the tools.

> **TIP**
> The 4.7GB size of DVD media is measured as 1000 megabytes per gigabyte, instead of the more commonly used 1024 megabytes per gigabyte, so don’t be surprised when the actual formatted capacity, about 4.4GB, is less than you anticipated. The dvd+rw-tools will not allow you to exceed the capacity of the disk.

You need to have the dvd+rw-tools package installed (as well as the cdrtools package). The dvd+rw-tools package contains the growisofs application (that acts as a front end to mkisofs) as well as the DVD formatting utility.

You can use DVD media to record data in two ways. The first way is much the same as that used to record CDs in a “session,” and the second way is to record the data as a true file system using packet writing.

# Session Writing

To record data in a session, you use a two-phase process:

+   - Format the disk with `dvd+rw-format` `/dev/sdcd0` (only necessary the first time you use a disk).
+   - Write your data to the disk with `growisofs` `-Z` `/dev/sdcd0` `-R -J` `/your_files`.