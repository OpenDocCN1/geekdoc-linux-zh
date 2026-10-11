
## SECURITY

MCS is designed to protect data confidentiality, thus allowing the domain-type part of the policy to be focused on protecting system integrity.

so this won’t be a problem.
After creating a file, it is possible to change the label to a different level with the `chcon -l` command. Below is an example of how to use it:

### Listing 1. Example of Using `semanage`

```bash
# semanage user -a -P user -R user_r -L s0:c1 -r s0:c1:SystemHigh rjc
# semanage user -l
```

| SELinux User | Labeling PREFIX | MLS/MCS Level | MLS/MCS Range | SELinux Roles |
| :--- | :--- | :--- | :--- | :--- |
| rjc | user | s0:c1 | s0:c1:SystemHigh | user_r |
| root | user | s0 | SystemLow:SystemHigh | system_r, sysadm_r |
| system_u | user | s0 | SystemLow:SystemHigh | system_r, user_r |
| user_u | user | s0 | SystemLow:SystemHigh | user_r, sysadm_r |

```bash
$ touch foo
$ ls -lZ foo
-rw-r--r-- rjc rjc rjc:object_r::t:tmp_t foo
$ chcon -l s0:c8 foo
$ ls -lZ foo
-rw-r--r-- rjc rjc rjc:object_r::t:tmp_t:ProjectA foo
```

Note that the level s0:c0 was translated to ProjectA; that is the translation I created previously.
It is possible to run a process with a different range.
The following is an example of the use of the `id -Z` command to display the SELinux context (including the MCS range at the end) as the user rjc uses the `runcon -l` command to run an instance of bash in a different range:

```bash
$ id -Z
rjc:system_r:unconfined_t:SystemLow:SystemHigh
```

```bash
$ runcon -l s0:c0:c10:c20 bash
$ id -Z
rjc:system_r:unconfined_t:s0:c0:c10:c20
$ runcon -l s0:c9:c20 bash
execvp: Permission denied
```

to support the needs of the MLS policy.
Fedora Core 5 uses the low end of the range for a process to specify the default context of files. The range parameter is specified by the `-r` switch. When using Fedora Core 5, often the only significant part of the range is the high end, which specifies the access. You should use the parameters `-P user -R user_r` when creating a user with the targeted policy (which is the default policy for a Fedora Core 5 install). The strict policy is much like the targeted policy in terms of MCS. Most of this article applies to the strict policy, although the `-P` and `-R` options to the `semanage` command will need different parameters.

After adding an identity, you must add a login entry to assign a UNIX account to an identity. The login configuration also allows you to specify the MCS range, because you may have many UNIX accounts with the same SELinux identity that have different MCS ranges assigned to them when they log in. You must use the `-s` parameter to specify the name of an SELinux identity that already exists. If you do not use the `-r` option to specify the range, it defaults to using no categories for the login entry in question (which may not be valid, depending on the low level of the range for the identity).

Below is an example of adding a login entry:

```bash
# semanage login -a -s rjc -r s0:c1:SystemHigh rjc
# semanage login -l
```

## Summary

| Login Name | SELinux User | MLS/MCS Range |
| :--- | :--- | :--- |
| __default__ | user_u | s0 |
| rjc | user_u | s0:c1:SystemHigh |
| root | root | SystemLow:SystemHigh |

MLS was implemented in a flexible manner via the policy language. This allowed us to develop the MCS policy afterward using the same language features and also permits the development of other category- and level-based confidentiality controls without changing kernel code. One example of this is my new development, Mandatory MCS (MMCS).

A Mandatory Access Control (MAC) system is a system where the access control is determined by the system administrator and enforced by the operating system. Users are not permitted to override this access control by granting excess access to their own data files. In UNIX permissions, it is possible to create a mode 777 file in the /tmp directory that grants full access to all users. With MMCS, I wanted to prevent such access being granted. In the MMCS policy, it is not permitted to write to a file with a level below the level of the process. This means that by setting the low levels for a user, the administrator can determine the minimum access needed to read files created by that user.

MCS and MLS policies have several significant differences. In MLS, the access is based on the low level of the range (the effective clearance) with the high level of the range used mostly to determine the access via the newrole program. In MCS, the access for both reading and writing is based on the high level of the range with the low level used only for restricting write access. Another difference is that MCS is designed to protect only the contents of files, while MLS restricts all methods of data transfer. Another major difference is that in MCS, a process may launch a child with a different range with minimal restrictions.

Note that the range for a login entry must be a subset of the range for an SELinux user identity. This means the low end of the login range must not be lower than the low end of the user identity range, and the high end of the login range must not be higher than the high end of the user identity range. In most cases, you will create a login entry with the same range as the user identity.

Russell Kaler has worked on Security-Enhanced Linux (SELinux) since 2001. He is an independent consultant specializing in SELinux and ISP administration.

## Polywell's Ultimate Linux Systems

More Choices, Better Service, Great Value

### Tower Systems

**4-way Opteron, OpenGL QFX**
**PolyStation 2055A-221O**
- 2x A8D Opteron Dual-Core 2210 Processors
- 2GB Dual Channel 667MHz DDR2 ECC
- NVIDIA Quadro FX 1300 OpenQ GL Graphics
- 2x SATA SATA Drives, SATA-RAID Controller
- Sony 16X DVD/DVD-ROM Loader, K6, Mouse
- 2x Gigabit LAN, 2 x PCIe 16x Slots
- Linux / BSD / Windows OS Supported
$1999 (custom config. available)

**4-way Opteron, SAS Drives**
**PolyStation 2055SS-2216**
- 2x A8D Opteron Dual-Core 2216 Processors
- 2GB Dual Channel 667MHz DDR2 ECC
- NVIDIA Quadro FX 1300 OpenQ GL Graphics
- 4x SAS SAS Drives, SATA-RAID Controller
- Sony 16X DVD/DVD-ROM Loader, K6, Mouse
- 2x Gigabit LAN, 2 x PCIe 16x Slots
- Linux / BSD / Windows OS Supported
$4679 (custom config. available)

**4-way Server, 32GB RAM**
**Tower Server 2500M-2220**
- 2x A8D Opteron Dual-Core 2220 Processors
- 32GB Dual Channel 667MHz DDR2 ECC
- 11 Bay Tower, w/ 2/7Gbit Power Supply
- 3/3x 150GB Serial ATA Drives, RAID 5
- Sony 16x DVD/DVD-ROM Loader, K6, Mouse
- 2x Gigabit LAN, 2 x PCIe 16x Slots
- Linux / BSD / Windows OS Supported
$9499 (custom config. available)

### Desktop Systems

**Low-Cost Linux Alliance PC**
**Poly 485Ax-280OSP**
- AMD Sempron 2800+ 64-bit Processor
- 256MB 667MHz DDR2 Memory
- ATI X300 PCIe Graphics
- 80GB SATA Drive, SATA-RAID Controller
- 1x 10/100/1000M LAN, K6, Mouse
- 100MHz LAN, 1 PCI + 1 PCIe 16x Slot
- Linux / BSD / Windows OS Supported
$299 (for volume purchase only)

**2TB Storage Alliance**
**MintBox 420AM2-3200OSP**
- AMD Athlon 64 3200+ 64-bit Processor
- 512MB Dual-Channel 667MHz DDR2 Memory
- NVIDIA GeForce 6150 Graphics
- 2TB 4500RPM SATA Drives, RAID5
- Optimal LAN 10/100 NIC, K6, Mouse
- Gigabit LAN, 2 PCI + 1 PCIe 16x Slots
- Linux / BSD / Windows OS Supported
$1239 (custom config. available)

**High-End PC, 4G DDR2**
**Poly 49X4MC-FX62**
- AMD Athlon 64 Dual-Core FX-62
- 4GB Dual-Channel 667MHz DDR2
- NVIDIA GeForce 7900GS Graphics
- 10K RPM 740GB 22200GB SATA Drives
- 14x 10/100/1000 NIC, K6, Mouse
- Gigabit LAN, 2 PCI + 1 PCIe 16x Slots
- Linux / BSD / Windows OS Supported
$2250 (custom config. available)

### Rack Servers

**Low-Cost ISP RackServer**
**1102EV-17 485Ax-3000OSP**
- 1102EV-17 10U, 19" 1U Rack
- 2xSB 667MHz DDR2 Memory
- ATI X300 PCIe Graphics
- 80GB SATA Drive, SATA-RAID Controller
- 117 1U Rack, 1U Slot, CD 2 - 3.5" Bays
- 100MHz LAN, 1 Optional PCI or PCI RISER
- Linux / BSD / Windows OS Supported
$399 (for volume purchase only)

**2GB RAM, 500GB ISP Server**
**1102EV-Ch 520AM2-4200**
- 1102EV-Ch 1U, 19" 1U Rack
- 2GB Dual-Channel 667MHz DDR2 Memory
- NVIDIA GeForce 6150 Graphics
- 500GB 2x250GB SATA Drives, RAID 5
- 117 1U Rack, 1U Slot, CD 2 - 3.5" Bays
- Gigabit LAN, 1 Optional PCI or PCI RISER
- Linux / BSD / Windows OS Supported
$950 (custom config. available)

**2GB ECC, 1TB ISP Server**
**1102EV-17 1000SL-1210**
- 1102EV-17 1U, 19" 1U Rack
- 2GB ECC, 2x 16x16GB DDR2 Memory
- 117 1U Rack, 1U Slot, CD 2 - 3.5" Bays
- 1TB 2x500GB SATA Drives, RAID 5
- 1U 1U Rack, 1U Slot, CD 2 - 3.5" Bays
- Optional PCI or PCI RISER
- Linux / BSD / Windows OS Supported
$1779 (custom config. available)

### High-Density Multi-Processor Servers

**16-way Opteron, 128GB RAM**
**5124XAS 8850S-8212**
- 16 x AMD Opteron 2105, 2112 Processors
- 128GB Dual Channel 667MHz DDR2 ECC
- 12TB 2x4500GB SATA Drives, RAID 5
- 4 x Gigabit Ethernet, 4 PCI, 2 PCIe Slots
- 24 1U Rack Redundant Power Supply
- Linux / BSD / Windows OS Supported
16-way 8212, 128GB RAM, 24x500GB $99999
8-way 8212, 32GB RAM, 8x500GB $59999

**18TB 4U Storage, 32GB RAM**
**4024AS 2500M-2210**
- 2 x AMD Opteron Dual-Core 2210 Processors
- 32GB Dual Channel 667MHz DDR2 ECC
- 18TB 2x4500GB SATA Drives, RAID 5
- 2 x Gigabit Ethernet, 4 PCI, 2 PCIe Slots
- 24 1U Rack Redundant Power Supply
- Linux / BSD / Windows OS Supported
18TB 2x4500G, 32G, 2x2210 $19999
1TB 2x500G, 32G, 1x2210 $9999

**6TB 2U Storage, 16GB RAM**
**2012AS 2500M-2210**
- 2 x AMD Opteron Dual-Core 2210 Processors
- 16GB Dual Channel 667MHz DDR2 ECC
- 6TB 12x500GB SATA Drives, RAID-5
- 2 x Gigabit Ethernet, 4 PCI, 2 PCIe Slots
- 2U 1U Rack, 2 x Redundant Power Supply
- Linux / BSD / Windows OS Supported
6TB 12x500G, 16G, 2x2210 $7999
1TB 6x500G, 16G, 1x2210 $3599

**2TB 1U Server, 32GB RAM**
**1104XS 2500M-2210**
- 2 x AMD Opteron Dual-Core 2210 Processors
- 32GB Dual Channel 667MHz DDR2 ECC
- 2TB 4x500GB SATA Drives, RAID-5
- 2 x Gigabit Ethernet, 4 PCI, 2 PCIe Slots
- 1U 1U Rack, 1U Slot, 2 x CD-RW 3.5" Bays
- Linux / BSD / Windows OS Supported
2TB 4x500G, 32G, 2x2210 $7888
1TB 2x500G, 32G, 2x2210 $7199

AMD Dual-Core technology enables one platform to meet the needs of multi-tasking and multi-threaded environments, provides platform longevity.

- 20 Years of Customer Satisfaction
- 5 Year Warranty, Industry's Longest
- First Class Customer Service

Polywell OEM Services. Your Virtual Manufacturer
Prototype Development with Linux/FreeBSD Support
Small Scale to Mass Production Manufacturing
Fulfillment, Shipping and RMA Repairs

888.765.9686
www.Polywell.com/us/LJ

Polywell Computers, Inc 1461 San Mateo Ave. South San Francisco, CA 94080
650.583.7222 Fax: 650.583.1974
