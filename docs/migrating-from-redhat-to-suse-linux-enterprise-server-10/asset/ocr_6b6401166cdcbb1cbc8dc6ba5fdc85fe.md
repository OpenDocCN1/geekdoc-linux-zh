Selecting the **Add** button opens the following dialog:

![](bbox=[0.09, 0.15, 0.21, 0.17])

![](bbox=[0.31, 0.14, 0.89, 0.49])

In this dialog you can define the name of the iSCSI device and the backend to use. To use more LUNs (Logical Unit Numbers) on one iSCSI target you have to edit the file /etc/ietd.conf manually.

The target name should be unique world wide. By default, the following syntax is used:

**iqn.YYYY-MM.reverse-domain-name: identifier**

**iqn** (iSCSI qualified name) is normally followed by the date of device creation and the domain name of the company in reverse order. The identifier is optional and can be used for a name based identification, like for example “iscsi-database-target”.

In the **path** box you define the backend device; in our case this would be /s/vliscsi/first-device.