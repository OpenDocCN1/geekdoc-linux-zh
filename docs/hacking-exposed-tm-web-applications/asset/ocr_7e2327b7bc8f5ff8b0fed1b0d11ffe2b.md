# Hacking Exposed Web Applications

Extended Stored Procedures The extended stored procedures, signed by the “xp_” prefix, provide robust system administration entirely from the comfort of SQL. We will cover countermeasures at the end of this chapter, but we’ll hint that one countermeasure involves removing these commands entirely. Table 9-4 lists some procedures that do not require a parameter. Table 9-5 contains a list of procedures that require a parameter. require a parameter.

These commands cover just about any aspect of system-level access. Also, before you're tempted to use xp_regread to grab the SAM file, you should know that technique only works against systems that do not have Syskey enabled. Windows 2000 enables this by default.

Default Local Tables (the Useful Ones) Also known as System Table Objects, these tables contain information about the database and the operating system. Table 9-6 lists tables that have the most useful information.

The easiest method to retrieve information from one of these tables is a SELECT * example:

```
SELECT * FROM sysfiles
```

However, if you are familiar with databases, then you can parse the request to certain fields—for example, view all stored procedures:

```
SELECT name FROM sysobjects WHERE type = 'P'
```

Default Master Tables (the Useful Ones) Table 9-7 lists selected tables from the Master database. These tables provide detailed information on the operating system and

| Extended Stored Procedure | Description |
|---|---|
| xp_loginconfig | Displays login information, particularly the login mode (mixed, etc.) and default login. |
| xp_logininfo | Shows currently logged in accounts. Only applies to NTLM accounts. | |
| xp_msver | Lists SQL version and platform information. |
| xp_enumdn | Enumerates ODBC data sources. |
| xp_enumgroups | Enumerates Windows groups. |
| xp_ntsec_enumdomains | Enumerates domains present on the network. |
| Table 9-4. | Extended Procedures That Do Not Require Parameters |