
## ftp

**Purpose**: Transfer files using FTP (File Transfer Protocol).

**Usage syntax:** `ftp [OPTIONS] [HOST]`

```
# ftp 10.10.1.48

Connected to 10.10.1.48.
Name (10.10.1.45): nick
Password: ********
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_163_0.png)

The **ftp** command transfers files using the FTP protocol. The above example demonstrates using the **ftp** command to connect to a remote FTP server. Once connected to the remote system, you can execute one of the FTP shell commands listed in the following table.

**FTP commands**

| **Command** | **Function** |
| :--- | :--- |
| **ascii** | Transfer files in ASCII format |
| **binary** | Transfer files in binary format |
| **status** | Display the connection status |
| **pwd** | Print the current working directory |
| **ls** | List remote directory contents |
| **get [FILE]** | Download the specified remote file |
| **put [FILE]** | Upload the specified local file |
| **cd [PATH]** | Change directories on the remote system |
| **lcd [PATH]** | Change directories on the local system |
| **mkdir [DIR]** | Create a directory |
| **rmdir [DIR]** | Remove a directory |
| **delete [FILE]** | Remove a file |
| **rename [FILE]** | Rename a file |
| **bye** | Terminate the FTP connection |

**Common usage examples:**

| **Example** | **Description** |
| :--- | :--- |
| `ftp [HOST]` | Start an FTP session with the specified host |
| `ftp -p [HOST]` | Use passive mode for data transfers |

## wget

**Purpose:** File download utility for Linux systems.

**Usage syntax:** `wget [OPTIONS] [SOURCE]`

![](img/fa2f95b64a707c963dfa0445bd9281a7_164_0.png)

wget is a file download utility for the command line. It can be used to download files via HTTP and FTP protocols. In the above example, a file is downloaded from a remote HTTP system and saved in the current directory.

> *Use the --user=[USERNAME] and --password=[PASSWORD] options to specify a username and password to used when connecting to the remote system.*

**Common usage examples:**

- `wget http://[HOST/FILE]`
  - Download the specified file via HTTP
- `wget ftp://[HOST/FILE]`
  - Download the specified file via FTP

## showmount

**Purpose:** Display NFS mount and export information.

**Usage syntax:** `showmount [OPTIONS]`

```
# showmount
Hosts on noc-01:
10.10.1.48
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_165_0.png)

The **showmount** command displays information about an NFS server running on the local system. The above example demonstrates using **showmount** to display a list of clients currently connected to the NFS server.

The next example demonstrates using the **-e** option to display the NFS server's export list.

```
# showmount -e
Export list for noc-01:
/home 10.10.1.0/255.255.255.0
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_165_1.png)

The **-d** option is used to display a list of exported directories that are currently in use, as shown in the next example.

```
# showmount -d
Directories on noc-01:
/home
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_165_2.png)

**Common usage examples:**

| **Command** | **Description** |
| :--- | :--- |
| `showmount` | Display NFS clients currently connected to the server |
| `showmount -e` | Display the NFS server's exported directories |
| `showmount -d` | List exported directories that are currently in use |
| `showmount -a` | Display NFS clients and the directories they have mounted |

## Section 9: Hardware Management Commands

**Overview**

Commands in this section cover basic Unix, Linux, and BSD hardware management utilities. These commands can be used to identify, configure, and troubleshoot system devices.

**Commands covered in this section:**

| **Command** | **Purpose** |
| :--- | :--- |
| lshw | List hardware on Linux systems. |
| ioscan | List hardware on HP-UX systems. |
| lsdev | List hardware on AIX systems. |
| lspci | List PCI devices on Linux systems. |
| pciconf | List PCI devices on BSD systems. |
| lsusb | List USB devices on Linux systems. |
| dmidecode | Display detailed information about devices on the system. |
| hdparm | Display/set hard drive parameters on Linux systems. |
| eject | Unload removable media. |

**Glossary of terms used in this section:**

- **IDE** | (Integrated Drive Electronics) Legacy interface used to link disk drives to a computer.
- **PCI** | (Peripheral Component Interconnect) Interface used to connect internal devices to a computer.
- **SATA** | (Serial Advanced Technology Attachment) Modern interface used to link disk drives to a computer.
- **USB** | (Universal Serial Bus) Interface used to connect external devices to a computer.

## lshw

**Purpose**: List hardware on Linux systems.

**Usage syntax:** `lshw [OPTIONS]`

```
# lshw -short
H/W path  Device    Class      Description
==========================================
        /     system     OptiPlex GX520
        /0   bus        0WG233
        /0/0   memory   64KiB BIOS
        /0/00    processor Intel(R) Pentium(R) 4 CPU 3.00GHz
        /0/000/700    memory    16KiB L1 cache
        /0/000/701    memory    2MiB L2 cache
        /0/000/0.1    processor  Logical CPU
        /0/000/0.2    processor  Logical CPU
        /0/1000   memory    2GiB System Memory
        /0/1000/0   memory  1GiB DIMM DDR Synchronous 533 MHz
        ...
```
Output of the lshw command using the -short option

```
# lshw
nc@-01
        description: Mini Tower Computer
        product: OptiPlex GX520
        vendor: Dell Inc.
        serial: ******
        width: 32 bits
        capabilities: smbios-2.3 dmi-2.3 smp-1.4 smp
        configuration: administrator_password=enabled boot=normal
        chassis=mini-tower cpus=1
*->core
        description: Motherboard
        product: 0WG233
        vendor: Dell Inc.
        ...
```
Default output of the lshw command

**Common usage examples:**

- `lshw`
  - Display a detailed hardware listing
- `lshw -short`
  - Display a simple hardware listing

## ioscan

**Purpose:** List hardware on HP-UX systems.

**Usage syntax:** `ioscan [OPTIONS]`

```
# ioscan
H/W Path  Class         Description
=======    ===         ==========
      0
            bc           I/O Adapter
8/0        ext_bus      GSC add-on Fast/Wide SCSI Interface
8/0.5      target
8/0.5.0    disk         SEAGATE  ST34371W
8/0.7      target
8/0.7.0    cti          Initiator
8/0.8      target
8/0.8.0    disk         SEAGATE  ST318436LC
8/4        ba           PCI Bus Bridge - GSCtoPCI
8/4/1/0    lan          HP  J3515A  HSC 10/100Base-TX D-Class
1 port     Core I/O Adapter
8/16       ba           Initiator
8/16/0     ext_bus      Built-in Parallel Interface
8/16/4     tty          Built-in RS-232C
8/16/5     ext_bus      Built-in SCSI
8/16/5.0   target
8/16/5.0.0 tape         HP  C1537A
8/16/5.2   target
8/16/5.2.0 disk         SONY   CD-ROM CDU-76S
8/16/5.7   target
8/16/5.7.0 cti          Initiator
8/16/6     lan          Built-in LAN
8/16/7     ps2          Built-in Keyboard/Mouse
8/20       ba           Core I/O Adapter
8/20/2     tty          Built-in RS-232C
...
```
Listing devices with ioscan on HP-UX

**ioscan** displays information about hardware installed on HP-UX systems. The above example displays the typical output of this command which shows information about the system’s hardware profile.

**Common usage examples:**

- `ioscan`
  - Display a simple hardware listing
- `ioscan -f`
  - Display a detailed hardware listing

## lsdev

**Purpose:** List hardware on AIX systems.

**Usage syntax:** `lsdev [OPTIONS]`

```
# lsdev
L2cache0      Available     L2 Cache
cd0           Available     L5-00       IDE DVD-ROM Drive
en0           Available     1L-08       Standard Ethernet Network Interface
en1           Defined       1J-08       Standard Ethernet Network Interface
ent0          Available     1L-08       10/100 Mpbs Ethernet PCI Adapter II
ent1          Available     1L-08       10/100/1000 Base-TX PCI-X Adapter
et0           Defined       1L-08       IEEE 802.3 Ethernet Network Interface
et1           Defined       1J-08       IEEE 802.3 Ethernet Network Interface
fd0           Available     01-D1-00-00 Diskette Drive
fda0          Available     01-D1       Standard I/O Diskette Adapter
hd1           Defined                   Logical volume
hd2           Defined                   Logical volume
hd3           Defined                   Logical volume
hd4           Defined                   Logical volume
hd5           Defined                   Logical volume
hd6           Defined                   Logical volume
hd8           Defined                   Logical volume
hd10opt       Defined                   Logical volume
hd11admin     Defined                   Logical volume
hd9var        Defined                   Logical volume
hdisk0        Available     1S-08-00-5,0 16 Bit LVD SCSI Disk Drive
hdisk1        Defined       1S-08-00-8,0 Other SCSI Disk Drive
hdisk2        Available     1S-08-00-8,0 16 Bit LVD SCSI Disk Drive
ide0          Available     L5-19       ATA/IDE Controller Device
...
```
Listing devices on AIX with lsdev

**lsdev** displays information about hardware installed on AIX systems. The above example displays the typical output of this command which includes information about hardware installed on the local system.

**Common usage examples:**

- `lsdev`
  - Display a simple hardware listing
