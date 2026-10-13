
Next, in the Actions tab, you should specify what action will occur when the indicator turns from one state to another; i.e., yellow to red. The default setting is that the action is executed when the indicator goes from yellow to red. Multiple actions can be configured for an alarm. You can, for example, run a script and also have an e-mail sent to you.

![](img/25fe75b93b97a021effaba85db112a52_346_0.png)

Figure 42.12: Actions for virtual machine alarms.

There are six different actions that you can configure for a virtual machine alarm. They are listed below as well as in Figure 42.12:

- Send a notification e-mail (SMTP)
- Send a notification trap (SNMP)
- Run a script
- Suspend the virtual machine
- Power off the virtual machine
- Reset the virtual machine

The first three actions listed for virtual machines are also available for the host alarms. These are also listed in Figure 42.13.

![](img/25fe75b93b97a021effaba85db112a52_346_1.png)

Figure 42.13: Actions for host alarms.

Sending an e-mail or a notification trap requires configuring the VirtualCenter Settings for SMTP and SNMP.

![](img/25fe75b93b97a021effaba85db112a52_347_0.png)

Figure 42.14: SNMP and SMTP settings for VirtualCenter alarms.

Open the Virtual Machine Settings window from the File menu. For SNMP, you can specify up to four hosts that can receive traps from your VirtualCenter environment. You must specify the IP address or hostname, the port, and the community string for each receiver.

For the SMTP settings, you must specify an identifier that will be used as the sender of the e-mail. For the delivery of the message, configure an SMTP host and port.

## Index

### A
- ACE ................ See VMware ACE
- Acronis True Image ................ 194
- Archiving virtual machines ............ 134
- Autorun, disable ...................... 163

### B
- Bridged networking ................... 141

### C
- CD-ROM
  - boot problem .................... 124
  - disable autorun ................. 163
  - working with .................... 122
- Clone
  - full ............................ 53
  - linked .......................... 53
  - virtual machines ................ 52
- Cloning
  - with VirtualCenter .............. 339
- Clustering
  - install Microsoft Cluster Services . 252
  - install Novell Cluster Services .... 244
  - prepare NetWare ................. 223
  - prepare Windows 2003 ............ 216
  - virtual machines ................ 213
- VMware ESX Server .................. 241
- VMware GSX Server .................. 232
- VMware Workstation ................ 226
- Command line
  - vmrun ........................... 96
  - vmware-fullscreen ............... 96
  - Workstation ....................... 95
- Console
  - remote for ESX Server ............ 327
  - virtual machine ................. 289

### D
- dd
  - command for imaging .............. 202
- Disk
  - split in 2 GB chunks ............. 41
  - types in VMware .................. 32
- Disk mode
  - non-persistent ................... 42
  - persistent ....................... 42

### G
- Generations ....................... 99
- Ghost
  - Peer to Peer imaging ............. 188
  - Ghost for Unix ................... 200
- GSX Server .... See VMware GSX Server
- Guest
  - install Linux .................... 61
  - install NetWare .................. 62
  - install Windows .................. 60
  - gui.restricted ................... 106

### H
- HAL.DLL
  - replacing ....................... 205
- Host only networking .............. 143

### I
- IDE to SCSI
  - imaging ......................... 207
- Imaging
  - file based ....................... 198
  - from IDE to SCSI ................. 207
  - Peer to Peer ..................... 193
  - Peer to Peer Linux commands ..... 203
  - with Linux commands .............. 200
- Import
  - virtual machines ................. 58
- Internet Connection Sharing ....... 160

### K
- kernel sources
  - Linux.................... 30
- options for VMware.................... 34
- routing................................... 149
- Token-Ring................................ 161
- wireless.................................. 160
- Non-persistent
  - disk mode................................ 42
- nvram.................................... 18, 98

### L
- Linux
  - graphical install problem ............ 168
  - kernel modules.......................... 30
  - kernel sources ......................... 167
  - VNC Installation....................... 169

### M
- MAC addresses ........................... 156
- Management Interface
  - GSX Server session length........... 304
- Memory
  - choose the right amount of........... 39
  - optimization.......................... 125
- Mounting
  - virtual disks......................... 117
- Movie
  - capture .............................. 57

### N
- NAT ... See Network Address Translation
- NetWare
  - network adapter ..................... 172
  - time synchronization................ 175
- Network Address Translation........... 145
- Network interface
  - general ............................. 141
- Network Interface
  - for NetWare ......................... 172
- Networking
  - bridged.............................. 141
  - host only ........................... 143
  - MAC addresses....................... 156

### O
- Operating System
  - Select correct....................... 38

### P
- Peer to Peer
  - imaging.............................. 193
- Performance
  - monitoring........................... 127
  - optimization......................... 131
- Persistent
  - disk mode ........................... 42
- Physical to Virtual conversion........ 183
- Port numbers
  - changing for GSX Server ............. 303
- Power on and off modes ............... 67
- Processors
  - assigning to virtual machines ....... 302

### R
- Restricting
  - Workstation ......................... 104
- Resume ................................ 43
- Routing in virtual machines .......... 149

### S
- Screenshot
  - of virtual machine................57
- SCSI adapters
  - changing the type of................122
- SCSI driver
  - for NetWare................176
  - for Windows................162
- SCSI to IDE
  - imaging................207
- Shared folders................138
- Shrinking
  - NetWare disks................173
  - virtual disks, general................133
  - Windows disks................163
- Snapshot
  - deleting................50
- Snapshots
  - introduction................45
  - using multiple................48
- Support
  - resources................94
- Suspend................43

### T
- Team
  - virtual machines................55
- Time synchronization................107
  - NetWare................175
- Tip of the day
  - customizing................102
- Token-Ring................161
- Tools................See VMware Tools
- True Image................See Acronis True Image

### U
- Upgrade
  - ESX Server................323
  - Workstation................25
- Upgrading
  - GSX Server................276
- User interface
  - restrictions................105
- UUID................158

### V
- Virtual disk
  - diskmount utility................117
- Virtual disk manager................114
- Virtual floppy................109
- Virtual machine
  - create in GSX Server................298
  - create in VirtualCenter................335
  - create in Workstation................36
  - performance monitoring................127
- Virtual machines
  - archiving................134
  - running from command line................95
- VirtualPC
  - import................58
- vmkd................18, 98
- vmrun
  - executable................96
- vmss................98
- VMware
  - choosing the right product................21
  - product generations................99
  - product overview................17
- Workstation................See Workstation
