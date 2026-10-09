
mature, this security concern should be resolved, and with the added flexibility of software zoning, it will become the preferred method. Another option for protecting from unauthorized access to a storage device is through logical unit number (LUN) masking. A LUN is nothing more than a logical disk. When a node requests access to a storage device, it is given through the LUN. The storage device can either accept or reject the request to this logical disk. The access control list is user defined but maintained through the device control access program. You will see this later in this chapter, as we consider the StorW@rk Specialist that is used in the IBM Enterprise Storage Server, also known as the Shark. Most shops use one large zone and LUN masking for segregation.

## When the Fabric Fills Up

As your infrastructure expands, you need to expand the fabric to accommodate the new devices. (Remember that new ERP project!) Adding more Fibre Channel switches is the easiest method and has many benefits. Adding more switches is referred to as switch cascading. You can add switches to the fabric dynamically without powering off anything, but extreme caution must be used, so follow the manufacturer's instructions carefully. With switch cascading comes increased bandwidth with the added Inter-Switch Links (ISLs), and extended high availability of the fabric because more switches mean more device ports. You sometimes just need more distance in the fabric, and switch cascading can make this an easy task. As you add switches, you also end up with a distributed name server across the fabric, which adds to the fault tolerance of the fabric itself. However, you still have a limit of 239 total switches in the fabric. Be careful, as you add to the SAN fabric, that you do not create a bottleneck of traffic through the fabric and that the hop count maximum is not exceeded. The hop count maximum varies, depending on the hardware and software used in the fabric.

## SAN Enterprise Storage Management Standards

With the mix of SAN hardware vendors, you would hope that every company is not doing its own thing. If this were the case, you would see incompatibility across the SAN, LAN, and WAN, actually across the entire enterprise. The good news is that vendors are working to come up with some standards for SAN hardware, software, and control mechanisms to make everything work together as one cohesive unit. The vendors group called the Storage Network Management Working Group (SNMWG) is working to come up with industry standards for the management and reliability of the SAN as an entire environment, which extends to the application level, where there must be a standard for APIs as well.

Management of the SAN infrastructure involves a consolidation of all of the available tools into one management application. This must encompass data, storage, and network management, and you need to think of the SAN as one entity. We have all heard that data is the driver that makes or breaks a business, and Quality of Service (QoS) is always at the heart of the discussion. So it should come as no surprise that the quality of the data must be maintained, or we can all just go home. Centralized management of the SAN is usually accomplished through some kind of control workstation using a central SAN management tool. This is a must because of the explosion of servers and copies of data. Now one Systems Administrator is expected to manage three terabytes of data. Automation is the key to making this possible, and the SAN management tools provide it. We do not want to manage everything one server at a time!

The SAN management tool must be able to handle all of the following SAN pieces:

- SAN resources
- SAN data
- SAN elements
- SAN network
- SAN fabric performance monitoring/correction
- SAN error monitoring/correction

Industry standards are being focused on the combination of these elements. We often hear the terms *inbound* and *outbound* in connection with management of SAN elements. Inbound refers to the internal communication between elements within the SAN fabric. This communication uses the SCSI Enclosure Services (SES) protocol, also known as SCSI-3 Enclosure Services. This is totally internal to the SAN and does not have any LAN connectivity. Other inbound standards are in the works. Outbound refers to the external communications of the SAN internals using TCP/IP. This is normally done using the Simple Network Management Protocol (SNMP) and the Management Information Base (MIB). These are both widely used protocols supported by most LAN and WAN vendors. Both of these methods provide a monitoring path for the SAN internals.

# Tivoli SANergy

Another aspect of a SAN is the capability for file sharing among machines. With file sharing, you have more control and better consolidation of data. IBM uses Tivoli *SANergy* for this purpose. Some of the benefits of Tivoli SANergy include file sharing at the speed of a SAN, LAN-free and serverless data movement, and heterogeneous file sharing. I recommend the following Redbook for details on installing, configuring, and using SANergy: *A Practical Guide to Tivoli SANergy*, `http://www.redbooks.ibm.com/pubs/pdfs/redbooks/sg245146.pdf`.

# ENTERPRISE STORAGE SERVER (ESS) A.K.A. THE SHARK

The Enterprise Storage Server (ESS), code name Shark, is a consolidated storage device that consists of two tightly coupled RS/6000 or pSeries machines that have full failover capability. The internal storage uses SSA disk subsystems, which are attached in loops. The disks can be configured as RAID 5 or non-RAID, known as JBOD (just a bunch of disks). As of this writing, only RAID 5 is supported. However, in the next release support for RAID 0+1 is to be added. Some people call this RAID 10, but there is really no such standard. RAID 0+1 will add more options to get faster I/O capability. RAID 5 will perform better than JBOD when your load is mainly reads and sequential operations because the data is striped across all of the drives, which translates into more spindles and read/write heads in action. This allows more I/O to be performed in parallel. When RAID 0+1 is added, you will see a huge increase in write capability, too. See Table 29-2 for a description of the different RAID levels.

There is a potential problem with the LVM's locking mechanism when you have multiple paths from the server to the Shark. Here is an example of what can happen: A colleague and I were adding a long list of logical volumes using a shell script before we realized that the volume group was not configured as a “Big” volume group. So, we just entered the command to change the VG on the fly, `chvg -B <vg_name>`, expecting that whenever the VG lock got a break, it would change the characteristic of the VG, but it blew up in our face! The lock was on a single path, so the command just went down another path and attempted to change the VG to a big volume group while the LVs were being created. You know what we had to do: stop the LV-creating script, remove all of the previously configured LVs, make the VG a Big VG, and restart the LV creation script. I never tried that again! So the LVM needs a better handle on controlling multipaths during VG locks. The Austin Development Center is aware and is working on a solution.

The ESS allows for storage consolidation and high-performance data solutions. The ESS supports all of the major platforms, including UNIX, Windows, and mainframes. Another huge benefit of the ESS lies in the areas of disaster recovery and data availability. The ESS design has no single point of failure and allows for failover servicing, which eliminates downtime.

## Table 29-2. Disk RAID Levels

| Level | Description |
| :--- | :--- |
| RAID 0 | Disk striping without fault tolerance |
| RAID 1 | Disk mirroring with duplexing and fault tolerance |
| RAID 2 | Disk striping with error correction using an algorithm |
| RAID 3 | Disk striping with parity information on a single disk |
| RAID 4 | Disk striping with large data blocks and one disk reserved for parity |
| RAID 5 | Disk striping with parity information distributed evenly among the drives |
| RAID 0+1 | Disk mirroring of RAID 0 arrays. Highest data transfer performance |
