Once proper Datafile location has been considered, the next step to maximizing Datafile I/O is to perform the read and write activity to the Datafiles as quickly as possible.

# Performing Datafile I/O Quickly to Improve Performance

After balancing the I/O requests by separating tables and indexes into their own tablespaces, you can try to perform the I/Os against these structures as quickly as possible. Performing Datafile I/O quickly is achieved in three ways: by placing high I/O Datafiles on separate disk drives and controllers, stripping tablespaces, and tuning the DB_FILE_MULTIBLOCK_READ_COUNT init.ora parameter.

# Segregating Datafiles by Drive and Controller

Improving I/O performance by separating table segments from their associated indexes was explained in the previous section. By additionally ensuring that two different devices are used to store these Datafiles and that these devices are attached to two separate disk controllers, I/O performance can be improved even more.

# Datafile Striping

The idea of separating Datafiles onto distinct devices can be extended even further through a technique called *striping*. When a Datafile is striped, it is stored across several devices, not just one. This increases I/O performance because multiple sets of disk drive heads are brought into use when a read or write of the Datafile is required. The easiest way to stripe a Datafile is to store the Datafile on a *RAID* device. A RAID, or Redundant Array of Independent Disks, consists of several physical disks that can be managed and accessed as if they were one or more physical devices. Therefore, placing a Datafile on a RAID device implicitly causes the file to be striped across all the devices in the RAID. This technique does not require any special action on the part of the DBA.

Two key considerations when using RAID striping are the *stripe width* and *stripe depth*. The number of devices across which the stripe is built determines stripe width. *Stripe depth* refers to the amount of data that will be written to one device before moving to the next. Ask your storage array vendor the recommended stripe width and depth configuration for their hardware.