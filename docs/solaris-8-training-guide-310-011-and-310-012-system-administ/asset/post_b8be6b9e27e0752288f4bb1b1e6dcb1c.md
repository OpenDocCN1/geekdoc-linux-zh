
| Field | Description |
|---|---|
| `<profile>` | The name of the class file, a text file that defines how the Solaris software is installed on the system if a system matches the rule. The information in a class file consists of class file keywords and their corresponding class file values. All class files must reside in the JumpStart directory. Class files are described in the section “Creating Class Files.” |
| `<finish>` | The name of an optional Bourne shell script that can be executed after the installation completes. If no finish script exists, you must enter a minus sign (-) in this field. All finish scripts must reside in the JumpStart directory. See the section “Begin and Finish Scripts” for more information. |

The rules file must have the following:

- At least one rule
- The name “rules”
- At least a rule keyword, a rule value, and a corresponding profile
- A minus sign (-) in the begin and finish fields if there is no entry

The rules file should be saved in the JumpStart directory, should be owned by root, and should have permissions equal to 644.

The rules file allows the following:

- A comment after the pound sign (#) anywhere on a line. If a line begins with a #, the entire line is a comment. If a # is specified in the middle of a line, everything after the # is considered a comment.
- Blank lines.
- Rules to span multiple lines. You can let a rule wrap to a new line, or you can continue a rule on a new line by using a backslash (\ ) before Enter gets pressed.

Table 21.3 describes the various rule_keywords and rule_values that were introduced earlier.

## Table 21.3
### Rule Keyword and Rule Value Descriptions

| Rule Keyword | Rule Value | Description |
|---|---|---|
| any | Minus sign (-) | The match always succeeds. |
| arch | processor_type | The following table lists the valid values for processor_type: |
| Platform SPARC x86 | processor_type sparc i386 | Matches a system's processor type. The uname -p command reports the system's processor type. |
| domainname | domain_name | Matches a system's domain name, which controls how a name service determines information. If you have a system already installed, the domainname command reports the system's domain name. |
| disksize | <disk_name><size_range><disk_name> A disk name in the Form c?t?d?, such as c0t3d0, or the special word rootdisk. If rootdisk is used, the disk to be matched is determined in the following order: 1. The disk that contains the preinstalled boot image (a new SPARC-based system with factory JumpStart installed) 2. The c0t3d0s0 disk, if it exists. 3. The first available disk (searched in kernel probe order). 4. <size_range> The size of disk, which must be specified as a range of MB (xx-xx). | Matches a system's disk (in MB). Example: disksize c0t3d0 1000-2000. This example tries to match a system with a c0t3d0 disk that is between 1000 and 2000 MB. Note: When calculating size_range, remember that a megabyte equals 1,048,576 bytes. A disk might be advertised as a “535MB” disk, but it might have only 510 million bytes of disk space. The Solaris installation program views the “535MB” disk as a 510MB disk because 535,000,000 / 1,048,576 = 510. Therefore, a “535MB” disk would not match a size_range equal to 530 to 550MB. |
| hostaddress | <IP_address> | Matches a system's IP address. |
| hostname | <host_name> | Matches a system's host name. If you have a system already installed, the uname -n command reports the system's host name. |
| installed | <slice> <version><slice> A disk slice name in the form c?t?d?s?, such as c0t3d0s5, or the special words any or rootdisk. If any is used, all the system's disks will try to be matched (in kernel probe order). If rootdisk is used, the disk to be matched is determined in the following order: 1. The disk that contains the preinstalled boot image (a new SPARC- based system with factory JumpStart installed). 2. The c0t3d0s0 if it exists. 3. The first available disk (searched in kernel probe order). 4. <version> A version name, Solaris_2.x, or the special words any or upgrade. If any is used, any Solaris or SunOS release is matched. If upgrade is used, any upgradeable Solaris 2.1 or greater release is matched. | Matches a disk that has a root file system corresponding to a particular version of Solaris software. Example: installed c0t3d0s1 Solaris_2.7. This example tries to match a system that has a Solaris_2.7 root file system on c0t3d0s1. |
| karch | `<platform_group>` Valid values are sun4d, sun4c, sun4m, sun4u, i86pc, and prep. | Matches a system's platform group. If you have a system already installed, the `arch -k` command or the `uname -m` command reports the system's platform group. |
| memsize | `<physical_mem>` The value must be a range of MB (xx-xx) or a single MB value. | Matches a system's physical memory size (in MB). Example: `memsize 64-128` The example tries to match a system with a physical memory size between 64 and 128MB. If you have a system already installed, the output of the `prtconf` command (line 2) reports the system's physical memory size. |
| model | `<platform_name>` | Matches a system's platform name. Any valid platform name will work. To find the platform name of an installed system, use the `uname -i` command or the output of the `prtconf` command (line 5). Note: If the `<platform_name>` contains spaces, you must enclose it in single quotes (`'`). Example: `'SUNW,Ultra-5_10'` |
| network | `<network_num>` | Matches a system's network number, which the Solaris installation program determines by performing a logical AND between the system's IP address and the subnet mask. Example: `network 193.144.2.1`. This example tries to match a system with a 193.144.2.0 IP address (if the subnet mask were 255.255.255.0). |
| osname | `<Solaris_2.x>` | Matches a version of Solaris software already installed on a system. Example: `osname Solaris_2.7`. This example tries to match a system with Solaris 2.7 already installed. |
| totaldisk | `<size_range>` The value must be specified as a range of MB (xx-xx). | Matches the total disk space on a system (in MB). The total disk space includes all the operational disks attached to a system. Example: `totaldisk 1000-2000`. This example tries to match a system with a total disk space between 1G and 2GB. |

During a custom JumpStart installation, the Solaris installation program attempts to match the system being installed to the rules in the rules.ok file in order—the first rule through the last rule. A rule match occurs when the system being installed matches all the system attributes defined in the rule. As soon as a system matches a rule, the Solaris installation program stops reading the rules.ok file and begins installing the software based on the matched rule's class file.

Here are a few example rules:

```
karch sun4u  -  basic_prof  -
```

Specifies that the Solaris installation program should automatically install any system with the sun4u platform group based on the information in the basic_prof class file. There is no begin or finish script.

```
hostname pyramid2  -  ultra_class  -
```

The rule matches a system on the network called pyramid2. The class file to be used is named ultra_class. No begin or finish script is specified.

```
network 192.168.0.0 && ! model 'SUNW,Ultra-5_10' - \
net_class set_root_passwd
```

The third rule matches any system on the network that is not an Ultra 5 or Ultra 10. The class file to be used is named net_class, the finish script to be run is named set_root_passwd.

```
any - - generic_class -
```

The last example matches any system. The class file to be used is named generic_class and there is no begin or finish script.

## Validating the Rules File

Before the rules file can be used, you must run the check script to validate that this file is set up correctly. If all the rules are valid, the rules.ok file is created.

To validate the rules file, use the check script provided in the <install_dir_path>/Solaris_8/Misc/jumpstart_sample directory on the install server.

Change the directory to the JumpStart directory, and run the check script to validate the rules file:

```
<install_dir_path>/Solaris_8/Misc/jumpstart_sample/check \
[-p path] [-r file_name]
```

<install_dir_path> is the directory that was specified using the setup_install_server script when the install server was setup.

The check script options are described in Table 21.4.
