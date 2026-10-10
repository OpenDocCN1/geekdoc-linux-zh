**TABLE 1.1 Continued**

| **Property** | **Description** |
| :--- | :--- |
| `LoadParamsOnConnect` | When `True`, dbExpress loads the `DriverName`, `GetDriverFunc`, `LibraryName`, `Params`, and `VendorLib` from the `dbxconnections.ini` configuration file at runtime. When `False`, all properties must be set at design time. |
| `LoginPrompt` | When `True`, dbExpress prompts the user for username and password information when connecting to the database. When `False`, the application must supply username and password information directly, through the `Params` property. |
| `Params` | Enables you to set database-specific parameters at design time or at runtime. See the section “Setting Database Parameters” for more information. |
| `TableScope` | Specifies the types of information returned by `GetTableNames`. This property is discussed in more detail in the section “Retrieving Database Metadata.” |
| `VendorLib` | Refers to the database vendor client library used for connecting to the database server. For example, InterBase supplies the `gds32.dll` client-side library. |

# ## Establishing the Connection

To connect to a database, set the appropriate connection properties and issue one of the following two statements:

```
SQLConnection1.Connected := True;
```

or

```
SQLConnection1.Open;
```

Both of these statements do the same thing, and it is up to you to decide whether you prefer to set a property or call a method to connect to the database.

The properties you set depend on whether you elect to use a named connection or an unnamed connection. Both connection types are discussed in the following two sections.

# ## Named Connections

Named connections refer to the fact that you set the properties for a connection in the file `dbxconnections.ini`, and give the properties a name. For example, the following example illustrates how you might set up a named connection for an accounting package:

![](bbox=[0.86, 0.15, 0.97, 0.26])