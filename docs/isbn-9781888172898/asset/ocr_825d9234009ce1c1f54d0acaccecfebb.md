+   4. EB66 (NekoTech Mach 1)
+   5. EB66+
+   6. Jensen (DEC PC 150, 2000 model 300, Cullean)
+   7. Universal Desktop Box (UDB, sometimes called Multia). This is just a nomae board and is treated as such for the rest of this document.
+   8. AlphaStation 200, 250, 255, 400 (Avanti machines)
+   9. EB164 (Aspen Avalanche, Timberline, Summit; Microway Screamer)
+   10. Platform 2000 machines from Kinetics
+   11. PC164 machines (Durango)
+   12. Alcor type machines (AlphaStation 500, 600; Maverick, Brett)
+   13. Alpha-XL
+   14. Alpha-XLT (XL 300, XL 366)
+   15. Mikasa type machines (AlphaServer 1000), 1000A not supported

All of those platforrms excecpt the Jensen include an NCR 810 SCSI controller, though BusLogic PCI SCSI controllers (other than the FlashPoint), the Adaptec AHA2940 SCSI controller, and Qlogic 1020 ISP controllers are also supported. The Jensen design uses an AHA1740 SCSI controller and is supported.

NE2000, DE422, and DE4x5 (PCI) Ethernet cards are supported. This includes the UDB’s internal Ethernet hardware. Token ring support is also included in the kernels.

The X Window System should work on any machine with a S3 based video card except the Jensen machines. There is a server available from ftp://ftp.astrarnet.com for S3 cards in /pub/linux/axp/jensen. Most of the cards from Orchid and Number 9 will work. Most Diamond Stealth cards are also supported. Digital TGA cards (based on the DC21030 chip) are supported in 8 bit mode, and an X server for Mach64 cards is also provided.

More information on Alpha hardware is available in Appendix C.