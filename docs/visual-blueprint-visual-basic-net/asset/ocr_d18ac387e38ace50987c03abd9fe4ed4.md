# USING ADO.NET

# Disconnected Recordsets

Although previous versions of ADO added disconnection as an afterthought, ADO.NET, through major changes in design, focuses its functionality around disconnected data. When you connect to a database, you actually load all of the data in tables of the database into the client application's memory. ADO.NET performs all of the data manipulation to these in-memory copies of the table information. When the user finishes with the form or application, and makes changes to the database, you can reconnect to the database. ADO.NET looks through the in-memory data and makes changes to synchronize the two.

Because of disconnection, you must carefully design your database. Large tables may perform poorly when you load them into memory. To improve speed, you must filter only necessary data down to a particular client. Also, multiple users can connect to a database, retrieve a table, make changes, and update the same records.

# Object Model

In ADO.NET, the Object Model recreates all of the functionality present in a database system. The Object Model must replicate the database contents because the database does not stay connected to the client. The DataTable object represents a single table of a database, and consists of DataColumn objects, which define the fields, and DataRow objects, which store the records of the table. A DataTable resides in a DataSet object, which is the main wrapper control, and can hold any number of tables. The DataSet object also allows you to create relationships between tables using DataRelation objects. These objects, the core set of data for storage and manipulation, allow you to bind the data to controls, whether the components connect to an actual database or not.

# ADO.NET OBJECTS

The connection and adapter components provide the basic ability for connecting to a database, while the DataSet provides storage in memory for everything that makes up tables and relationships. See the section "Add a Connection to a Form" for more information. The table, row, and column objects provide the underlying data and manipulation abilities for the DataSet object.

# DbConnection

To attach a database to your application, you first create a data connection object. Microsoft includes two components that implement the DbConnection interface, OleDbConnection and SqlConnection. The OleDbConnection components allow you to connect to any database that the OLEDB interface supports, and SqlConnection allows you to connect to a Microsoft SQL Server database. This chapter develops database applications using the SQL connection classes, but you can substitute the use of OLEDB classes because they use the same interfaces, methods, and properties.

# DataSet

The DataSet component is the major component for retrieving and manipulating information. The DataSet object stores a set of tables from the database, including their field definitions and all of the associated data. Controls can bind to the DataSet or contained tables to view or modify the data.

# DataAdapter

A data adapter provides the conduit for connecting a DbConnection to the objects in ADO.NET that actually store and manipulate the database information. For a particular connection component, you must have a specific adapter that understands how to communicate with the connection. Microsoft provides the SqlDataAdapter and the OleDbDataAdapter, depending on which DbConnection you use.

# DataTable

The DataTable object represents a single database table. Because the database source disconnects, this object must provide all the abilities of an actual database table. The DataTable object relies on DataColumn objects to define the fields of the table and DataRow objects to store the actual data of the table. See the section "Work with Data Tables" for more information on the DataTable object.