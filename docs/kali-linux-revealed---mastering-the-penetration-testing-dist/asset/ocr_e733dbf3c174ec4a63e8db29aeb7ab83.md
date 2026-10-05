Systemd's journal also stores multiple logs (stdout/stderr output of daemons, syslog messages, kernel logs) and makes it easy to query them with journalctl. Without any arguments, it dumps all the available logs in a chronological way. With the -r option, it will reverse the order that newer messages are shown first. With the -f option, it will continuously print new log entries as they are appended to the database. The -u option can limit the messages to those emitted by a specific systemd unit (ex: journalctl -u ssh.service).

# 3.4.6. Discovering the Hardware

The kernel exports many details about hardware through the /proc/ and /sys/ virtual filesystems. Several tools summarize these details. Among them lspci (in the pciutils package) lists PCI devices, lusb (in the usbt package) lists USB devices, and lspcmia (in the pcmciutils package) lists PCMCIA cards. These tools are very useful for identifying the exact model of a device. identification also allows more precise searches on the web, which can lead to relevant documents. Note that the pciutils and usbt packages are already installed on the base Kali system but must be installed with apt install pciutils. We will discuss more about package installation and management in a later chapter.

> Example 3.1 Example of information provided by lspci and lusb

```
lspci
...
00:2.0 Display controller: Intel Corporation Mobile 915GM/GMS/910GML Express Graphics Controller (rev 03)
00:1.0 PCI bridge: Intel Corporation 82801FB/FBM/FR/FW (ICH6 Family) PCI Express Part 1 (rev 03)
00:1.0 USB Controller: Intel Corporation 82801FB/FBM/FR/FW (ICH6 Family) USB HCI #1 (rev 03)
01:0.0 Ethernet controller: Broadcom Corporation Nettreme BCM5751 Gigabit Ethernet PCI Express (rev 01)
02:0.0 Network controller: Intel Corporation PRO/Wireless 2208BG Network Connection (rev 05)
lsusb
Bus Bus 002 Device 004: Dell Corp.
Bus Bus 002 Device 008: ID 82c1:9001 Dell Corp.
Bus Bus 002 Device 007: ID 45de:00dd Microsoft Corp.
Bus Bus 002 Device 006: ID 046d:c0d3 Logitech, Inc.
Bus Bus 002 Device 004: ID 413c:0103 Dell Corp. Wireless 350 Bluetooth
```

These programs have a -v option that lists much more detailed (but usually unnecessary) information. Finally, the lsdev command (in the procinfo package) lists communication resources used by devices.

The lshw program is a combination of the above programs and displays a long description of the hardware discovered in a hierarchical manner. You should attach its full output to any report about support problems.