# # 19.3 Method 1: broadcasts

Every node (machine) on a Microsoft Windows network has its own unique name. This is the name that you configure as the **Computer Name** in the **Control Panel > Network > Identification** window, or when you installed the Windows software on the PC in the first place. This name uses suffix <00> and – like any other name – must be explicitly *registered*.

# ## Name registration (name claim)

Registration is also called *name claim*, which is a much more explanatory term when used on a network that's using broadcasts. The machine broadcasts a *NAME REGISTRATION REQUEST* on its local wire, to the IP sub-net broadcast address, on port 137. All the other PCs on the same sub-net hear this request. Then:

+   * if one of them has already registered the name itself, it sends back a *NEGATIVE NAME REGISTRATION RESPONSE* to the PC that is trying to register this address and the registration fails. If the name in question is the PC's computer name, it will have to be reconfigured with a different name and rebooted
+   * if no other PC sends back a negative response, the requestor is free to have this name so it says to itself “I have succeeded, this name belongs to me.”

Below is the Ethereal trace of a PC booting (IP address 192.0.2.35, name ALICENT). After checking that no other machine is using its IP address, the PC issues four NB (NetBIOS) name claim (name registration) requests. These are sent to the sub-net broadcast address (192.0.2.127 here, because our netmask is 255.255.255.128). The total elapsed time was 5½ seconds (not shown). Because no other machine has replied to the name claim, the PC sets its name to ALICENT.

| Source | Destination | Protocol | Info |
|---|---|---|---|
| 00:50:da:e4:61:34 | ff:ff:ff:ff:ff:ff | ARP | Who has 192.0.2.35? Tell 192.0.2.35 |
| 00:50:da:e4:61:34 | ff:ff:ff:ff:ff:ff | ARP | Who has 192.0.2.35? Tell 192.0.2.35 |
| 00:50:da:e4:61:34 | ff:ff:ff:ff:ff:ff | ARP | Who has 192.0.2.35? Tell 192.0.2.35 |
| 192.0.2.35 | 192.0.2.127 | NBNS | Registration NB ALICENT <00> |
| 139.0.2.35 | 139.0.2.132 | NBNS | Registration NB ALICENT <00> |
| 192.0.2.35 | 192.0.2.127 | NBNS | Registration NB ALICENT <00> |
| 192.0.2.35 | 192.0.2.127 | NBNS | Registration NB ALICENT <00> |

The following trace shows the trace of a PC booting with a name (BOBNT) that's already in use on another PC (192.0.2.31). The existing PC responds that it's already using the name BOBNT, and the booting PC can't register (claim) the name for its own use.

| T | Source | Destination | Protocol | Info |
|---|---|---|---|---|
| 3.15 | 192.0.2.35 | 192.0.2.127 | NBNS | Registration NB BOBNT <00> |
| 3.15 | 192.0.2.31 | 192.0.2.35 | NBNS | Registration response NB 192.0.2.31 Registration NB BOBNT |
| 3.15 | 192.0.2.35 | 192.0.2.127 | NBNS | Registration NB BOBNT <00> |
| 3.15 | 192.0.2.31 | 192.0.2.35 | NBNS | Registration response NB 192.0.2.31 |

![](bbox=[0.2, 0.86, 0.77, 0.94])