
# Chapter 8
- Methods Shows how to add callable methods to an application server.
- LocalConn Shows how to implement a single-EXE database application using multiple techniques.
- Stateless Shows how to create a stateless application server for use with MTS or COM+.

# Chapter 9
- ConMan A complete sample application that draws on many of the techniques discussed throughout the book to create a simple contact manager.

With respect to the source code, each chapter has its own subdirectory, with VCL and CLX subdirectories under it. In turn, the VCL and CLX subdirectories have a separate subdirectory for each sample application.

In addition to a subdirectory for each chapter, there is a separate subdirectory named Components, which contains the data-aware component descendants mentioned earlier. The Data subdirectory contains the common.gdb data file used in a number of the sample applications and the SQL script file (common.sql) used to create the database.

If you maintain this directory structure on your own drive, the sample programs should all run fine out of the box. They are set up to access the CONMAN database using the relative path ..\..\..\Data\conman.gdb. If you have trouble running the sample programs, you might want to modify them to provide a complete path to the data, such as D:\Data\conman.gdb.

# dbExpress
dbExpress is Borland's newest database-access technology, supported both by Delphi and Kylix. Several database access technologies are supported by Delphi in previous releases, including BDE, ADO, and IBX. With these three technologies, you may wonder why we need a new one. dbExpress has a number of exciting characteristics, including:

- Cross-platform: Whereas BDE and ADO are specific to the Windows platform, dbExpress currently operates under Windows and Linux (the two platforms that Delphi/Kylix support). If Borland ever decides to support another platform, such as Mac, BE, or what have you, dbExpress will be there also.
- Low overhead: dbExpress is a thin layer over the underlying database engine's API. For this reason, it adds very little overhead to database operations.
- High-performance: Largely because of its low overhead, dbExpress is extremely high-performance. It is designed to work in conjunction with Delphi's client dataset technology.
- Easy to distribute: Again largely because of its low overhead, dbExpress applications are easy to redistribute. A typical multitier application needs to deploy MIDAS.DLL and a dbExpress driver for the back-end database, which commonly weighs in at around 150KB. Contrast this to the BDE’s 10MB footprint.

## Databases Used in This Book
dbExpress can connect to a number of database backends, including InterBase, Oracle, DB2, and MySQL. I had to pick a single database engine to use for the examples presented in this book. I chose InterBase, for four reasons:

- It's free. Anyone can download a free copy of InterBase from Borland’s Web site and work with any of the examples in this book.
- It's universally accessible. InterBase ships on the Delphi and Kylix CDs, so if you have a copy of either Delphi 6 or Kylix, you should already have a copy of InterBase.
- It's manageable. I can easily provide a small InterBase database for download. You can copy the database onto your local machine and be off and running. I don’t need to worry about how I’m going to redistribute a 30MB Oracle database to my readers.
- It’s the only one of the four database engines that I have.

## Conventions Used in This Book
Several typographic conventions are used through Delphi/Kylix Database Development. These have been kept to a minimum in an attempt to make the text as concise and clean as possible, but the ones that have been used should help clarify certain types of text. Specifically, monospace font is used for Web addresses, code listings, and Object Pascal syntax, such as TClientDataSet. Filenames are written with lowercase letters.

## Contacting the Author
If you would like to contact me regarding any questions, comments, or criticism you might have concerning this book, please feel free to email me at Eric.Harmon@txp.turbopower.com. I will do my best to respond to you as quickly as possible. Please understand, though, that I receive a large amount of e-mail on a daily basis, so it can sometimes take a little while.

# Establishing and Using Database Connections

## IN THIS CHAPTER
- Connecting to and Disconnecting from a Database 8
- Retrieving Database Metadata 18
- Executing DDL and DML Statements 27
- Transaction Support 37
- Providing Feedback During SQL Operations 46

In this chapter, I’ll show you how to connect to and disconnect from a database using dbExpress, as well as how to manage the connection after you’ve established it.

## Connecting to and Disconnecting from a Database
Before you can perform any operation on a database, you must connect to it. Connecting to a database ensures that the database is physically accessible from your location and that you have the necessary rights to connect.

Just because you have the rights to connect to a database doesn’t mean you have the right to actually do anything with the database. You might be prevented from creating new tables, modifying data, or even viewing existing data.

To connect to a database using dbExpress, you use the TSQLConnection component. TSQLConnection publishes a short list of properties that you can use to specify connection parameters and attributes. These properties are listed in Table 1.1.

### TABLE 1.1 TSQLConnection Properties
| Property | Description |
| :--- | :--- |
| Connected | A Boolean property that you can set to True to try connecting to a database, or set to False to disconnect. |
| ConnectionName | Used to establish a named connection. Setting ConnectionName automatically sets DriverName, GetDriverFunc, LibraryName, Params, and VendorLib. See the section titled “Named Connections” for more information on setting up a named connection. |
| DriverName | Indicates the type of database you are connecting to, such as InterBase, Oracle, and so on. |
| GetDriverFunc | Specifies the name of the function exported by the dbExpress driver that provides access to the driver. |
| KeepConnection | When True, keeps the connection to the database, even when there are no active datasets for the connection. When False, drops the connection as soon as all active datasets are closed. |
| LibraryName | Specifies the name of the dbExpress database driver, such as dbexptint.dll. |
| userAuthentication | When True, DBExpress reads the DriverName, SetDriverFunc, LibraryName, Params, and VendorLib from the dbconnections.ini configuration file at runtime. When False, all properties must be set at design time. |
| userPrompts | When True, DBExpress prompts the user for username and password information when connecting to the database. When False, the application must supply username and password information directly, through the Params property. |
| Params | Enables you to set database-specific parameters at design time or at runtime. See the section “Setting Database Parameters” for more information. |
| GetTableScope | Specifies the types of information returned by GetTableServes. This property is discussed in more detail in the section “Retrieving Database Metadata.” |
| vendorLib | Returns the database vendor client library used for connecting to the database server. For example, InterBase supplies the gd32.dll client-side library. |

## Establishing the Connection
To connect to a database, set the appropriate connection properties and issue one of the following two statements:

```pascal
SQLConnection1.Connected := True;
```

or

```pascal
SQLConnection1.Open;
```

Both of these statements do the same thing, and it is up to you to decide whether you prefer to set a property or call a method to connect to the database.

The properties you set depend on whether you elect to use a named connection or an unnamed connection. Both connection types are discussed in the following two sections.

## Named Connections
Named connections refer to the fact that you set the properties for a connection in the file dbconnections.ini, and give the properties a name. For example, the following example illustrates how you might set up a named connection for an accounting package:
