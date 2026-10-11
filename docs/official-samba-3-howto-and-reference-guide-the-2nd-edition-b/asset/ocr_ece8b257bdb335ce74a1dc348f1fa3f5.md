# **Figure 21.9** Raster to Printer-Specific Formats.

![](bbox=[0.1, 0.1, 0.85, 0.44])

servers). Examples for CUPS device-URIs to use are `ipp://192.193.194.195/ipp` (for many HP printers) and `ipp://remote_cups_server:631/printers/remote_printer_name`.

**http** This backend sends print files to HTTP-connected printers. (The `http://` CUPS backend is only a symlink to the `ipp://` backend.) Examples for the CUPS device-URIs to use are `http://192.193.194.195:631/ipp` (for many HP printers) and `http://remote_cups_server:631/printers/remote_printer_name`.

**smb** This backend sends print files to printers shared by a Windows host. Examples of CUPS device-URIs that may be used include:

+   * `smb://workgroup/server/printersharename`
+   * `smb://server/printersharename`
+   * `smb://username:password@workgroup/server/printersharename`
+   * `smb://username:password@server/printersharename`

The `smb://` backend is a symlink to the Samba utility `smbspool` (does not ship with CUPS). If the symlink is not present in your CUPS backend directory, have your root user create it: `ln -s 'which smbspool' '/usr/lib/cups/backend/smb'`.

It is easy to write your own backends as shell or Perl scripts if you need any modification or extension to the CUPS print system. One reason could be that you want to create “special” printers that send the print jobs as email (through a “mailto:” backend), convert them to PDF (through a “pdfgen:” backend) or dump them to `/dev/null`. (In fact, I have the systemwide default printer set up to be connected to a default; there are just too many people sending jobs without specifying a printer, and scripts and programs that do not name a printer. The systemwide default deletes the job and sends a polite email back to the $USER asking him or her to always specify the correct printer name.)