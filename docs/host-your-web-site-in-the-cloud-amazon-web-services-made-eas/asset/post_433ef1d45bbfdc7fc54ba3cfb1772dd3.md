
# Table 5.2. Sample Security Groups

| Group Name | Rules |
| :----------------------: | :-----------------------------------------: |
| web_access | □ allow HTTP access (port 80) from anywhere <br> □ allow SSH access (port 22) from corporate network |
| db_access | □ allow access to MySQL database (port 3306) <br> □ allow SSH access (port 22) from corporate network |
| app_access | □ allow access to application server (port 5000) <br> □ allow SSH access (port 22) from corporate network |

The security groups would then be applied to the instances as listed in Table 5.3.

# Table 5.3. Instances and Security Groups

| Instance Role | Security Group |
| :----------------------: | :----------------------: |
| web server | web_access |
| database server | db_access |
| application server | app_access |

With a clean and properly factored set of groups as a base, it becomes possible to think about making changes dynamically. For example, a scheduling utility built around the `AuthorizeSecurityGroupIngress` and `RevokeSecurityGroupIngress` AWS functions could make periodic changes to the `app_access` group to implement rotating, remote access by backup system administrators for emergency access. Or, the rules in the `db_access` group could be made more selective by dynamically adding permissions based on the IP addresses of the servers in the web tier.

Instances within a single security group can communicate freely with each other. Therefore, it would be imprudent to use, for example, a single `ssh_access` group to allow SSH access to instances in more than one tier of the previous example.

A public IP address is assigned to each instance as part of the launch process. However, because the instances are ephemeral, the IP address will have the same lifetime as the instance. The EC2 Elastic IP address feature supports allocation of public IP addresses that are stable and that have a lifetime independent of any particular EC2 instance. The addresses are allocated to your AWS account. Once allocated they remain under your control until relinquished, regardless of whether you use them or not. You can attach (route) any of your IP addresses to any of your EC2 instances.

As noted earlier in this section, the local disk storage included with each EC2 instance is ephemeral. The storage will remain intact if a running instance is rebooted, but it’s scrubbed and then reused after the instance has been terminated. The EC2 Elastic Block Store (EBS) provides persistent storage with high reliability and availability. You can create an EBS volume and then attach it to any of your instances in the same Availability Zone. You can create point-in-time snapshot backups to Amazon S3 and then restore the backups to the same volume, or you can use them to create a fresh volume. EBS volumes can be formatted and used to store files, or they can be used as unformatted “raw” storage.

The Amazon DevPay system lets you use Amazon’s subscription and billing infrastructure for your own EC2-based applications. DevPay gives you the ability to create your own payment plan with any combination of up-front, recurring, and usage-based fees. Once you’ve attached the payment plan to an AMI of your creation, your customers can sign up for it and launch one or more copies of the AMI. They’ll pay for usage via their Amazon account.

## All Together Now

Amazon EC2 functionality becomes even more powerful when it’s used in conjunction with the other AWS infrastructure services. We’ve already talked about the use of Amazon S3 for storage of AMIs and EBS snapshots. And, as we saw in the last chapter, you can call the S3 APIs using PHP code running on an EC2 instance. S3 is ideal for storage of any amount of unstructured application data—binary or string.

In a similar fashion, code running on an EC2 instance can use Amazon SimpleDB for structured data store, the Relational Database Service for storage of relational data, and the Amazon Simple Queue Service as a scalable inter-instance or inter-process buffer. Elastic MapReduce runs on EC2 services and can be used to process large amounts of data.

Adding to the appeal of this architectural model is the fact that latency between EC2 services and these services is very low, since they’re running in the same Region.

# The Amazon EC2 Pricing Model

Your Amazon EC2 usage is charged in a number of dimensions that include instance use, data transfer, AMI storage, IP address reservations, EBS data storage, and EBS I/O. These prices will change over time, so you should consult the Amazon EC2 home page[2] for the latest information.

## Instance Use

Hourly (on-demand) pricing for each of the EC2 instance types is shown earlier in Table 5.1. Instance usage begins when the instance starts running, and is billed in whole-hour increments. These are base prices, and several factors can affect the final price:

- It’s more expensive to run EC2 instances in the Europe and Asia Pacific Regions.
- It costs more to run Windows than it does to run Linux or OpenSolaris.
- AMIs accessed via DevPay are charged at the rates set by the AMI’s creator.
- You can arrange for a lower hourly rate by purchasing reserved instances.

Taking all these factors into consideration, you should plan on watching your AWS account with care during the first hours and weeks of operation.

If you plan to keep a number of EC2 instances running over time, you should also investigate the reserved instance option. With this option you pay an up-front fee to reserve an instance for a period of one or three years, and then pay a smaller per-hour charge when you’re actually using the instance. The final per-hour cost is lower than it would be for on-demand usage. At current rates, a three-year reserved instance is less expensive than an on-demand instance if the instance is used at least 19% of the time. Purchase of a reserved instance will also ensure that you can allocate an EC2 instance when you need it.

## Data Transfer

Your data transfer charges are based on the amount of data transferred in and out of your EC2 instances. Data transferred into your instances is charged at a rate of $0.10 per gigabyte. Once again, this amount is prorated. Data transferred out of your instances is charged on a sliding scale that starts at $0.17 per gigabyte and decreases according to volume, reaching $0.10 per gigabyte for all outgoing data transfer in excess of 150 terabytes per month.

There are some important special cases for data transfer:

- There’s no charge for data transfers within an AWS Availability Zone.
- Data transferred between regions is charged at internet rates as described at the beginning of this section. You’ll be charged for both sides of the transfer (out of one region and into the other).
- Data transferred between Availability Zones in the same region is charged at the rate of $0.01 per gigabyte.
- No charges apply to transfer data back and forth between EC2 and other AWS services in the same region.

## AMI Storage

The AMIs that you create are stored directly in Amazon S3 or as EBS snapshots (which are also stored in S3), and you pay the usual S3 rates for doing so. My own customized Linux AMIs typically consume 500 to 700 megabytes of space. Windows AMIs are generally larger, often weighing in at more than five gigabytes. If you create
