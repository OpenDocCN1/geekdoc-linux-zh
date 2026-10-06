# Chapter 13 ✦ Working with Files 361

One problem is it is difficult to extract the pure text from all the markup and formatting instructions. Another is that there have been several revisions of the RTF specification. RTF files open well in any of the Linux word processing applications, including those that have a smaller footprint than OpenOfficeorg.

# Working with Excel Files

Microsoft Excel files usually open just fine in OpenOfficeorg or Gnumeric provided that they do not include macros, in which case you may have difficulties.

> OpenOfficeorg has its own macro language, but this is not compatible with VBA (Visual Basic for Applications), which is used by Microsoft Office. In general, this means that you will have to convert or rewrite the macros in an Excel workbook to make it work in OpenOfficeorg.

# Working with Access Files

Microsoft Access databases are a problem in more ways than once: Until, there was no freely available open Linux desktop application with similar functionality. That has been changed with the release of Recall under an open source license. Recall is included in SUSE Linux Professional.

To deal with this that Access creates (.mdb files), the Mdbtools project may be useful: http://mdbtools.sourceforge.net/.

Otherwise, the best approach is to use an intermediate format (such as .csv or a SQL dump) for export and import.

# The OpenOfficeorg Native File Formats

The OpenOfficeorg native files are zipped archives that contain a variety of XML documents, as in the following example:

```
userfile--> file.zip
file.zip: Zip archive data, at least v2.0 to extract

userfile--> zipinfo.asm
Archive: file.zip  9043 bytes 7 files
-rw--      30 B-  stor 23-Jun-04 11:39 mimetype
-rw--      2.0 fat         18 b- stor 23-Jun-04 11:39 layout-cache
-rw--      2.0 fat        10336 defl 23-Jun-04 11:39 content.xml
-rw--      2.0 fat        17791 defl 23-Jun-04 11:39 styles.xml
-rw--      2.0 fat        1168 b- stor 23-Jun-04 11:39 media.xml
-rw--      2.0 fat        8560 defl 23-Jun-04 11:39 META-INF/manifest.xml
7 files, 37247 bytes uncompressed, 8261 bytes compressed: 77.8%
```

XML is a structured markup language, which means that all OpenOffice documents are ultimately text documents, unlike the traditional Microsoft formats, which are