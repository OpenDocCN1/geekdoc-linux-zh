**Provisioning** When a virtual machine is created, you choose the amount of disk storage. However, it is a little more complicated than simply selecting the size. Virtual disks are provisioned either thinly or thickly.

**Thick provisioning** is a static setting where the virtual disk size is selected and the physical file(s) created on the physical disk is preallocated. Thus, if you select 700 GB as your virtual disk size, 700 GB of space is consumed on the physical drive. Some hypervisors (VMMs) have various versions of thick provisioning, such as lazy zero ticks, that have performance implications.

**Thin provisioning** is grown dynamically, which causes the hypervisor to consume only the amount of disk space actually used for the virtual drive. Thus, if you select 700 GB as your virtual disk size but only 300 GB of space is written to the virtual drive, then only 300 GB of space is consumed on the physical drive. As more data is written to the virtual drive, more space is utilized on the physical drive up to the 700 GB setting. Be aware that the reverse is not necessarily true—when you delete data from the virtual drive, it does not automatically free up disk space from the physical drive.

Thin provisioning is often done to allow overprovisioning. In this scenario, more disk space is assigned virtually than is available physically. The idea is that you can scale up the physical storage as needed. For example, if the host system is using LVM (covered in Chapter 11, “Handling Storage”), additional volumes are added as needed to the physical logical volume to meet virtual machine demand.

**Persistent Volumes** The term persistent volume is used by many virtualization products, such as OpenStack and Kubernetes. In essence, a virtualized persistent volume is similar to a physical disk in how it operates. Data is kept on the disk until the system or user overwrites it. The data stays on the disk, whether the virtual machine is running or not, and with some virtualization products, it can remain even after the virtual machine using it is destroyed.

**Blobs** Blob storage is a Microsoft Azure cloud platform term. Blob storage is large unstructured data, which is offered over the Internet and can be manipulated with .NET code. Typically, a blob consists of images, streaming video and audio, big data, and so on.

Blob data items are grouped together into a container for a particular user account and can be one of three different types:

+   • **Block blobs** are blocks of text and binary data. The blobs are not managed as a group but instead are handled independently of one another. Their size limit is 4.7 TB.
+   • **Append blobs** are also blocks of text and binary data. However, their storage is enhanced to allow for efficient appending operations. Thus, this blob type is often used for logging data.
+   • **Page blobs** are simply random access files, which can be up to 8 TB in size. They are also used as virtual disks for Azure virtual machines.