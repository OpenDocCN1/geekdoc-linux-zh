local disk storage. You can launch instances in any EC2 Region and you can choose to specify an Availability Zone if needed. Once launched, the instances are attached to your account and should remain running until you shut them down.

Each instance is protected by a firewall which, by default, blocks all internal and external connectivity. When you launch instances you can associate any number of security groups with them. The security groups allow you to control access to your instances on a very granular basis.

The EC2 infrastructure provides instances with an IP address and a DNS entry when they're launched. The address and the entry are transient: when the instance shuts down or crashes they are disassociated from the instance. If you need an IP address that will survive a shutdown or that can be mapped to any one of a number of machines, you can use an Elastic IP Address. These addresses are effectively owned by your AWS account rather than by a particular EC2 instance. Once allocated, the addresses are yours until you decide to relinquish them.

The instances have an ample amount of local disk storage for temporary processing. Like the standard IP address and DNS name, this storage is transient and is erased and reused when you're finished with the instance.

Elastic Block Store (EBS) volumes can be used for long-term and more durable storage. You can create a number of EBS volumes, attach them to your instances, and then format the volumes with the file system of your choice. You can make snapshot backups to S3, and you can restore the snapshots to the same volume or use them to create new volumes.

EC2 charges accrue based on the number of hours the instance runs and the amount of data transferred in and out. There is no charge to transfer data to and from other AWS services in the same Region. The charges for EBS volumes are based on the size of the volume (regardless of how much data is actually stored) and there are also charges for I/O requests. To prevent hoarding, you are charged for Elastic IP addresses that you allocate but don't use.

The EC2 **CloudWatch** feature provides monitoring within EC2. It collects and stores information about the performance (CPU load average, disk I/O rate, and network I/O rate) of each of your EC2 instances. The data is stored for two weeks and can be retrieved for analysis or visualization.