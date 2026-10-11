
| Friday | Full Backup | 2 TB | 6.18 TB |

Table 14.2: Full and differential Backup example

It is possible to observe how the total **Backup** size required using **Different Backup** is bigger than with the **Incremental Backup**. The advantage of this method is that restoring a file from Wednesday’s **Backup** requires only a copy of the Sunday’s (**Full Backup**) and Wednesday’s one (**Different Backup**).

## Backup sources

As described previously, **Backup** is the process of copy data being protected. Depending on the data to be saved, there are different strategies and storage media. Some examples of elements that can be backed up are as follows:

- **Static files**: These are the common elements to be included. These files are usually not modified often, and only new files are copied. For example, the copy can include files used by applications or end users.
- **Dynamic files**: These files are being modified often, such as log files or automatically generated files (such as an exported *database*).
- **Block devices**: The **Backup** can include the whole data in a device, such as a full disk or partition.
- **Virtual Machine**: It is possible to make a **Backup** of the full **Virtual Machine** in two different ways:
  - Using the *hypervisor*, which can create a *snapshot* (a copy of the data in a specific time) and export it to a regular file to be included in the copy.
  - Installing the **Backup client** to perform a full copy of the data inside.
- **Containers**: They have not copied themselves, only the data associated with them (such as *Volumes*).
- **Databases**: A backup of a database can be done in two main ways:
  - Exporting the content and the database structure to regular files to be included in the **Backup**.
  - Copying the associated files directly, thus, ensuring that the data would not be corrupted on the copy. This can approach have the following two options:
    - **Hot Backup**: The **Database** is still running while the backup is being performed.
    - **Cold Backup**: The **Database** is stopped earlier to perform the file-based copy.

## Backup strategies

Deciding a **Backup strategy** is essential to protect the data saved in the case of data loss as well as any possible disaster event. Different strategies are available to mitigate disaster situations, and they are as follows:

- **3-2-1 Rule**: This strategy consists of having three copies, of which two of them are located on the same site but using different media, where the **Backup** is performed to speed up possible recovery of the data. The third copy is **off-site** (different location) to have a safe copy in case of a disaster situation.
- **Remote Backup**: Performing the **Backup** to a remote service which usually is not managed by the owners of the original place. For example, using a service **Backup as a Service** or an *Object Storage solution*.
- **Site-to-Site Backup**: This strategy always copies the data to a location off-site under the current location. Both sites are managed the same owners.
- **Disaster Recovery** is the practice of having a second location, different from the main one, where the services are usually ready to be promoted as a primary. This method requires to have configured the replication between the sites. The biggest advantages of the implementation of **Disaster Recovery Site(s)** are as follows:
  - Reduce downtime, and the secondary site is able to resume the service quickly.
  - Data loss is reduced to the last replication, usually in seconds or minutes.
  - Possibility to go back to the main site when the incident is resolved.

### Backup solution features

**Backup solutions** include different features to improve performance, reduce the size needed and increase the security of the data stored. Some of the popular features are as follows:

- **File locking:** The solution should be able to make a copy even when the file is in use, such as log files or databases data.
- **Data expiration:** Out-of-date data can be automatically deleted after the retention period is over. This feature reduces the space needed in the storage media.
- **Compression:** Compression can be done by the **Backup Solution** or directly applied to the storage media, such as built-in compression in a *Tape*.
- **Deduplication:** One of the most advanced features of **Backup Solution** is avoiding the duplication of data in the storage media. If several systems have the same data, such as using the same operating system, only one copy of the data would be stored in the storage media.
- **Duplication:** The copies can be distributed in different locations; the **Backup Solution** is responsible, after receiving the data from the client, for distributing it properly to different locations, ensuring they are not in the same location.
- **Encryption:** Another advanced feature is to encrypt the data saved in a **Backup**. *Encryption* requires more resources, and it slows the copy and the restore. However, for some environments, it is a requirement.
- **Multiplexing:** A **Backup Solution** is responsible for receiving data from multiple sources and storing them properly.
- **Staging:** For some storage media, intermediate storage is first used to store the media. Usually, making a copy to a *Tape* requires having a disk, which is used temporarily, before sending all the data to the *Tape*.

When all the data is written in the *Tape*, the temporary data is removed from the disk.

### Bacula

This is one of the best open-source **Backup** products available. This solution includes community and commercial support, being a perfect option for small and enterprise companies. Some of the benefits of using **Bacula** are as follows:

- GUI and CLI interface.
- A wide variety of possible backup levels and techniques, including **full**, **differential**, and **incremental**.
- Ability to both backup and restore entire systems or single files easily.
- **Cloud backup** support for AWS S3.
- The capability of using snapshots on Linux/Unix systems. Snapshots can be automatically created and used to backup files.
- Use either the command line and/or GUI to execute and control your backup process.
- Use *partition backup* for your Linux data storage to keep precise images of these disks for easy management and recovery.
- Tape backup is fully supported and allows it to work with a variety of different tape drives, autoloaders, and autochangers. *VTL* support is also included.
- Deduplication developed by themselves.

### Bacula installation

The **Bacula** installation requires to use a *database* to store configuration and all the needed information about the clients and the copies. The available options are **MariaDB** (MySQL) and **PostgreSQL**. When the *Database* is available, the installer configures whatever is needed to use it. The instructions included are for a system using *Ubuntu 22.04* (at the time of writing this book, **Bacula** was still not available on the official repository in Ubuntu) are as follows:

```bash
# Create repository file
echo "deb [arch=amd64] https://bacula.org/packages/5bd703346c037/debs/13.0.1 jammy main" | tee /etc/apt/sources.list.d/Bacula-Community.list

# Add GPG key as trusted
wget -qO - https://www.bacula.org/downloads/Bacula-4096-Distribution-Verification-key.asc | gpg --dearmor > /etc/apt/trusted.gpg.d/bacula.gpg

# Install mariadb-client and bacula-mysql packages
apt install mariadb-client bacula-mysql
```

### Bacula services

**Bacula** is made up of the following five major components or services:

- **Bacula Director:** The Bacula Director service is the program that supervises all the backup, restore, verify, and archive operations.
- **Bacula Console:** The Bacula Console service is the program that allows the administrator or user to communicate with the **Bacula Director**.
- **Bacula File:** This service (also known as the Client program) is the software program that is installed on the machine to be backed up.
- **Bacula Storage:** These services consist of software programs that perform the storage and recovery of the file attributes and data to the physical backup media or volumes.
- **Catalog:** These services are comprised of the software programs responsible for maintaining the file indexes and volume databases for all files backed up.

*Figure 14.2* features the Bacula components:
