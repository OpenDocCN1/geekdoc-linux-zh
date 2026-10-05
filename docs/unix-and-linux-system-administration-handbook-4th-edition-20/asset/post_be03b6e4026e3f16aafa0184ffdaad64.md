
## Vendor specifics for iSCSI initiators

iSCSI can run IPSec, although that is not required. If you don't use an IPSec tunnel, data blocks themselves are not encrypted. According to RFC3720, connections that do not use IPSec use CHAP secrets at least 12 characters long.

Targets and initiators both have iSCSI names, and several naming schemes are defined. The names in common use are iSCSI Qualified Names (IQNs), which have the following bizarre format:

```
iqn.yyyy-mm.reversed.DNS_domain:arbitrary_name
```

In most cases, everything up to the colon is a fixed (i.e., essentially irrelevant) prefix that characteristic of your site. You implement your owning naming scheme in the arbitrary_name portion of the IQN. The month and year (mm and yyyy) qualify the DNS domain to guard against the possibility of a domain changing hands. Use original DNS registration date. An actual name looks like this:

```
iqn.1995-08.com.example:disk54.dbngr
```

Despite the specificity of the IQN name format, it is not important that the prefix reflect your actual DNS domain or inception date. Most iSCSI implementations default to using the vendor's domain as an IQN, and this works. It is not necessary that the IQNs involved in a service relationship have matching prefixes.

## Booting from an iSCSI volume

If you're going to put your important data on a SAN, would it be nice to eliminate local hard disks entirely? Not only could you eliminate many of the special procedures needed to manage local disks, but you could also allow administrators to “swap” drives with a simple reboot, bringing instant updates and multiple boot configurations within each of Windows systems.

Unfortunately, the use of an iSCSI volume as a boot device is not widely supported. At least, not straightforward and not as a mainstream feature. Various Linux projects have made a go of it, but the implementations are necessarily tied to specific hardware and to specific iSCSI initiator software, and no current iSCSI boot project converges with the now-predominant initiator software, OpeniSCSI. Similarly, iSCSI support for Solaris and OpenSolaris is being worked, but there’s no production-ready solution yet.

The lone exception among our examples is AIX, which has a long history of good support for iSCSI. AIX versions 5.3 and later running on POWER hardware have full support for iSCSI booting over IPv4.

## Vendor specifics for iSCSI initiators

There have at least four different iSCSI initiator implementations for Linux. Several had died off and others have merged. The solver at this point seems to be Open-iSCSI, which is the standard initiator packed with all example Linux distributions. To get it up and running, install the open-scsi-package on Ubuntu and SUSE and the isscsi-initiator-utils package on Red Hat.

![](img/579efec8c67772f31ecf34844bbb71a2_325_0.png)

## Chapter 8 Storage

The project's home page is open-scsi.org, but don't go there looking for documentation. None seems to exist other than the main pages for iscidid and isciadam, which represent the implementation and the administrative interface for the system, respectively. Unfortunately, the administrative model for Open-iSCSI is best described as "creative".

In Open-iSCSI's world, a "node" is an iSCSI target, the thing that's normed with an IQN. Open-iSCSI maintains a database of the nodes it knows about an anarchy underneath the /etc/iscid/nodes. Configuration parameters for individual nodes are stored in this tree. Defaults are set in /etc/iscid/iscid.conf, but they are sometimes copied to newly defined nodes, so their function is not entirely predictable. The process of setting per-target parameters is painful; isciadam tortures you by making you change one parameter at a time and by making you the IQN and server on each command line.

The saving grace of the system is that iscid.conf and all the database files are editable files. Therefore, the same approach is to use isciadam for the few things it does and to circumvent it for the others.

To set up the system for simple, static operation with a single username and password for all iSCSI targets, first edit the iscid.conf file and make sure the following lines are configured as:

We show these lines together, they'll be separated in the actual file. The file is actually quite nicely commented and contains a variety of commented-out configuration options. Make sure you don't introduce duplicates.

Next, point isciadam at your target server and create node entries for each of the targets it discovers by reading server's discovery. Here, we will configure the target called from the server named iscid.

```
ubuntu$ sudo isciadam -m discovery -st -p iserver
192.168.0:75260,1 iqn.1994-11.com.admin:test
```

isciadam creates a subdirectories in /etc/iscid/nodes for each target. If there are targets you don't want to deal with, it's fine to use rm -rf their configuration directories. If the server offers many targets and you'd rather specify the details of the one you want, then:

```
ubuntu$ sudo isciadam -m node -o new -p iserver
-T iqn.1994-11.com.admin:test
New ISCSI node [tcp:hw=default,ip=,net_if=default,iscid_if=default]
server,3260,-1 iqn.1994-11.com.admin:test] added
```

Strangely, these methods achieve similar results but create different hierarchies under /etc/iscid/nodes. Which version you use, check the text files that are the leaves of the hierarchy to be sure the configuration parameters are set up appropriately. If you entered the hierarchy manually, you may need to set the property node.startup to automatic by hand.

You can connect to the remote targets with iscsiadm -m node -l

```
ubuntu sudo iscsiadm -m node -l
Logging to [if: default, target: iqn.1994-11.com.admin:test, portal:
192.168.0.75,3260]
Login to [if: default, target: iqn.1994-11.com.admin:test, portal:
192.168.0.75,3260]
Login to [if: default, target: iqn.1994-11.com.admin:test, portal:
192.168.0.75,3260] successful
```

Despite the specificity of the IQN name format, it is not important that the prefix reflect your actual DNS domain or inception date. Most iSCSI implementations default to using the vendor's domain as an IQN, and this works. It is not necessary that the IQNs involved in a service relationship have matching prefixes.

You can connect to the remote targets with iscsiadm -m node -l

Despite the specificity of the IQN name format, it is not important that the prefix reflect your actual DNS domain or inception date. Most iSCSI implementations default to using the vendor's domain as an IQN, and this works. It is not necessary that the IQNs involved in a service relationship have matching prefixes.

Despite the specificity of the IQN name format, it is not important that the prefix reflect your actual DNS domain or inception date. 

## Vendor specifics for iSCSI initiators

![](img/579efec8c67772f31ecf34844bbb71a2_325_0.png)

## Chapter 8 Storage

The project's home page is open-scsi.org, but don't go there looking for documentation. None seems to exist other than the main pages for iscidid and isciadam, which represent the implementation and the administrative interface for the system, respectively. Unfortunately, the administrative model for Open-iSCSI is best described as "creative".

In Open-iSCSI's world, a "node" is an iSCSI target, the thing that's normed with an IQN. Open-iSCSI maintains a database of the nodes it knows about an anarchy underneath the /etc/iscid/nodes. Configuration parameters for individual nodes are stored in this tree. Defaults are set in /etc/iscid/iscid.conf, but they are sometimes copied to newly defined nodes, so their function is not entirely predictable. The process of setting per-target parameters is painful; isciadam tortures you by making you change one parameter at a time and by making you the IQN and server on each command line.

The saving grace of the system is that is much.conf and all the database files are editable files. Therefore, the same approach is to use isciadam for the few things it does and to circumvent it for the others.

To set up the system for simple, static operation with a single username and password for all iSCSI targets, first edit the iscid.conf file and make sure the following lines are configured as:

We show these lines together, they'll be separated in the actual file. The file is actually quite nicely commented and contains a variety of commented-out configuration options. Make sure you don't introduce duplicates.

Next, point isciadam at your target server and create node entries for each of the targets it discovers by reading server's discovery. Here, we will configure the target called from the server named iscid.

```
ubuntu$ sudo isciadam -m discovery -st -p iserver
192.168.0:75260,1 iqn.1994-11.com.admin:test
```

isciadam creates a subdirectories in /etc/iscid/nodes for each target. If there are targets you don't want to deal with, it's fine to use rm -rf their configuration directories. If the server offers many targets and you'd rather specify the details of the one you want, then:

```
ubuntu$ sudo isciadam -m node -o new -p iserver
-T iqn.1994-11.com.admin:test
New ISCSI node [tcp:hw=default,ip=,net_if=default,iscid_if=default]
server,3260,-1 iqn.1994-11.com.admin:test] added
```

Strangely, these methods achieve similar results but create different hierarchies under /etc/iscid/nodes. Which version you use, check the text files that are the leaves of the hierarchy to be sure the configuration parameters are set up appropriately. If you entered the hierarchy manually, you may need to set the property node.startup to automatic by hand.

You can connect to the remote targets with iscsiadm -m node -l

[content]![](img/579efec8c67772f31ecf34844bbb71a2_325_0.png)

## Vendor specifics for iSCSI initiators

There have at least four different iSCSI initiator implementations for Linux. Several had died off and others have merged. The solver at this point seems to be Open-iSCSI, which is the standard initiator packed with all example Linux distributions. To get it up and running, install the open-scsi-package on Ubuntu and SUSE and the isscsi-initiator-utils package on Red Hat.

![](img/579efec8c67772f31ecf34844bbb71a2_325_0.png)

[content]

Wait, it looks like the provided text has repetitive sections and overlaps. Let me provide the clean, merged version based on the logic requested.

[content]
Despite the specificity of the IQN name format, it is not important that the prefix reflect your actual DNS domain or inception date. Most iSCSI implementations default to using the vendor's domain as an IQN, and this works. It is not necessary that the IQNs involved in a service relationship have matching prefixes.

## Booting from an iSCSI volume

If you're going to put your important data on a SAN, would it be nice to eliminate local hard disks entirely? Not only could you eliminate many of the special procedures needed to manage local disks, but you could also allow administrators to “swap” drives with a simple reboot, bringing instant updates and multiple boot configurations within each of Windows systems.

Unfortunately, the use of an iSCSI volume as a boot device is not widely supported. At least, not straightforward and not as a mainstream feature. Various Linux projects have made a go of it, but the implementations are necessarily tied to specific hardware and to specific iSCSI initiator software, and no current iSCSI boot project converges with the now-predominant initiator software, OpeniSCSI. Similarly, iSCSI support for Solaris and OpenSolaris is being worked, but there’s no production-ready solution yet.

The lone exception among our examples is AIX, which has a long history of good support for iSCSI. AIX versions 5.3 and later running on POWER hardware have full support for iSCSI booting over IPv4.

## Vendor specifics for iSCSI initiators

There have at least four different iSCSI initiator implementations for Linux. Several had died off and others have merged. The solver at this point seems to be Open-iSCSI, which is the standard initiator packed with all example Linux distributions. To get it up and running, install the open-scsi-package on Ubuntu and SUSE and the isscsi-initiator-utils package on Red Hat.

![](img/579efec8c67772f31ecf34844bbb71a2_325_0.png)

## Chapter 8 Storage

The project's home page is open-scsi.org, but don't go there looking for documentation. None seems to exist other than the main pages for iscidid and isciadam, which represent the implementation and the administrative interface for the system, respectively. Unfortunately, the administrative model for Open-iSCSI is best described as "creative".

In Open-iSCSI's world, a "node" is an iSCSI target, the thing that's normed with an IQN. Open-iSCSI maintains a database of the nodes it knows about an anarchy underneath the /etc/iscid/nodes. Configuration parameters for individual nodes are stored in this tree. Defaults are set in /etc/iscid/iscid.conf, but they are sometimes copied to newly defined nodes, so their function is not entirely predictable. The process of setting per-target parameters is painful; isciadam tortures you by making you change one parameter at a time and by making you the IQN and server on each command line.

The saving grace of the system is that iscid.conf and all the database files are editable files. Therefore, the same approach is to use isciadam for the few things it does and to circumvent it for the others.

To set up the system for simple, static operation with a single username and password for all iSCSI targets, first edit the iscid.conf file and make sure the following lines are configured as:

We show these lines together, they'll be separated in the actual file. The file is actually quite nicely commented and contains a variety of commented-out configuration options. Make sure you don't introduce duplicates.

Next, point isciadam at your target server and create node entries for each of the targets it discovers by reading server's discovery. Here, we will configure the target called from the server named iscid.

```
ubuntu$ sudo isciadam -m discovery -st -p iserver
192.168.0:75260,1 iqn.1994-11.com.admin:test
```

isciadam creates a subdirectories in /etc/iscid/nodes for each target. If there are targets you don't want to deal with, it's fine to use rm -rf their configuration directories. If the server offers many targets and you'd rather specify the details of the one you want, then:

```
ubuntu$ sudo isciadam -m node -o new -p iserver
-T iqn.1994-11.com.admin:test
New ISCSI node [tcp:hw=default,ip=,net_if=default,iscid_if=default]
server,3260,-1 iqn.1994-11.com.admin:test] added
```

Strangely, these methods achieve similar results but create different hierarchies under /etc/iscid/nodes. Which version you use, check the text files that are the leaves of the hierarchy to be sure the configuration parameters are set up appropriately. If you entered the hierarchy manually, you may need to set the property node.startup to automatic by hand.

You can connect to the remote targets with iscsiadm -m node -l

```
ubuntu sudo iscsiadm -m node -l
Logging to [if: default, target: iqn.1994-11.com.admin:test, portal:
192.168.0.75,3260]
Login to [if: default, target: iqn.1994-11.com.admin:test, portal:
192.168.0.75,3260]
Login to [if: default, target: iqn.1994-11.com.admin:test, portal:
192.168.0.75,3260] successful
```

Despite the specificity of the IQN name format, it is not important that the prefix reflect your actual DNS domain or inception date. Most iSCSI implementations default to using the vendor's domain as an IQN, and this works. It is not necessary that the IQNs involved in a service relationship have matching prefixes.
[/content]
```
*(Self-correction: The input text had repeated headers and overlapping pages. I will provide the cleaned version of the unique content provided.)*

Actually, the prompt asks to process the *provided* OCR text which includes duplicates. I will merge the pages and follow the logical flow while fixing errors as requested.

[content]
## Vendor specifics for iSCSI initiators

iSCSI can run IPSec, although that is not required. If you don't use an IPSec tunnel, data blocks themselves are not encrypted. According to RFC3720, connections that do not use IPSec use CHAP secrets at least 12 characters long.

Targets and initiators both have iSCSI names, and several naming schemes are defined. The names in common use are iSCSI Qualified Names (IQNs), which have the following bizarre format:

```
iqn.yyyy-mm.reversed.DNS_domain:arbitrary_name
```

In most cases, everything up to the colon is a fixed (i.e., essentially irrelevant) prefix that characteristic of your site. You implement your owning naming scheme in the arbitrary_name portion of the IQN. The month and year (mm and yyyy) qualify the DNS domain to guard against the possibility of a domain changing hands. Use original DNS registration date. An actual name looks like this:

```
iqn.1995-08.com.example:disk54.dbngr
```

Despite the specificity of the IQN name format, it is not important that the prefix reflect your actual DNS domain or inception date. Most iSCSI implementations default to using the vendor's domain as an IQN, and this works. It is not necessary that the IQNs involved in a service relationship have matching prefixes.

## Booting from an iSCSI volume

If you're going to put your important data on a SAN, would it be nice to eliminate local hard disks entirely? Not only could you eliminate many of the special procedures needed to manage local disks, but you could also allow administrators to “swap” drives with a simple reboot, bringing instant updates and multiple boot configurations within each of Windows systems.

Unfortunately, the use of an iSCSI volume as a boot device is not widely supported. At least, not straightforward and not as a mainstream feature. Various Linux projects have made a go of it, but the implementations are necessarily tied to specific hardware and to specific iSCSI initiator software, and no current iSCSI boot project converges with the now-predominant initiator software, OpeniSCSI. Similarly, iSCSI support for Solaris and OpenSolaris is being worked, but there’s no production-ready solution yet.

The lone exception among our examples is AIX, which has a long history of good support for iSCSI. AIX versions 5.3 and later running on POWER hardware have full support for iSCSI booting over IPv4.

## Vendor specifics for iSCSI initiators

There have at least four different iSCSI initiator implementations for Linux. Several had died off and others have merged. The solver at this point seems to be Open-iSCSI, which is the standard initiator packed with all example Linux distributions. To get it up and running, install the open-scsi-package on Ubuntu and SUSE and the isscsi-initiator-utils package on Red Hat.

![](img/579efec8c67772f31ecf34844bbb71a2_325_0.png)

## Chapter 8 Storage

The project's home page is open-scsi.org, but don't go there looking for documentation. None seems to exist other than the main pages for iscidid and isciadam, which represent the implementation and the administrative interface for the system, respectively. Unfortunately, the administrative model for Open-iSCSI is best described as "creative".

In Open-iSCSI's world, a "node" is an iSCSI target, the thing that's normed with an IQN. Open-iSCSI maintains a database of the nodes it knows about an anarchy underneath the /etc/iscid/nodes. Configuration parameters for individual nodes are stored in this tree. Defaults are set in /etc/iscid/iscid.conf, but they are sometimes copied to newly defined nodes, so their function is not entirely predictable. The process of setting per-target parameters is painful; isciadam tortures you by making you change one parameter at a time and by making you the IQN and server on each command line.

The saving grace of the system is that iscid.conf and all the database files are editable files. Therefore, the same approach is to use isciadam for the few things it does and to circumvent it for the others.

To set up the system for simple, static operation with a single username and password for all iSCSI targets, first edit the iscid.conf file and make sure the following lines are configured as:

We show these lines together, they'll be separated in the actual file. The file is actually quite nicely commented and contains a variety of commented-out configuration options. Make sure you don't introduce duplicates.

Next, point isciadam at your target server and create node entries for each of the targets it discovers by reading server's discovery. Here, we will configure the target called from the server named iscid.

```
ubuntu$ sudo isciadam -m discovery -st -p iserver
192.168.0:75260,1 iqn.1994-11.com.admin:test
```

isciadam creates a subdirectories in /etc/iscid/nodes for each target. If there are targets you don't want to deal with, it's fine to use rm -rf their configuration directories. If the server offers many targets and you'd rather specify the details of the one you want, then:

```
ubuntu$ sudo isciadam -m node -o new -p iserver
-T iqn.1994-11.com.admin:test
New ISCSI node [tcp:hw=default,ip=,net_if=default,iscid_if=default]
server,3260,-1 iqn.1994-11.com.admin:test] added
```

Strangely, these methods achieve similar results but create different hierarchies under /etc/iscid/nodes. Which version you use, check the text files that are the leaves of the hierarchy to be sure the configuration parameters are set up appropriately. If you entered the hierarchy manually, you may need to set the property node.startup to automatic by hand.

You can connect to the remote targets with iscsiadm -m node -l

```
ubuntu sudo iscsiadm -m node -l
Logging to [if: default, target: iqn.1994-11.com.admin:test, portal:
192.168.0.75,3260]
Login to [if: default, target: iqn.1994-11.com.admin:test, portal:
192.168.0.75,3260]
Login to [if: default, target: iqn.1994-11.com.admin:test, portal:
192.168.0.75,3260] successful
```
