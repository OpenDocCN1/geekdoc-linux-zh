+   ■ **Server message block file system (SMBFS)** A mountable SMBFS for Linux that allows Windows- or Linux-based workstations access to directory/file shares on a network-based Linux server.

+   ■ **Network file system (NFS)** NFS, as presented in Chapter 2, is a framework designed to allow a user on a client workstation to access remotely files over a network on a network-based server.

# INTRODUCTION

The Linux+ certified professional needs to have a good understanding of the creation, administration, and management of the Linux filesystem environment. This chapter presents the strategies for the creation of filesystems, the different types of filesystems, the tools used to create filesystems, and the tools used to administer filesystems.

# FILESYSTEM TYPES

The computer architecture is comprised of many critical components. In Chapter 2, we discussed many of those critical components (for example, hardware, disk drive, and partition) during the installation of the Linux distribution. For this section, we will discuss Linux filesystem types in greater detail. A filesystem provides the operating system with a framework [a structure] for the storage, organization, modification, removal, and retrieval of digital information.

To achieve this objective, filesystems are responsible for organizing and maintaining files, folders, metadata, and residual data as containers for storing digital information. Regardless of the selected filesystem type, data containers can be as large as terabytes (TB) in size or as small as a sector. The size of a sector can vary among the different filesystem types; it is the smallest amount of disk space that can be assigned to hold a file. The default size of sector is typically 512 bytes.

Each form of data is described below:

+   ■ **Files** are sectors of allocated space within a filesystem used for storing digital information, which is available to access or execute. The allocated space can be contiguous or noncontiguous. To identify files, files are assigned a filename, which is identified by a sequence of alphanumerical and/or Unicode character sets. In some cases, while not mandatory, a filename can include a dot followed by a series of alphanumerical and/or Unicode character sets (for example, report.doc