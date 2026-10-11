
- **NS-8**
  NS-8 is the name given to TR-4 drives that include built-in compression. These drives also support read-after-write operation (which I describe later in this chapter, in the section “Read-After-Write Verification”). Most NS-8 drives use SCSI interfaces.

- **NS-20**
  NS-20 is the compressed variant of TR-5. Like NS-8 drives, NS-20 drives generally use the SCSI interface and support read-after-write verification.

> **NOTE**
>
> NS-8 drives use TR-4 tapes, and NS-20 drives use TR-5 tapes. Some tapes are marketed for one line or another, but marketing aside, there’s no difference between TR- and NS- tapes.

In addition to these versions, a few companies offer nonstandard Travan-like drives. These drives have peculiar capacities, such as 5GB. The media for these drives often look just like ordinary Travan media, but they’re incompatible. I recommend sticking with a standard Travan format, in order to increase your choice in media.

Unfortunately, most Travan drives cannot write to lower-capacity Travan media, although they can usually read lower-capacity media. This fact can make upgrading a Travan drive difficult, because you must replace the (expensive) media along with the drive.

Modern Travan drives generally use the EIDE or SCSI ports on your system, but a few models use unusual interfaces, such as the parallel port or even the USB port. It’s best to stick with the EIDE or SCSI interfaces.

As a general rule, Travan drives are inexpensive ($200–$500 for TR-4 or TR-5 drives in early 2000, for example), but the media are costly ($20–$40 for TR-4 or TR-5 tapes). This fact makes Travan drives an economically good choice if you expect to purchase few tapes, but if you expect to buy many tapes, you might want to consider DAT instead.

Travan drives have a reputation for noise; they make a loud whirring sound, not unlike that of a dentist’s drill, when in operation. Because the tapes spin at such high speed, they also tend to generate a substantial amount of heat, so you should place the drives away from other heat-generating components whenever possible, to avoid exacerbating heat stresses on all components.

## DAT

*Digital Audio Tape* is a tape format that was developed for the storage of audio data, but that’s been adapted for use as a computer data storage medium. DAT cartridges are physically smaller than QIC or Travan cartridges, but they store a lot of data. This feat is accomplished, in part, by the use of more advanced head technology. QIC and Travan drives record data in a handful of linear tracks on the drive. A DAT drive's read/write head resembles that of a VCR—it's tilted at an angle and spins, so that the data tracks cut crosswise. This recording method is known as *helical scan recording* (see Figure 8.3 for a comparison of these data storage methods). DAT drives also use a different encoding method than do linear drives like QIC and Travan devices. This more advanced design allows more data to be stored per square inch on a DAT tape than on a QIC or Travan tape, all other things being equal.

![](img/860d0c38bd76c9ded976e9d1e179ef25_265_0.png)

![](img/860d0c38bd76c9ded976e9d1e179ef25_265_1.png)

### FIGURE 8.3
The rotating DAT head design yields a more efficient data storage pattern on the tape.

Like Travan, DAT drives are available in several variants:

- **DDS-1** The *digital data storage* (DDS) format is used by most DAT drives, and DDS-1 is the first incarnation of that format. DDS-1 drives have an uncompressed capacity of 2GB.
- **DDS-2** DDS-2 doubles the capacity of DDS-1, to 4GB uncompressed.
- **DDS-3** DDS-3 drives have a 12GB uncompressed capacity.
- **DDS-4** These drives have a 20GB capacity, uncompressed.

It's possible to vary these capacities (generally downward) by using shorter tapes. For instance, 1.3GB DDS-1 tapes are not uncommon. Almost all DAT drives support hardware data compression, which produces an average 2:1 compression ratio, thus doubling DAT capacity.

Compared to Travan drives, DAT drives are expensive ($650–$1000 for DDS-2 and DDS-3 drives, and around $1000 for DDS-4 drives), but their tapes are inexpensive ($8–$25 for DDS-2 and DDS-3 tapes, and $30–$35 for DDS-4 tapes). This pricing scheme makes DAT a cost-effective solution if you plan to buy many tapes. DAT drives can usually both read and write earlier DAT versions. You therefore don't need to abandon your old media if you replace a drive with a newer version, but the new drive is likely to be expensive.

DAT drives almost invariably use the SCSI interface, and always have. The drives are much quieter than are Travan or QIC drives, and they usually generate less heat. Their head mechanisms are extremely delicate, however, so you must be careful not to damage a drive, particularly if it's an external unit which might be dropped or receive other shocks.

## Other Tape Drive Types

Although Travan and DAT drives dominate the marketplace for low-end and mid-range tape units, other technologies do exist, and might be of interest to you if you need to back up large quantities of data. Most of these drives are very expensive, costing $1000–$5000 or even more, but if you need to do regular backups of a 60GB server, this cost can be quite well justified. Keep in mind that these are only a few of the high-end tape backup formats. If you have a serious need for ultra-high-capacity backup, you should investigate the market more thoroughly.

## DLT

*Digital Linear Tape* (DLT) is a high-capacity linear tape technology. DLT drives are marketed for servers and other high-capacity markets; they can store 20GB–35GB uncompressed. The drives themselves are quite expensive, unfortunately, costing upward of $3000.

## 8mm

One technology that's related to DAT is the 8mm tape drive. These tapes resemble those used in 8mm video cameras, although the tapes are formulated differently and so shouldn't be interchanged with 8mm videotapes. Exabyte ([http://www.exabyte.com](http://www.exabyte.com)) is the only supplier of 8mm tape drives. Like DAT, 8mm uses helical scan recording. Some models of 8mm drive can store up to 60GB uncompressed, making these drives well suited for very high-capacity installations (at least by the standards of PC storage).

## AIT

The *Advanced Intelligent Tape* (AIT) format ([http://www.aittapeco/](http://www.aittapeco/)) uses cartridges that are superficially similar to 8mm cartridges, but the two are incompatible. Like DLT, AIT tapes can currently store up to 35GB uncompressed.

### Tape Drive Features

No matter what variety of drive you choose to purchase, there are certain features you should look into. Some of these features are more common on some types of drives than on others.

#### Compatibility with Prior Standards

As I described earlier, some types of tape drives, such as DAT drives, are usually compatible with previous versions of the same format. A DDS-3 DAT drive, for example, can usually both read and write DDS-2 and DDS-1 tapes. This characteristic can be useful for two reasons:

- **Using old media** If you have an older drive of the same basic type, replacing that drive with a newer and higher-capacity model of the same basic type enables you to continue to use your existing media, while providing room for greater capacity when you buy new tapes. Similarly, future variants of the same drive type will likely be able to use the tapes you buy for your present drive, which might become important at some point in the future.
- **Low-cost media** Lower-capacity tapes of a given type typically cost less than their higher-capacity counterparts. You might therefore want to purchase tapes of a mix of capacities if you need to make some backups of large amounts of data and others with less data. For instance, full backups are typically quite large, but incremental backups are usually much smaller.

Some tape drive types, such as most Travan drives, support read, but not write, access to older media of the same type. This characteristic can be useful if you keep tapes for archival purposes, or if you need to replace a drive that is broken unexpectedly. It’s not useful if you want to purchase lower-cost and lower-capacity media for smaller backup jobs.

Of course, if you have one tape drive and purchase one of a different type entirely, you’ll have no compatibility with your current media. (The capability of most Travan drives to read some QIC MC tapes is an exception to this rule.)

#### Hardware Data Compression

Most low-end tape drives write data to tape in the form in which they receive it. The problem with this approach is that some backup software, such as tar in conjunction with gzip, creates a backup that’s very sensitive to errors. If even a single bit of the recorded data is flawed, all the subsequent data on the backup becomes useless. Other backup packages, such as the commercial Backup and Recovery Utility (BRU—see http://www.estice.com), don’t suffer from this problem. Hardware data compression is another way around this problem. Instead of using gzip, you set the drive to use compression, which is usually the default configuration.
