# Chapter 8

+   - **Methods**	Shows how to add callable methods to an application server.
+   - **LocalConn**	Shows how to implement a single-EXE database application using multiter techniques.
+   - **Stateless COM+**	Shows how to create a stateless application server for use with MTS or COM+.

# Chapter 9

+   - **ConMan**	A complete sample application that draws on many of the techniques discussed throughout the book to create a simple contact manager.

With respect to the source code, each chapter has its own subdirectory, with VCL and CLX subdirectories under it. In turn, the VCL and CLX subdirectories have a separate subdirectory for each sample application.

In addition to a subdirectory for each chapter, there is a separate subdirectory named Components, which contains the data-aware component descendants mentioned earlier. The Data subdirectory contains the common.gdb data file used in a number of the sample applications and the SQL script file (connman.sql) used to create the database.

If you maintain this directory structure on your own drive, the sample programs should all run fine out of the box. They are set up to access the CONMAN database using the relative path .\.\.\.\.\Data\connman.gdb. If you have trouble running the sample programs, you might want to modify them to provide a complete path to the data, such as D:\Data\connman.gdb.

# dbExpress

dbExpress is Borland's newest database-access technology, supported both by Delphi and Kylix. Several database access technologies are supported by Delphi in previous releases, including BDE, ADO, and IBX. With these three technologies, you may wonder why we need a new one. dbExpress has a number of exciting characteristics, including

+   - **Cross-platform**	Whereas BDE and ADO are specific to the Windows platform, dbExpress currently operates under Windows and Linux (the two platforms that Delphi/Kylix support). If Borland ever decides to support another platform, such as Mac, BE, or what have you, dbExpress will be there also.
+   - **Low overhead**	dbExpress is a thin layer over the underlying database engine's API. For this reason, it adds very little overhead to database operations.
+   - **High-performance**	Largely because of its low overhead, dbExpress is extremely high-performance. It is designed to work in conjunction with Delphi's client dataset technology.