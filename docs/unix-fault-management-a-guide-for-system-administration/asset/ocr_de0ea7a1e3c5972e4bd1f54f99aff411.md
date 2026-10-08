# Failure of a Peripheral

In addition to the internal computer components, other important components are attached to the system. These peripheral devices include tape drives, disk devices, printers, and CD-ROM drives.

A variety of errors can affect tape drives. Tape devices should be monitored proactively, because backups normally have a small window of time to complete. Detecting failures and recovering before the backup window starts can help to ensure that the backup will succeed. You should also watch for mount requests during the backup process, to keep the backup application from being blocked for too long.

Disk errors and failures are an increasing problem, because the amount of stored information continues to grow. Many high availability environments now use RAID devices, which provide data redundancy by spreading data across an array of disks. Data can thus be reconstructed from surviving disks in the event of a disk failure. The arrays can even be repaired online. In addition to monitoring for disk failures, you may want to monitor the logical volume status, physical volume status, I/O errors, and the loss of a mirrored copy of data. Each of these types of failure conditions can be detected with monitoring software.

Various printer events can be interesting to monitor. For example, the printer can jam, fail, or be set offline. Also, the print spooler can fail and the queue can be full. Printers require vigilant monitoring because they can often get into a state in which they are not performing properly. It is important to detect problems and fix them quickly to avoid receiving user complaints.

CD-ROM drives are perhaps the least interesting of the peripheral devices to monitor. You may be interested in knowing when a drive is mounted or unmounted, but receiving only drive failure notifications is usually sufficient.

# Failure or Loss of an External Service

Hardware or software failures are not the only critical events that can occur on your system. Monitoring your corporate networks is critical as well. With the movement away from mainframes to distributed client/server environments, the dependency on local area networks (LANs) and wide area networks (WANs) is increasing. If the proper precautions are not taken in designing the company data center, the loss of a single network could cause denial of service to all clients trying to access critical server machines. You also need to understand the purpose of each of your networks so that you know the consequences of a failure. For example, in a high availability environment, you have networks that are used for sending data between systems, networks dedicated for high availability status checking, and backup networks.

You can check a variety of networking faults and statistics to further analyze the status of your networks. You should watch for connectivity problems and “Node Unreachable” errors. You can also check Ethernet collision rates and use performance tools to check network bandwidth utilization.

A UNIX server is dependent on external services, such as network services. For example, a server may be active, but the Domain Name System (DNS) server for its domain may be down, preventing clients from connecting successfully. An e-mail server is another example of a machine in this category.