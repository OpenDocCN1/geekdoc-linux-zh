
## GNOME Office and Ximian

Office applications for GNOME have been developed independently, such as the Gnumeric spreadsheet. Most are accessible from various More menus such as More Office Applications for AbiWord and Gnumeric, or More Internet Applications for Galeon. The chart rendering tool, DIA, though, is included in the main Office menu. GNOME Office integrates various independent office applications such as Gnumeric and AbiWord into a productivity suite. Sun Microsystems has also integrated OpenOffice into GNOME, making all OpenOffice applications part of GNOME Office. You can find out more from the GNOME Office at www.gnome.org/gnome-office. Here, you can link to download pages for current versions and view screen shots. A current listing is shown in Table 11-4. All implement the CORBA model for embedding components, ensuring drag-and-drop capability throughout the GNOME interface. All are based on a set of GNOME technologies, including Bonobo, Gnome-Print, and XML. Bonobo is the GNOME architecture for supporting compound documents and reusable software components. Gnome-Print is the GNOME printing architecture designed to support graphics applications as well as work easily with any printing resource. XML is used as the native file format to support the easy exchange of data between GNOME applications.

Currently, GNOME Office includes AbiWord, Gnumeric, GIMP, Dia, Eye of GNOME, Evolution, and GNOME-DB. AbiWord is a word processor, Gnumeric is a spreadsheet, GIMP is the GNOME image editing application, Dia is a diagram composer, Eye of GNOME is an image viewer, Evolution is an integrated e-mail and personal information manager, and GNOME-DB provides database connectivity (see Table 11-4).

Table 11-4: GNOME Office

| Application | Description |
|---|---|
| AbiWord | Cross-platform word processor |
| Balsa | E-mail client |
| Gfax | Send and receive faxes |
| Galeon | Web browser |
| Gnumeric | Spreadsheet |
| Gnucash | Personal finance manager |
| Dia | Diagram and flow chart editor |
| Evolution | E-mail and calendar |
| Eye of GNOME | Image viewer |
| GIMP | GNU image manipulation program |
| GNOME-DB | Database connectivity |
| Gnumeric | Spreadsheet |
| Evolution | Integrated email, calendar, and personal organizer |
| Gnumeric | Spreadsheet |
| Guppi | Plotting and graphing program |
| Sketch | Vector drawing package |
| Toudoux | Project manager |
| OpenOffice | OpenOffice office suite |

Gnumeric is the GNOME spreadsheet, a professional-level program meant to replace commercial spreadsheets. Like GNOME, Gnumeric is freely available under the GNU Public License. Gnumeric is included with the GNOME release, and you will find it installed with GNOME on any distribution that supports GNOME. Its development is currently managed by Ximian. You can download current versions from www.ximian.com or www.gnome.org/projects/gnumeric. Gnumeric supports standard GUI spreadsheet features, including autofilling and cell formatting, and it provides an extensive number of formats. It supports drag-and-drop operations, enabling you to select and then move or copy cells to another location. Gnumeric also supports plug-ins, making it possible to extend and customize its capabilities easily.

AbiWord is an open source word processor that supports such features as unlimited undo operations and Word 97 imports. It is part of a set of desktop productivity applications being developed by the AbiSource project (www.abisource.com).

GIMP is the GNU image manipulation program, which supports operations such as photo retouching, image composition, and image authoring (see the section on graphics in Chapter 12). You can obtain more information from www.gimp.org.

Dia is a drawing program designed to create diagrams. You can select different kinds of diagrams to create, such as database, circuit object, flow chart, and network diagrams. You can easily create elements along with lines and arcs with different types of endpoints such as arrows or diamonds. Data can be saved in XML format, making it easily transportable to other applications.

Eye of GNOME (EOG) is an image viewer that can also function as an image cataloging program. It is designed to be fast and provide high-quality image displays.

GNOME-DB is a suite of libraries and applications that allow easy access to different database systems. It provides an API to which databases can plug in. These back-end connections are based on CORBA. Through this API, GNOME applications can then access a database. You can find out more about GNOME-DB at www.gnome.org/gnome-db.

Ximian is a GNOME project designed to provide a professional-level desktop for GNOME that will include a full range of office applications. You can find out more about Ximian at www.ximian.com. Ximian currently provides an enhanced version of the GNOME desktop called Ximian Desktop. It also supports development of the Gnumeric spreadsheet. Its first office application is a contact, calendar, and mail client application called Evolution (see Chapter 13). Evolution has become the standard mail client for Red Hat Linux. It does not require Ximian GNOME to run. Their next project is a word processor.

## Document Viewers (PostScript, PDF, and DVI)

Though located under Graphic headings in both the main menu and the Start Here window, PostScript, PDF, and DVI viewers are more commonly used with Office applications (see Table 11-5). Linux features a tool called Ghostview that can display any PostScript file. Several applications can view both Adobe PDF and PostScript files. PostScript (.ps) and PDF (.pdf) files can be displayed using GNOME Ghostview (GGV) or KGhostView. Another application, xpdf, displays only PDF files. Alternatively, you can download Acrobat reader for Linux from Adobe to display PDF and PostScript files. All these viewers also have the ability to print PDF and PostScript documents.

Table 11-5: PostScript, PDF, and DVI viewers

| Viewer | Description |
|---|---|
| GNOME Ghostview (GGV) | GNOME interface for displaying PostScript and PDF files |
| KGhostView | KDE interface for displaying PostScript and PDF files |
| xpdf | X Window System tool for displaying PDF files only |
| KDVI | KDE tool for displaying TeX DVI files (plug-in to KViewShell) |
| Acrobat Reader | Adobe PDF and PostScript display application |

Linux also features a professional-level typesetting tool, called TeX, commonly used to compose complex mathematical formulas. TeX generates a DVI document that can then be viewed by DVI viewers, of which there are several for Linux. DVI files generated by the TeX document application can be viewed by KDVI. KDVI is a plug-in to the KViewShell tool that can display and print any kind of document for which it has a plug-in. You can access KDVI as the DVI Viewer in the Graphics menu.

These applications are available under the Graphics submenu. xpdf bears the name PDF viewer, GGV uses the name Postscript viewer, KGhostView is named PS/PDF viewer (More Graphic Applications), and KDVI is called DVI viewer.

## Database Management Systems

Database software can be generally organized into three categories: SQL, Xbase, and desktop databases. SQL-based databases are professional-level relational databases whose files are managed by a central database server program. Applications that use the database do not access the files directly. Instead, they send requests to the database server, which then performs the actual access. SQL is the query language used on these industrial-strength databases. Red Hat Linux includes both MySQL and PostgreSQL databases. Both are open source projects freely available for your use. Table 11-6 lists DBMSs currently available for Linux.

The Xbase language is an enhanced version of the dBase programming language used to access database files whose formats were originally developed for dBase on the PC. With Xbase, database management systems can directly access the database files. Xbase is used mainly for smaller personal databases, with database files often located on a user's own system.

### SQL Databases (RDBMS)

SQL databases are relational database management systems (RDBMS) designed for extensive database management tasks. Many of the major SQL databases now have Linux versions, including Oracle, Informix, Sybase, and IBM (but not, of course, Microsoft). These are commercial and professional database management systems of the highest order. Linux has proved itself capable of supporting complex and demanding database management tasks. In addition, many free SQL databases are available for Linux that offer much the same functionality. Most commercial databases also provide free personal versions, as do Oracle, Adabas D, and MySQL.

Table 11-6: Database Management Systems for Linux

| System | Site |
|---|---|
| PostgreSQL | The PostgreSQL database: www.postgresql.org |
| MySQL | MySQL database: www.mysql.com |
| Oracle | Oracle database: www.oracle.com |
| Sybase | Sybase database: www.sybase.com |
| DB2 | IBM database: www.software.ibm.com/data/db2/linux |
| Informix | Informix database: www.informix.com/linux |
| Adabas D | Adabas D database: www.softwareag.com/adabasd |
| GNU SQL | The GNU SQL database: www.ispras.ru/~kml/gss |
| Flagship | Interface for Xbase database files: www.fship.com/free.html |

### PostgreSQL

PostgreSQL, included with Red Hat, is based on the POSTGRES database management system, though it uses SQL as its query language. POSTGRES is a next-generation research prototype developed at the University of California, Berkeley. Linux versions of PostgreSQL are included in most distributions, including Red Hat, Debian, and Mandrake distributions. You can get more information on it from the PostgreSQL Web site at www.postgresql.org. PostgreSQL is an open source project, developed under the GPL license.

> Note Red Hat now offers a version of Linux with PostgreSQL, called the Red Hat Database, that is optimized for database operations.

PostgreSQL is often used to provide database support for Internet servers with heavy demands such as Web servers. With a few simple commands, you can create relational database tables. Use the createuser command to create a PostgreSQL user that you can then log into the server with. You can then create a
