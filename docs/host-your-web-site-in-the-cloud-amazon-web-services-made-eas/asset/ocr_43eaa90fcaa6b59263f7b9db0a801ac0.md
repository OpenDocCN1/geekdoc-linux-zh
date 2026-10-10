# Elastic Block Store Volume

An **Elastic Block Store** (EBS) volume is an addressable disk volume. You (or your application, working on your behalf) can create a volume and attach it to any running instance in the same Availability Zone. The volume can then be formatted, mounted, and used as if it were a local disk drive. Volumes have a lifetime independent of any particular instance; you can have disk storage that persists even when none of your instances are running. Volumes are created using the CreateVolume function or the ec2-create-volume command, and then attached to a running instance using the AttachVolume function or the ec2-attach-volume command.

# Security Group

A **Security Group** defines the allowable set of inbound network connections for an instance. Each group is named and consists of a list of protocols, ports, and IP address ranges. A group can be applied to multiple instances, and a single instance can be regulated by multiple groups. Groups are created using the CreateSecurityGroup function and the ec2-add-group command. The AuthorizeSecurityGroupIngress function and the ec2-authorize command add new permissions to an existing security group.

# Access Control List

An **Access Control List** (ACL) specifies permissions for an object. An ACL is a list of identity/permission pairs. The GetObjectAccessControlPolicy function retrieves an object’s existing ACL and the SetObjectAccessControlPolicy function sets a new ACL on an object.

# AWS Infrastructure Web Services

Now that you know the key concepts, let’s look at each of the AWS infrastructure web services.

# Amazon Simple Storage Service

The **Amazon Simple Storage Service** (S3) is used to store binary data objects for private or public use. The S3 implementation is fault-tolerant and assumes that hardware failures are a common occurrence.