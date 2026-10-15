
## CREATE A DATABASE CONNECTION

To access a database in an application, you must create a connection to it via the Server Explorer. You can attach a number of database formats to your application using ADO.NET, which provides the same interface to multiple formats.

When you open the Server Explorer window in the Development Environment, it presents a list of the current database connections. The Server Explorer also displays a list of servers, which allow you to access remote data objects. From the Server Explorer window, you can access the Data Link Property dialog box. Here, you can create a new connection, tell VB .NET what type of data provider to use, and name the database. For databases that support password protection, you see options to enter the appropriate password, which allows you to connect to the database.

You can access a list of advanced settings when creating the connection. These settings, which depend on the data provider you use, enable you to edit access permissions for the application’s connection and specify connection timeouts.

After you create the connection, VB .NET shows you the database in the Server Explorer and lists all of the tables, views, and stored procedures available in the database. You can edit the database contents directly in Visual Basic .NET via the tables in the Server Explorer. This allows you to make quick changes to test data before you complete the entire application interface.

Adding a connection to the Server Explorer does not change your project. The Server Explorer stores database connections independently. Only when you add the connection to a form does the database actually become a part of your project. For more information on adding a connection you create in the Server Explorer to a form, see the section “Add a Connection to the Form.”

![](img/d6f772854306e15fb6df39b861a7b541_221_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_221_1.png)

1 Access the Server Explorer window.
2 Click the Connect to Database button ( ).
Note: Click View > Server Explorer if you do not have the Server Explorer open.

The Data Link dialog box appears.
3 Click the Provider tab.
4 Select the appropriate database provider for your data.

The example uses the Microsoft OLE DB Provider for SQL Server.
5 Click Next.

## Extra

The Server Explorer provides the ability to edit and modify table information. The Development Environment includes an entire database editor package. You can use the abilities provided in the Development Environment to add tables, modify designs, and modify data present in a database. To add a new table, right-click the Tables category inside the connected database and click New Table. You can modify the design of an existing table by right-clicking an existing table and clicking Design Table. To edit the data inside an existing table, click Retrieve Data from Table.

You can use the Advanced tab of the Data Link Properties dialog box to specify network protection levels. The protection level determine how and when the client must authenticate with the server to ensure an accurate and untampered connection over the network. The Call setting makes the client authenticate the source of the data on each request. You can use the Connect setting, which requires that the client authenticate at the first connection, to improve the speed of the data connection while maintaining minimum security. When you select None, no authentication takes place. These settings only appear when you connect to a database over a network, and the database supports these authentication options.

![](img/d6f772854306e15fb6df39b861a7b541_222_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_222_1.png)

6 Type a server name, or click and then the appropriate server.

7 Type the name of, or click to select, the database to use.

You can click the option to enter log-on information to the server and then type the username and password.

You can click the Advanced tab to alter advanced connection properties.

8 Click OK.

The Server Explorer creates the connection and shows the information available in the database.

Note: See the section "Add a Connection to the Form" to add the connection to a form.
