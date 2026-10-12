This driver allows you have a dummy network interface device, which you can use to fool a network client program. Keeping this as a module might be handy; hence, the default is recommended.

+   EQL (serial line load balancing) support [CONFIG_EQUALIZER] [N/y/m/?]

This feature is not useful for most server configurations. The default answer is recommended.

+   Ethernet (10 or 100Mbit) [CONFIG_NET_ETHERNET] [Y/n/?]

Yet another no-brainer.

Answers to the following questions depend on what types of network cards you have; respond accordingly:

+   3COM cards [CONFIG_NET_VENDOR_3COM] [N/y/?]
+   
+   AMD LANCE and Pcn (AT1550 and ME1200) support [CONFIG_LANCE] [N/y/m/?]
+   
+   Western digital/SMC cards [CONFIG_NET_VENDOR_SMC] [N/y/?]
+   
+   Racal-Interlan (Hicorn) NI cards [CONFIG_NET_VENDOR_RACAL] [N/y/?]
+   
+   Other ISA cards [CONFIG_NET_ISA] [N/y/?]
+   
+   EISA, VLB, PCI and on board controllers [CONFIG_NET_EISA] [Y/n/?]
+   
+   AMD Pctnet32 (VLB and PCI) support [CONFIG_PCTNET32] [N/y/m/?]
+   
+   Apricot Xen-II on board Ethernet [CONFIG_APRICOT] [N/y/m/?]
+   
+   CS89x0 support [CONFIG_CS89x0] [N/y/m/?]
+   
+   Generic DECChip & DIGITAL EtherWORKS PCI/EISA [CONFIG_DE4X5] [N/y/m/?]
+   
+   DEChip tulip (dc21x4x) PCI support [CONFIG_DEC_ELCEP] [N/y/m/?]
+   
+   Digi Intl. RightSwitch SR-X support [CONFIG_DECRE] [N/y/m/?]
+   
+   EtherExpressPro/100 support [CONFIG_EXPRESS_PRO100] [Y/n/m/?]
+   
+   PCI ME2000 support [CONFIG_MEZK_PCI] [N/y/m/?]
+   
+   Tl ThunderLAN support [CONFIG_TLAN] [N/y/m/?]
+   
+   VIA Rhine support [CONFIG_VIA_RHINE] [N/y/m/?]
+   
+   Pocket and portable adapters [CONFIG_NET_POCKET] [N/y/?]
+   
+   FDDI driver support [CONFIG_FDDI] [N/y/?]
+   
+   Frame relay DLCI support [CONFIG_DLCI] [N/y/m/?]
+   
+   PPP (point-to-point) support [CONFIG_PPP] [N/y/m/?]
+   
+   SLIP (serial line) support [CONFIG_SLIP] [N/y/m/?]
+   
+   Wireless LAN (non-hamradio) [CONFIG_NET_RADIO] [N/y/?]