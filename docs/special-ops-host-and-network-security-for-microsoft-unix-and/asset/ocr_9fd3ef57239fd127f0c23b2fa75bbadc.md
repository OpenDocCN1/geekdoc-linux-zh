attacking and defending Windows Server 2003. You will be able to find this article on the Special Ops Security's Web site at www.SpecialOpsSecurity.com.

> WARNING
When you install Terminal Services on Windows Server 2003, your currently-installed programs will no longer work in a TS session and will need to be reinstalled. All future applications for T5 will need to be installed using Add Or Remove Programs in the Control Panel.

# Terminal Server Clients

Terminal Services offers a wide range of options when it comes to selecting a client. Users can connect with their Windows 95 systems to a Terminal Server down the hall or across the Atlantic, harnessing the raw power of a 32-processor Windows 2000 Datacenter Server. Terminal Services clients even exist for the Linux, Mac, and the PocketPC. Although each client may look different, all implement RDP in a similar manner, connecting to TCP port 3389 unless configured to do otherwise.

# Windows Remote Desktop Client

Microsoft now offers a single client solution to connect to Terminal Services that will run on operating systems from Windows 95 to Windows XP. The client that I recommend because it forces 128-bit encryption and offers the ability to connect to ports other than 3389. To connect to an alternate port, just add it to the IP address specified with a colon: 10.1.1.1:9999. This client is available on the Windows XP Professional CD and from www.microsoft.com/windowsxp/pro/downloads/rdclientdl.asp.

To install the CD:

+   1. Insert the CD.
2. On the Welcome page, click Perform Additional Tasks.
3. Click Set up Remote Desktop Connection. Remote Desktop Connection runs on most of Microsoft's operating systems, including Windows 95/98/ME/NT 4, Windows 2000, and Windows XP. The Terminal Server Client window is shown in Figure 9.4.