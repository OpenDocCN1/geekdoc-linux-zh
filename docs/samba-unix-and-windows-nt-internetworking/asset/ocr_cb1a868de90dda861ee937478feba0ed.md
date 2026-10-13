|  |  |
|---|---|
| Backup Browser | 0x01 |
| Standby Browser | 0x02 |
| Master Browser | 0x04 |
| Domain Master Browser | 0x08 |
| WINS Client | 0x20 |
| Windows NT Server | 0x80 |

Each domain also has a domain master browser whose responsibility is to synchronize the share datasets between all the local master browsers. The domain master is the collection point for intersubnet browsing. The domain PDC always acts as the domain master browser. In single-subnet domains, the PDC is the domain master browser and local

# File Systems

When it comes to file systems, MS Windows is the 24-flavors ice cream shop of operating systems. Popular flavors include FAT, FAT16, FAT32, OS/2 HPFS, NTFS, and DFS. Then there are the UNIX interoperability flavors: NFS and Samba. Windows provides a great deal of functionality in supporting legacy and contemporary file systems. This capability is especially useful in heterogeneous environments, regardless of whether there are multiple versions of Windows or a mixture of Windows and other operating systems.

# FAT

The file allocation table (FAT) file system represents the basic common denominator for file and directory support across the family of Windows platforms. The FAT architecture is essentially an indexed table that references data containers called clusters within a partition of contiguous space on a disk. A cluster represents the smallest unit of storage on a disk. Cluster size ranges from 512 to 32K bytes depending on disk size and format.

Because cluster size represents the smallest container for a file or directory, it may be important to tailor the file system and drive format to meet the file size profile for a particular data set.

FAT file systems are defined by four control areas. The first or reserve area contains the boot sector, bootstrap program, and partition table. The next area is the FAT index of clusters, followed by the root directory table, which is a directory of files and top level directories. The fourth area is the file area collection of clusters where data are stored.

FAT architecture has evolved over the years in keeping with the availability of larger disks and the demand for larger file sizes. Basically, this has meant an increase in the number of bits in the FAT used to index clusters. More index bits means more clusters can be