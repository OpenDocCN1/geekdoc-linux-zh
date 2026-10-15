
On the server side you have to configure the DB2 instance so that clients can connect to any database within this instance.

Verify on the server side these following items:

- The DB2 service name and port are set in the file `/etc/services`, for example:

  ```
  db2c_db2inst1 50001/tcp
  ```

- The `DB2COMM` registry variable is set for TCP/IP:

  ```
  db2set -all
  ```

  and look at `DB2COMM=tcpip`.

- TCP/IP service name in database manager configuration should be set:

  ```
  db2 get dbm cfg | grep SVCENAME
  ```

  Output:
  
  ```
  TCP/IP Service name (SVCENAME) = db2c_db2inst1
  ```

## Installing DB2 Administrator Client on Linux

Once you have checked the prerequisites as specified in 2.1, "Basic requirements" on page 24, do the following tasks:

1. Log in as root user.
2. Mount your CD-ROM or copy the DB2 Code to disk.
3. Enter the command `./db2setup` and the DB2 setup wizard will start.
4. Follow the instructions under the wizard to install the client.

After installing your DB2 Client, you should configure the client to access a remote DB2 server. DB2 Version 8 only supports TCP/IP to administer a remote database.

To configure the client, start the Configuration Assistant graphical tool by typing `db2ca &` as a valid DB2 user or open it in the DB2 folder (Figure 3-26).

![](img/d95c931f4f3da4a6bd0ee55148fefad7_137_0.png)

Figure 3-26 Add Database Wizard in CA

In the next window, select Search Network and click Next. Expand the tree under Known systems until you see all databases on this system. Select your desired database. After filling out all required fields, you can test a connection to this database (Figure 3-27).

![](img/d95c931f4f3da4a6bd0ee55148fefad7_138_0.png)

Figure 3-27 Connection test window

To configure many clients in your company, perform all configurations on one client and export the definition to a flat file. The file can be transferred to each client and imported under Configuration Assistant (Figure 3-28).

```
Comment = DB Server udblnx02
Directory entry type = LOCAL
Protocol = TCPIP
Hostname = udblnx02
Service name = 50001
```

```
# db2 list db directory

Database 1 entry:

Database alias = ITSODB
Database name = ITSODB
Node name = UDBLNX02
Database release level = a.00
Comment = Test database for ITSO
Directory entry type = Remote
Authentication = SERVER
Catalog database partition number = -1
```

```
# db2 connect to itsodb user db2inst1 using <password>

Database Connection Information

Database server = DB2/LINUX 8.1.0
SQL authorization ID = DB2INST1
Local database alias = ITSODB
```

> Note: For more details and explanation, refer to the IBM DB2 UDB Command Reference V8, SC09-4828.

## 3.7 Configuring licensing

DB2 is a licensed product. There are two tools that you can use to configure the license policy: the DB2 License Center and the db2licm utility. The License Center is a graphical tool found within the Control Center and db2licm is its command line counterpart. This section provides instructions about how to configure licensing using both of these tools. The following topics will be discussed:

- Installing the license key
- Setting up the Registered user policy
- Updating the number of licensed processors
- Changing the enforcement policy

All of these tasks are optional, as they depend on the version of DB2 you are using (*Try and Buy* or fully licensed) and the type of license policy your company purchased.

### 3.7.1 DB2 License Center

The DB2 License Center is a graphical tool found within the Control Center that manages licensing. You can use this tool to view license information, add and remove license keys, specify user and enforcement policies, and specify the number of licensed processors. It can also generate usage statistics and display connection information for current users. To access the License Center, do the following:

1. Log in as instance owner.
2. From Control Center, select **License Center** from the **Tools** menu.
3. Select which system and product on which you want to configure licensing. You may configure a local or remote system. Select **DB2 Enterprise Server Edition** from the Installed products menu.

![](img/d95c931f4f3da4a6bd0ee55148fefad7_141_0.png)

Figure 3-29 DB2 License Center

### Installing a license key

To install a license key using the License Center, you must add the *db2ese.lic* license file as follows:

1. Select **Add** from the License menu.
