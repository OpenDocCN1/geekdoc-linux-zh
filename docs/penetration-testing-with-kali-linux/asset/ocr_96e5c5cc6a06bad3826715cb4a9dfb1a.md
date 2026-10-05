# OffSec Penetration Testing with Kali Linux

```
kalikali:~/Downloads$ exiftool -u brochure.pdf
Exiftool Version Number : 12.41
File Name : brochure.pdf
Directory : 
File Size : 303 KiB
File Modification Date/Time : 2022:04:27 02:37:04:00
File Access Date/Time : 2022:04:28 07:56:58:00
File Inode Date/Time : 2022:04:28 07:56:54:00
File Permissions : -rw-
File Type : PDF
File Type Extension : pdf
MIME Type : application/pdf
PDF Version : 1.7
Linearized : No
Page Count : 4
Language : en-US
Tagged PDF : Yes
XMP Tool : Image::ExifTool 12.41
Creator : Stanley Velantes
Title : Mountain Vegetables
Author : Stanley Stanley
Producer : Microsoft PowerPoint® for Microsoft 365
Create Date : 2022:04:27 07:34:01+02:00
Create Tool : Microsoft PowerPoint® for Microsoft 365
Modify Date : 2022:04:27 07:34:01+02:00
Document ID : uuid:B6EED371-D165-4BD4-B9C9-A15FA9C3A3CF
Instance ID : uuid:B6EED371-D165-4BD4-B9C9-A15FA9C3A3CF
Title : Mountain Vegetables
Author : Stanley Velantes
Create Date : 2022:04:27 07:34:01+02:00
Modify Date : 2022:04:27 07:34:01+02:00
Producer : Microsoft PowerPoint® for Microsoft 365
Creator : Stanley Velantes
```

Listing 2.1: Displaying the metadata for brochure.pdf

This generated list of the most important information include the file creation date, last modified date, the author, the operating system, and the application used to create the file.

The Create Date and Modify Date sections reveal the relative age of the document. Given that these dates are recent (at the time of this writing) we have a high level of trust that this is a good source of metadata.

The Author section reveals the name of an internal employee. We could use our knowledge of this person to establish a trust relationship by dropping their name casually into a targeted email or phone conversation. This is especially helpful if the author maintains a relatively small profile.

The output further reveals that the PDF was created with Microsoft PowerPoint for Microsoft 365. This is crucial information for us to plan our client-side attack since we know that the target uses Microsoft Office and since there is no mention of "macOS" or "for Mac" in any of the metadata tags, it's probable that Windows was used to create this document.

We can now leverage client-side attack vectors against Windows systems to create malicious Documents.