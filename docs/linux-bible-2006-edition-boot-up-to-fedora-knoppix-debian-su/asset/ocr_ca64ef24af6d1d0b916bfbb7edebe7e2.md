# Chapter 26 ✦ Running a Printer Server 703

3. When prompted, fill in the username and password needed to access the SMB printer. (You may also fill in the Workgroup information, if required.) Click OK to continue.

Alternatively, you can identify a server that does not appear on the list of servers. Click the Specify button and enter the following information in the appropriate fields:

+   ♦ Workgroup—The workgroup name assigned to the SMB server. Filling in the workgroup name is not necessary in all cases.

+   ♦ Server—NetBIOS name or IP for the computer, which may or not be the same as its TCP/IP name. To translate this into the address needed to reach the SMB host, Samba checks several places where the name may be assigned to an IP address. Samba checks the (in the order shown) until it finds a match: the local /etc/hosts file, the local /etc/hosts, a WINS server on the network, and responses to broadcasts on each local network to resolve the name.

+   ♦ Share—The name under which the printer is shared with the remote computer. It may be different from the name which local users of the SMB printer know the printer.

+   ♦ User—Username is required by the SMB system to give you access to the SMB printer. A username is not necessary if you are authenticating the printer on share-level or user-level access. With share-level access, you can add a password for each shared printer or file system.

+   ♦ Password—Password associated with the SMB name or the shared resource, depending on the kind of access being used.

> Caution When enter a User and Password for SMB, information is stored encrypted in the /etc/cups/printers.conf file. Be sure that the file remains readable by root.

Complete the rest of the procedure as you would for a local printer (see “Adding a Local Printer in Red Hot” section earlier in this chapter).

The result is new entries in the /etc/cups/cupsd.conf and printers.conf files. This /etc/cups/printers.conf entry shows the printer entry created:

```
<Printer NS1-PS>
Info Created by redhat-config-Eprinter 0.6.x
DeviceURI smb://jones:my9passwd@FREET/NS1/hp
Location HP on ns
State Idle
Accepting Yes
JobNames none none
QuotaPeriod 0
PageLimit 0
Klimit 0
</Printer>
```

![](bbox=[0.131, 0.588, 0.209, 0.663])