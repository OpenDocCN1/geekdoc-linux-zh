
## Availability Zone

An AWS **Availability Zone** represents a set of distinct locations within an AWS Region. Each Availability Zone has independent power grid and network connections so that it’s protected from failures in other Availability Zones. The zones within a Region are connected to each other with inexpensive, low-latency connections. The Region name is part of the zone name. For example, `us-east-1a` is one of four zones in the `us-east-1` Region.

The mapping of a zone name to a particular physical location is different yet consistent for each AWS account. For example, my `us-east-1a` is possibly different to your `us-east-1a`, but my `us-east-1a` is always in the same physical location. This per-user mapping is intentional and was designed to simplify expansion and load management.

The `DescribeAvailabilityZones` function and the `ec2-describe-availability-zones` command return the list of Availability Zones for a Region.

## Region

An AWS **Region** represents a set of AWS Availability Zones that are located in one geographic area. Each AWS Region has a name that roughly indicates the area it covers, but the exact location is kept secret for security purposes. The current Regions are `us-east-1` (Northern Virginia), `us-west-1` (Northern California), `eu-west-1` (Ireland), and `ap-southeast-1` (Singapore). Over time, additional Regions will become available. The `DescribeRegions` function and the `ec2-describe-regions` command return the current list of Regions. You may choose to make use of multiple Regions for business, legal, or performance reasons.

## Access Identifiers

AWS uses a number of different **access identifiers** to identify accounts. The identifiers use different forms of public key encryption and always exist in pairs. The first element of the pair is public, can be disclosed as needed, and serves to identify a single AWS account. The second element is private, should never be shared, and is used to create a signature for each request made to AWS. The signature, when transmitted as part of a request, ensures the integrity of the request and also allows AWS to verify that the request was made by the proper user. AWS can use two different sets of access identifiers. The first comprises an Access Key ID and a Secret Access Key. The second is an X.509 certificate with public and private keys inside. You can view your access identifiers from the AWS portal.⁶

## Amazon Machine Image

An **Amazon Machine Image (AMI)** is very similar to the root drive of your computer. It contains the operating system and can also include additional software and layers of your application such as database servers, middleware, web servers, and so forth. You start by booting up a prebuilt AMI, and before too long you learn how to create custom AMIs for yourself or to share, or even sell. Each AMI has a unique ID; for example, the AMI identified by `ami-bf5eb9d6` contains the Ubuntu 9.04 jaunty server. The DescribeImages function and the `ec2-describe-images` command return the list of registered instances. The AWS AMI catalog⁷ contains a complete list of public, registered AMIs.

## Instance

An **instance** represents one running copy of an AMI. You can launch any number of copies of the same AMI. Instances are launched using `RunInstances` and the `ec2-run-instances` command. Running instances are listed using `DescribeInstances` and `ec2-describe-instances`, and terminated using the `TerminateInstances` function or the `ec2-terminate-instances` command. Before long you will also learn about the AWS Management Console, which is a visual tool for managing EC2 instances.

## Elastic IP Address

AWS allows you to allocate fixed (static) IP addresses and then attach (or route) them to your instances; these are called **Elastic IP Addresses**. Each instance can have at most one such address attached. The “Elastic” part of the name indicates that you can easily allocate, attach, detach, and free the addresses as your needs change. Addresses are allocated using the `AllocateAddress` function or the `ec2-allocate-address` command, and attached to an instance using the `AssociateAddress` function or the `ec2-associate-address` command.

## Elastic Block Store Volume

An **Elastic Block Store** (EBS) volume is an addressable disk volume. You (or your application, working on your behalf) can create a volume and attach it to any running instance in the same Availability Zone. The volume can then be formatted, mounted, and used as if it were a local disk drive. Volumes have a lifetime independent of any particular instance; you can have disk storage that persists even when none of your instances are running. Volumes are created using the CreateVolume function or the ec2-create-volume command, and then attached to a running instance using the AttachVolume function or the ec2-attach-volume command.

## Security Group

A **Security Group** defines the allowable set of inbound network connections for an instance. Each group is named and consists of a list of protocols, ports, and IP address ranges. A group can be applied to multiple instances, and a single instance can be regulated by multiple groups. Groups are created using the CreateSecurityGroup function and the ec2-add-group command. The AuthorizeSecurityGroupIngress function and the ec2-authorize command add new permissions to an existing security group.

## Access Control List

An **Access Control List** (ACL) specifies permissions for an object. An ACL is a list of identity/permission pairs. The GetObjectAccessControlPolicy function retrieves an object’s existing ACL and the SetObjectAccessControlPolicy function sets a new ACL on an object.

## AWS Infrastructure Web Services

Now that you know the key concepts, let’s look at each of the AWS infrastructure web services.

## Amazon Simple Storage Service

The **Amazon Simple Storage Service** (S3) is used to store binary data objects for private or public use. The S3 implementation is fault-tolerant and assumes that hardware failures are a common occurrence.

There are multiple independent S3 locations: the United States Standard Region, Northern California Region,⁸ Europe, and Asia.

S3 automatically makes multiple copies of each object to achieve high availability, as well as for durability. These objects can range in size from one byte to five gigabytes. All objects reside in buckets, in which you can have as many objects as you like. Your S3 account can accommodate up to 100 buckets or named object containers. Bucket names are drawn from a global namespace, so you'll have to exercise some care and have a sound strategy for generating bucket names. When you store an object you provide a key that must be unique to the bucket. The combination of the S3 domain name, the globally unique bucket name, and the object key form a globally unique identifier. S3 objects can be accessed using an HTTP request, making S3 a perfect place to store static web pages, style sheets, JavaScript files, images, and media files. For example, here's an S3 URL to a picture of Maggie, my Golden Retriever: http://sitepoint-aws-cloud-book.s3.amazonaws.com/maggie.jpg.

The bucket name is **sitepoint-aws-cloud-book** and the unique key is **maggie.jpg**. The S3 domain name is s3.amazonaws.com.

Each S3 object has its own ACL. By default, each newly created S3 object is private. You can use the S3 API to make it accessible to everyone or specified users, and you can grant them read and/or write permission. I set Maggie's picture to be publicly readable so that you can see her.

Other AWS services use S3 as a storage system for AMIs, access logs, and temporary files.

Amazon S3 charges accrue based on the amount of data stored, the amount of data transferred in and out of S3, and the number of requests made to S3.

## Amazon CloudFront

Amazon **CloudFront** is a content distribution service designed to work in conjunction with Amazon S3. Because all Amazon S3 data is served from central locations in the US, Europe, and Asia, access from certain parts of the world can take several hundred milliseconds. CloudFront addresses this “speed of light” limitation with
