**AMI:**
Any AMI FastDisk disk controller that is a true BusLogic MultiMaster clone

**BusLogic:**
MultiMaster \"W\" series host adapters, including BT-948, BT-958, and BT-9580
MultiMaster \"C\" series host adapters, including BT-946C, BT-956C, BT-956CD, BT-445C, BT-747C, BT-757C, BT-757CD, BT-545C, and BT-540CF
MultiMaster \"S\" series host adapters, including BT-445S, BT-747S, BT-747D, BT-757S, BT-757D, BT-545S, BT-542D, BT-742A, and BT-542B
MultiMaster \"A\" series host adapters, including BT-742A and BT-542B

**Compaq:**
Intelligent disk array controllers: IDA, IDA-2, 1AES, SMART, SMART-2/E, Smart-2/IP, SMART-2SL; Integrated Array; and Smart Arrays 3200, 3100ES, 221, 4200, 4200, and 4250ES

**DPT:**
SmartCACHE Plus, SmartCACHE III, SmartRAID III, SmartCACHE IV, and SmartRAID IV SCSI/RAID are supported. The DPT SmartRAID/CACHE V is not yet supported. The DPT PM3754U2-16M SCSI RAID controller is also supported.

**DTC:**
EISA SCSI controller in 1542 evaluation mode

**SymBios (also NCR):**
53C810, 53C810a, 53C815, 53C820, 53C825a, 53C860, 53C875, 53C875j, 53C885, and 53C896 PCI SCSI controllers, including ASUS SC-200; Data Technology DTC3130 (all variants); Diamond FirePort (all); NCR cards (all); SymBios cards (all); Tekram DC390W, 390U, and 390F; and Tyan S1365

**QLLogic:**
1020, 1040, 1040B, and 2100 SCSI and fiber

> NOTE
> FreeBSD supports SCSI-I and SCSI-II devices. However, CD-RW and WORM devices are supported only in read-only mode by the driver included with FreeBSD. To get write access to these devices, install cdrerecord from the FreeBSD ports tree.