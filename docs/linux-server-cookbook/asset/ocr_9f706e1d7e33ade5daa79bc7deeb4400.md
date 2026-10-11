```
[stack@undercloud ~]$ openstack --os-cloud development catalog show nova
| Field | Value |
| endpoints | regionOne | public: http://10.0.0.150:8774/v2.1 regionOne | internal: http://172.17.0.150:8774/v2.1 regionOne | admin: http://172.17.0.150:8774/v2.1 | id | a95e9fea9beb40ebbc3848992ecd080a | name | nova | type | compute |
```

![](bbox=[0.34, 0.33, 0.68, 0.36])

The clients access the cluster using the *public* endpoint, the services use the *internal* endpoint (located in the *internal API* network), and some administrative tasks are performed using the *admin* endpoint.

# Images

To run a *Virtual Machine*, it is required to use an *image* containing the operating system desired. The project to upload, manipulate or delete *images* is called **Glance**. The popular disk formats are as follows:

+   • **QCOW2 (QEMU copy-on-write version 2)**: is the main format used with the *KVM* hypervisor, the one used on **OpenStack**. The size is compressed, can be dynamically resized, and it is possible to run several *Virtual Machines* from a base image as well as only store the differences.
+   • **RAW**: This is an unstructured disk image; it contains the full size of the disk. This format is needed when *Ceph* is used as the backend for the storage.
+   • **VMDK (Virtual Machine Disk)**: This format is supported by many hypervisors, including *Vmware ESXi*.
+   • **VDI (Virtual Disk Image)**: Format supported by *VirtualBox* and *QEMU*.

Creating an *Image* requires specifying the disk format and the container format. When the image has no metadata, the container format is *bare*. *Figure 16.8* shows the creation of an image for *Debian 10*.