
maintain backward compatibility. One exception is when you are dealing with VDISK (see "Virtual DASD (VDISK)" on page 264 for more information about this topic).

## Volume label and real device address

The volume label and the real device address both apply to the real DASD pack that houses this particular virtual DASD device. These parameters are provided for informational purposes and you are not likely to need to refer to them unless you are a system administrator.

## Size in cylinders

The size of DASD devices is given in cylinders. For 3390 DASD, a single cylinder is exactly equivalent to 849,960 bytes, which in turn is roughly equivalent to 850 KB.

**Notes:**

- To determine how many megabytes your x cylinder DASD device holds, multiply x by 0.85.
- To determine how many cylinders you should have for x MB of data, multiply x by 1.2.

## Creating DASD

At some time, you might require more disk space. However, the definition of a new DASD pack must be performed by an administrator, because a new virtual DASD device must be backed by a real disk somewhere, and general users do not have the authority to allocate from real disks.

You might, however, have the authority to create a TDISK or a VDISK; refer to "Temporary DASD (TDISK)" on page 262 and "Virtual DASD (VDISK)" on page 264 for details about these topics. Another option might be to ask your administrator for shared file pool (SFS) space; refer to 5.3.11, "The CMS Shared File System" on page 272 for further details.

## Accessing another user's DASD

This book described the concepts of accessing someone else's disks ("Accessing another user's disk (linking)" on page 130). With the proper authority you can read from and execute programs, or even write to the other disk. Refer to that section for detailed information about the subject.

## Removing DASD

You can remove a DASD device in the same way you would remove any other virtual device, by using the DETACH command. As its only parameter, this command takes the virtual device number of the device to detach. See Example 5-34.

### Example 5-34 Example of the DETACH command

```
DETACH 592
DASD 0592 DETACHED
```

Do not be concerned that you will lose anyone else's data by detaching a disk that you linked. When you detach a disk, all you are doing is removing the virtual device within your virtual machine that points to the real disk. (This is not true, however, for TDISKs and VDisks.)

## Temporary DASD (TDISK)

A TDISK is a virtual DASD device that is allocated from a pool of real DASD packs set aside specifically for the creation of temporary disks. TDISK is an abbreviation of temporary disk.

**Important:**

- When you log off or the system fails, any TDISKs that you have created are destroyed and the data is lost. A TDISK is meant to be used as temporary storage space.
- Do not store the only copy of important data on a TDISK.

TDISKs cannot be linked by other user IDs.

z/OS hint: A temporary z/VM DASD is similar to z/OS temporary data sets, for instance by specifying:

```
DSN=&&DATASET,DISP=(NEW,DELETE)....
```

### Creating a TDisk

Not all z/VM installations allow the creation of TDISKs. This might be the case for your installation if the system administrator has not set up the system for TDISK allocation, or if all TDISK space is in use at the time of your request.

However, you can request a TDISK allocation by using the DEFINE T3390 command. The T3390 argument specifies that you want to create a temporary model 3390 DASD device.

Note that DEFINE T3390 command takes two parameters: the virtual device number you want to assign to the new disk, and the size of this disk in cylinders.

If you want a TDISK at device number 9FF that is 100 cylinders in size, use the command shown in Example 5-35.

### Example 5-35 Defining a TDISK

```
DEFINE T3390 9FF 100
DASD 09FF DEFINED
```

> Note: If you want an x megabyte TDISK, multiply x by 1.2 to determine how many cylinders to specify during creation.

You can use the QUERY VIRTUAL DASD command to verify that your 9FF disk exists, as shown in Example 5-36.

### Example 5-36 Verifying that a TDISK was created

```
QUERY VIRTUAL DASD
DASD 0190 3390 LX6RES R/O 107 CYL ON DASD CD31 SUBCHANNEL = 0005
DASD 0191 3390 DKCD37 R/W 005 CYL ON DASD CD37 SUBCHANNEL = 0000
DASD 019D 3390 LX6W01 R/O 146 CYL ON DASD CD32 SUBCHANNEL = 0006
DASD 019E 3390 LX6W01 R/O 250 CYL ON DASD CD32 SUBCHANNEL = 0007
DASD 0401 3390 LX6W01 R/O 146 CYL ON DASD CD32 SUBCHANNEL = 0009
DASD 0402 3390 LX6W01 R/O 146 CYL ON DASD CD32 SUBCHANNEL = 0008
DASD 0405 3390 LX6W01 R/O 156 CYL ON DASD CD32 SUBCHANNEL = 000A
DASD 0592 3390 LX6W01 R/O 070 CYL ON DASD CD32 SUBCHANNEL = 000B
DASD 09FF 3390 (TEMP) R/W 100 CYL ON DASD 59D4 SUBCHANNEL = 000C
```

Notice that there is no volume label for the TDISK, because it is residing in TDISK, and not on a specific real DASD pack.

To use this TDISK space to store temporary files, you must CMS-format the disk when you access it. We use the disk file mode of F for Example 5-37.

### Example 5-37 Format TDISK

```
format 9ff f
DMSFOR603R FORMAT will erase all files on disk F(9FF). Do you wish to continue?
Enter 1 (YES) or 0 (NO).
1
DMSFOR605R Enter disk label:
tmp9ff
DMSFOR7331 Formatting disk F
DMSFOR7321 100 cylinders formatted on F(9FF)
Ready; T=0.01/0.05 10:44:37
```
