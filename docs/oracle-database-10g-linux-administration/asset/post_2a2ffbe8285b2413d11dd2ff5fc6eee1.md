
tablespace will be created with the locally managed option unless otherwise specified.

Locally managed tablespaces manage the extents within the tablespace itself. This allows for a more scalable solution by reducing the contention on the Data Dictionary. Within locally managed tablespaces, the extents can either be created in a uniform size or in a progressively larger size. With locally managed tablespaces, a bitmap is used to manage the extents within the tablespace. In addition, when modifying extents, no rollback information is created, as was done with dictionary managed tablespaces.

With a locally managed tablespace, the extent size can either be determined automatically on a per tablespace basis or it can be specified in the storage clause for a given database object. If you specify the extent size, it will be uniform throughout the tablespace.

## Manual or Automatic Space Segment Management

Within the tablespace, the freespace in the segments can either be managed via freelists or with a bitmap. Using freelists is the traditional method of managing segments within a tablespace and uses the PCTUSED and PCTFREE parameters, as described later in this chapter. Freelist segment management is configured by specifying MANUAL in the segment management clause. New with Oracle9i is the bitmap method of managing free space within segments. This is known as automatic space segment management and is the preferred method of managing segments. Bitmap extent management is enabled by specifying AUTO.

## Creating Tablespaces

Creating a tablespace consists of specifying one or more datafiles and storage parameters. The datafiles can either be filesystem files or raw devices. The storage parameters specify how the tablespace is used. They are very important and will be discussed in greater detail later in this chapter.

Creating tablespaces is done with the CREATE TABLESPACE command using various options. Not every option will be covered here, since there are so many of them, and since you can easily look them up, but let’s look at a few of them. The basic commands to create a tablespace are

```
CREATE [UNDO] TABLESPACE *tname*
*DATAFILE data_file_name data_file_size*
*[storage clause]*
*[BLOCKSIZE size [K]]*
*[TEMPORARY]*
*[EXTENT MANAGEMENT DICTIONARY]*
*[EXTENT MANAGEMENT LOCAL [AUTOALLOCATE]]*
*[EXTENT MANAGEMENT LOCAL [UNIFORM SIZE *size* [K,M]]*
*[SEGMENT SPACE MANAGEMENT AUTO]*
*[SEGMENT SPACE MANAGEMENT MANUAL]*
```

Let’s look at these key parameters in a little more detail.

| Parameter | Use |
| :--- | :--- |
| UNDO | The undo parameter specifies that the tablespace you are creating is an undo tablespace. Undo tablespaces are covered in detail in the next chapter. |
| Storage clause | The storage clause specifies the filename, size, and so on. |
| BLOCKSIZE | The BLOCKSIZE parameter is used to allow you to create a nonstandard block size tablespace. |
| TEMPORARY | Specifies that the tablespace is used as a temporary tablespace. |
| EXTENT MANAGEMENT | The EXTENT MANAGEMENT clause allows you to specify whether the tablespace is locally or dictionary managed. |
| SEGMENT SPACE MANAGEMENT | The SEGMENT SPACE MANAGEMENT clause is used to specify AUTOMATIC (bitmap) or MANUAL (freelist) management of free space within segments. |

There are many more optional parameters that can be used to create tablespaces. These optional parameters can be found in the Oracle documentation. Here are a few examples of creating tablespaces.

A locally managed simple tablespace

```
CREATE TABLESPACE *ts1*
*DATAFILE '/u01/app/oracle/oradata/orac/ts01.dbf' SIZE 10M;*
```

Same as the previous, but specifying the details

```
CREATE TABLESPACE ts2
DATAFILE '/u01/app/oracle/oradata/orac/ts02.dbf' SIZE 10M
EXTENT MANAGEMENT LOCAL UNIFORM SIZE 1M
SEGMENT SPACE MANAGEMENT AUTO;
```

A dictionary managed tablespace

```
CREATE TABLESPACE ts3
DATAFILE '/u01/app/oracle/oradata/orac/ts03.dbf' SIZE 10M
DEFAULT STORAGE (INITIAL 1M NEXT 1M PCTINCREASE 10)
EXTENT MANAGEMENT DICTIONARY
SEGMENT SPACE MANAGEMENT MANUAL;
```

A locally managed undo tablespace

```
CREATE UNDO TABLESPACE undo01
DATAFILE '/u01/app/oracle/oradata/orac/undo01.dbf' SIZE 10M;
```

There are a number of optional parameters in the CREATE TABLESPACE command. The Oracle docs will list all of these options.

## Tablespace Size

A normal tablespace can consist of up to 1024 datafiles. An Oracle datafile has a limit of 4 million blocks; thus, the Oracle size limit is 4 million blocks x block size. The maximum size of an OS datafile is OS-dependent; therefore, the maximum size of a datafile is either the size of the maximum OS file, or the Oracle limitation, whichever is smaller.

Oracle 10g has introduced the Bigfile Tablespace. The bigfile tablespace allows you to create one large datafile that is 4 billion blocks in size. The bigfile tablespace is designed to be used with RAID systems that support large datafiles or with ASM. In order to create a bigfile tablespace, use the command CREATE BIGFILE TABLESPACE instead of CREATE TABLESPACE.

## Coalescing the Tablespace

With local management of extents, it is unnecessary to coalesce extents, but with dictionary management it is sometimes necessary. Since the Data Dictionary managed tablespace allocates space to schema objects in extents of various sizes, it is possible that over time this space may become fragmented. As extents are allocated, Oracle looks for free space that is closest in size to the space needed for the new extent. As the tablespace ages, and extents are added and freed, you may find there are many small free extents located next to each other.

By coalescing the tablespace, the adjacent free extents are coalesced into larger free extents, thus making the free space more flexible to new extent allocations. The SMON process will automatically coalesce tablespaces if this feature has not been disabled. It is rarely necessary to coalesce a tablespace by hand, but it is important to know how and why this operation is performed.

## System Tablespace

If your SYSTEM tablespace is locally managed, you cannot create any dictionary managed tablespaces and the preceding example will fail. If you want to create dictionary managed tablespaces, the SYSTEM tablespace must be dictionary managed.

## Adding Datafiles to a Tablespace

It can be faster to add datafiles to a tablespace than to specify them at tablespace creation since adding datafiles can be done in parallel. Datafile creation at tablespace creation time is done serially, one at a time. For a large tablespace creation, this can save significant time.

## Adding Datafiles

It is often necessary to add more datafiles to a tablespace if you need more space or want to spread out I/Os among more disk drives. It is also faster to add datafiles to a tablespace than to create them at database creation time. The CREATE TABLESPACE command works serially, that is, it creates one datafile at a time. By adding datafiles, this operation can be parallelized; thus, multiple datafiles can be added to a tablespace simultaneously.

Datafiles are added by using the ALTER TABLESPACE command, as shown in this example.

```
ALTER TABLESPACE ts1
ADD DATAFILE '/u01/app/oracle/oradata/orac/ts01b.dbf' SIZE 10M;
```

This command will add an additional 10MB datafile to the tablespace named ts1.

## Altering Tablespace Properties

Other properties of the tablespace that can be changed via the ALTER TABLESPACE command are

- 1. Add or rename a datafile
- 2. Bring it offline or online
- 3. Coalesce the extents in a dictionary managed tablespace
- 4. Begin or end backup mode
- 5. Change from permanent to temporary or temporary to permanent
- 6. Change the storage clause, size, or put it into autoextent mode

As you can see, there are a number of options.

## Read-Only Tablespaces

As described earlier, it is possible to alter a tablespace to make it read-only. Read-only tablespaces are similar to read-write tablespaces with the restriction that no changes can be made to the schema objects residing on those tablespaces. When a tablespace is made read-only, the need to back up this tablespace is eliminated.
