A device URI (Uniform Resource Identifier) can be used to specify a printer. Device URIs are used in some of the CUPS command-line tools, for example **lpadmin**.

A device URI for the IPP protocol would look like the following:

`ipp://cputserver/printers/printqueue`

+   - **LPD (Line Printer Daemon)**—The LPD protocol is described in RFC 1179 (requests for comments can be found at http://www.ietf.org/rfc.html).
+     
+     Because some job-related data, such as the printer queue, is sent before the actual print data, a printer queue must be specified when configuring the LPD protocol for the data transmission.
+     
+     The implementations of most printer manufacturers are flexible enough to accept any name as the printer queue. The printer manual might indicate which name to use (such as LPT, LPT1, or LP1).
+     
+     An LPD queue can also be configured on a different Linux or UNIX host in a network that uses the CUPS system. The port number for an LPD service is 515.
+     
+     Device URI example: `lpd://host-printer/LPT1`.

+   - **SMB (Server Message Block)**—CUPS supports printing on printers connected to Windows shares. The protocol used for this purpose is SMB.
+     
+     SMB uses port numbers 137, 138, and 139.
+     
+     Device URI examples:
+     
+     `smb://user:password@workgroup/server/printer`
+     
+     `smb://user:password@host/printer`
+     
+     `smb://server/printer`

+   - **IPX**—This protocol is used to print via a Novell NetWare Server.

+   - **socket**—This protocol is used to connect to a printer, such as HP’s JetDirect, equipped with a network port. Some socket port numbers that are commonly used are 9100 or 35.
+     
+     Device URI example: `socket://host-printer:9100/`.

The dialogs that appear next depend on your choice. We will cover three of them here:

+   - Print via CUPS Network Server
+   - Print Directly to a Network Printer
+   - Print to an SMB Printer