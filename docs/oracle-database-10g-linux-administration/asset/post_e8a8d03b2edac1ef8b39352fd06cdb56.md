
Since the data is guaranteed not to change, it is unnecessary to perform regular backups on the read-only data. If a backup has been performed at some time in the past, this backup should be good for the life of the tablespace.

Since the read-only tablespace is not modified by Oracle, it is possible to place the tablespace on read-only media such as a CD-ROM or a WORM drive. If this data is archival in nature but must be available, a CD-ROM is an excellent choice.

## Creating Read-Only Tablespaces

All tablespaces are created read-write and must have data populated in them before they are useful. Once the data and indexes have been created to your specification, the tablespace can be made read-only either via the ALTER TABLESPACE command or within the Oracle Enterprise Manager.

The tablespace can also be made read-only with the ALTER TABLESPACE command, as shown here. The syntax used will look something like this:

```
ALTER TABLESPACE "t81" READONLY;
```

There are several uses for the read-only tablespace, but they are fairly specific. Whether or not you can take advantage of them depends on your applications.

If you have a large amount of static data that can be put on slower media, the read-only tablespace may be advantageous for you. Also, if you want to guarantee that archival data is not modified, this may also work for you.

## Temporary Tablespaces

Temporary tablespaces are used in order to perform sort operations that cannot fit into memory. By allocating a tablespace specifically for sorting, it is unnecessary to allocate and deallocate space in tablespaces that are used for other purposes, thus causing fragmentation.

When a sort operation cannot fit in memory, it must create and use a temporary segment. This temporary segment allocates extents and will continue to allocate extents until it has enough room to perform the sort. With large DSS queries these temporary segments can become quite large.

By having tablespaces specifically for this type of operation, not only will the sorts be more efficient, but there will be less temporary usage on your data tablespaces.

## Creating Temporary Tablespaces

A tablespace can be made temporary when it is created with the CREATE TABLESPACE command, or it can be changed from a permanent tablespace to a temporary tablespace by using either the GUI tools or the ALTER TABLESPACE command. A tablespace can be changed to temporary using a syntax similar to this:

```
ALTER TABLESPACE "t82" TEMPORARY;
```

It is rare that you will ever be changing a tablespace from permanent to temporary or temporary to permanent. Typically, temporary tablespaces will be created one way or the other, and remain that way for the duration of their existence.

## Tablespace Tricks and Tips

The tablespace is the resource from which the schema objects obtain their space. It can be thought of as similar to a filesystem on a set of disk drives. The space is there and allocated, but is not used until somebody creates a file or saves some data. This is also true of the Oracle tablespace.

As schema objects are created, extents are allocated from the tablespace. These extents are allocated based on the storage parameters of the schema creation, or in lieu of them, the tablespace’s default storage parameters.

Oracle tries to balance space within the tablespace based on the percentage of freespace available. This can cause some problems, however.

If you have two 18GB disk drives and create an Oracle tablespace with two datafiles—one of 10GB on the first disk drive and one of 5GB on the second—Oracle will proportionally fill the datafiles such that the larger one has twice as much data. This is all fine and good, but will typically cause more I/Os to be done on the disk drive with the larger tablespace. This imbalance is not good. If you need multiple datafiles, it is better to spread them equally among disk drives.

Other ways to better balance the I/O load are to take advantage of hardware features or OS features, such as disk striping. By striping your disk drives either with a disk array or software striping, the load will be fairly well balanced among all of the disk drives in the stripe.

Configuring and managing tablespaces can be a time-consuming task, requiring a lot of up-front planning. This planning is well worth it, however. Time spent planning now can mean much less time spent fixing problems later.

### Tablespace Maintenance

Once the tablespaces have been created, your job is not over. It is necessary to monitor both the space used and the load balancing of your tablespaces. Capacity planning and sizing are very important duties. By anticipating problems and solving them before they become critical, you will avoid costly problems.

By monitoring the system and planning for the future, you can also avoid costly downtime.

### Monitoring the Tablespace

Tablespaces can be monitored via the Enterprise Manager or a variety of third-party applications that are very good at graphically showing tablespaces, extents, and segments. Although it is a good idea to monitor your tablespaces regularly, locally managed tablespaces have made tablespace management much easier.

> **Use RAID Rather than Tablespace Load Balancing**
> 
> Disk striping can be an easy way to balance the I/O load between disk drives. A hardware or software disk array will evenly distribute the data among all of the disk drives in the stripe.
> 
> The old-fashioned way of laying out Oracle Databases was to create tablespaces with many datafiles and spread them among individual disk drives. This has been replaced with the more modern standard of creating large RAID stripes and fewer, large datafiles in a tablespace.

## Perform Regular Tablespace Monitoring

Try scheduling several days during the month to monitor system performance. Put it on your calendar at the beginning of the month. Designate several different days of the week and times of day so you get some different samples.

The most important task in tablespace management is space management. It is not unusual for databases to grow much faster than you initially anticipated. This can cause serious space problems if you are not prepared.

### Load Balancing

It is very important to monitor the physical I/O usage of your disk drives in order to make sure you are not experiencing performance problems. Periodically look at the physical disk statistics during peak and non-peak usage periods. Don’t rely on anything staying the same. The performance characteristics of your system are constantly changing and must be monitored.

## Data Blocks

Within Oracle, the space used to store data is controlled by the use of logical structures. These structures consist of segments, extents, and data blocks. A segment is a set of extents used to store a particular type of data. Segments, in turn, are made up of collections of pieces called extents, which are themselves composed of data blocks (see Figure 2-2). A block is the smallest unit of storage in an Oracle Database. The database block contains header information concerning the block itself, as well as the data.

![](img/9479df2d00f5e62b87366b125224950f_73_0.png)

**FIGURE 2-2.** *Segments, extents, and data blocks*

## Nonstandard Block Sizes

Prior to *Oracle9i*, all blocks in the database were the same size. The block size was determined at database creation and was fixed. From *Oracle9i* forward, the initial database is still created with a single block size, but additional tablespaces can be created with different block sizes. This allows a single database to be optimized for both OLTP and data warehousing applications. This can be useful for different types of database activity. Small block sizes are very efficient for OLTP type activity, whereas large blocks are great for data warehousing and decision support applications.

Data blocks are the smallest pieces that make up an Oracle Database. Every I/O operation to disk and Oracle data operation in memory is done at the block level, although multiple blocks can be written or read at a time. Oracle data is stored on disk, and in memory, in blocks. The block size of a tablespace is determined at tablespace creation time. The size of a data block can vary depending on what you choose and can be as small as 512 bytes or as large as 64KB.

*Oracle9i* introduced the concept of nonstandard block sizes. With *Oracle9i* and Oracle Database 10g servers, you can now have a database with different tablespaces utilizing different block sizes.

The Oracle block is the basic building block of all the data stored within the Oracle Database. The Oracle block holds row pieces within the block. A row piece is either an entire row, a part of a row, or a pointer to a row. If only a part of a row is stored in the block, then this is said to be a chained row. If a pointer to a row is stored in the block, then this is a migrated row. Chained and migrated rows are discussed later in this section.

The block itself consists of several parts. The beginning of the block is made up of the block header. Next is the table directory, followed by the row directory. The rest of the block is made up of free space and row data. How the block is allocated between free space and row data is determined by the block allocation parameters PCTFREE and PCTUSED, which are described later in this section. The block header, the table directory, and the row directory are considered overhead and usually take up 84 to 107 bytes of space. The different parts of the block are described here:

### Block Header

The block header contains information about the block, such as the block address and the type of segment that the block is a part of. As you will learn later in this chapter, there are several different types of segments, such as data segments and index segments.

### Table Directory

The table directory contains information about the table data that is stored in the block.
