# Disaster management 1219

A disaster recovery plan should include the following sections (based on the NIST disaster recovery standard, 800-34):

+   - Introduction – purpose and scope of the document
- Concept of operations – system description, recovery objectives, information classification, line of succession, responsibilities
- Notification and activation – notification procedures, damage assessment procedures, plan activation
- Recovery – the sequence of events and procedures required for recovery of lost systems
- Return to normal operations – concurrent processing, reconstituted system testing, return to normal operations, plan deactivation

We are accustomed to using the network to communicate and access documents. However, these facilities may be unavailable or compromised by an insider. Store all relevant contents and procedures off-line. Where to get recent dump tapes and how to make use of them without reference to on-line data.

In disaster scenarios, you will need access to both on-line and off-line copies of essential information. The on-line copies, if possible, be kept on a self-sufficient machine: one that has a rich complement of tools, has keys sysadmin's environments, its own name server, has a complete local /etc/hosts file, has no file-sharing dependencies, has a printed anchor, and so on. Don't use an old junker's tape is no good for anything else; the disaster recovery storage machine should be fast and have plenty of memory and scratch disk space you can use for restores and copies during recovery. The machine needs a complete development environment that it can patch and recompile any compromised software. It helps if the machine also interfaces for all the types of drives used at your site (IDE, SATA, SCSI, FC-AL, etc.).

Here's a list of handy data to keep on the backup machine and in the form of a printed booklet or optical disc:

+   - An outline of the recovery procedure: who to call, what to say
- Service contract phone numbers and customer numbers
- Key local phone numbers: police, fire, staff, boss
- Inventory of backup tapes and the backup schedule that produced them
- Network maps
- Software serial numbers, licensing data, and passwords
- Copies of software installation media (can be kept as ISO files)
- A copy of your systems' service manuals
- Vendor contact info for that emergency disk you need immediately
- Administrative passwords

![](bbox=[0.965, 0.815, 0.995, 0.915])