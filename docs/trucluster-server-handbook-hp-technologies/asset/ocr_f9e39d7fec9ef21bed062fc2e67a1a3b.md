# Network Resource Attributes

| Required? | Attribute | Description |
|---|---|---|
| ✓ | SUBNET = xxx.xxx.xxx.xxx | The xxx.xxx.xxx.xxx is the network subnet. The network subnet is the bitwise AND of the IP address and the netmask.
IP Address = 18. 32. 64. 121
& netmask = 255. 255. 255. 0
subnet = 18. 32. 64. 0 |

Table 23-7: CAA Network Resource Attribute

# Tape/Media Changer Resource Attributes

| Required? | Attribute | Description |
|---|---|---|
| ✓ | DEVICE_NAME = device-name | The device-name is the tape or media changer device-special file name. You can specify either the full path or only the device-special file name.
/dev/tape/tape0 | tape0
/dev/changer/mc0 | mc0 |

Table 23-8: CAA Tape and Media Changer Resource Attribute

# 23.4.4.3 Network Resource Attributes

Table 23-7 lists the one attribute that is specific to the Network resource type.

# 23.4.4.4 Tape and Media Changer Resource Attribute

Table 23-8 lists the one attribute that is specific to both the Tape and Media Changer resources.

# 23.4.5 Type Definition File

Starting with TruCluster Server version 5.1A-IPK the TYPE_*.cap files in the /var/cluster/caa/template directory have been replaced with a new file format, the type definition file (*.tdf). This change was made primarily to facilitate ease of customization in adding user-defined attributes to application resources.