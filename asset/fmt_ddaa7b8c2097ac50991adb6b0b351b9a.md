
## Overview of MySQL GUI Tools

`MySQL` has a graphical tool known as `MySQLGUI` for some time. This tool is still available from the `MySQL` Web site, but development is now concentrated on an alternative tool, the `MySQL` Control Center, or `MySQLCC`. The `MySQL` Control Center is a very useful all-around tool, and one worth installing.

We strongly suggest you look at `MySQLCC`; it's a powerful, stable, and easy-to-use graphical interface for `MySQL` that is available precompiled for both `Linux` and `Windows` (even the source code is available if you want it). It allows you to both administer a `MySQL` server and execute `SQL` through a GUI interface.

If `MySQLCC` is not available on your `Linux` distribution, you can download a copy from the `MySQL` Web site and follow the simple installation instructions. Alternatively, you can manage your copy of `MySQL` running on your `Linux` server directly from `MySQLCC` running on a `Windows` desktop. It looks and runs almost identically.

### First Launch

The first time you run `MySQLCC`, you will be presented with a blank Control Center window, with an empty Console Manager, as shown in Figure 8-2. Hovering the mouse over the first icon on the toolbar reveals that this is the icon for creating a new connection.

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_363_0.png)

**Figure 8-2**

When you click this button, you will be asked for some basic details in an additional popup window (see Figure 8-3).

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_364_0.png)

**Figure 8-3**

If you want to manage your server remotely from a `Windows` PC, then configuration is almost identical, except that you need to enter a host name or `IP` address in the Host Name field, as shown in Figure 8-4.

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_364_1.png)

**Figure 8-4**

All the information you need to provide is the name to identify the connection (which can be anything you choose), the host name, the user name, and the password. All other values are filled in by default for you. Then click the Test button, which will tell you which connection is okay.

Then click Add to add this connection to the list. The name `gw1` (or whatever chose—`gw1` just happens to be the name of the machine it is running on) should be displayed in the list of `MySQL` servers, and by clicking it you should be able to drop down more information, as you can see in Figure 8-5.

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_365_0.png)

**Figure 8-5**

If you explore the database section, you can see the tables, and by right-clicking a table, you can edit the table definition or the data in the table, as you can see in Figure 8-6.

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_366_0.png)

**Figure 8-6**

You can also edit users and their permissions, execute `SQL`, look at connections to the database, and do many other things.

## Accessing MySQL Data from C

Now that we have the rudiments of `MySQL` out of the way, let's explore how to access it from our own application, rather than using `mysql` or the basic `mysql` client.

`MySQL` can be accessed from many different languages. We know of:

- `C`

- `C++`

- `Java`

- `Perl`

- `Python`

- `REXX`

- `Tcl`

- `PHP`

`ODBC` drive is also available for accessing `MySQL` from `Windows`-native applications such as Access; and there is even an `ODBC` driver for `Linux`, although little exists to use it.

In this chapter, we'll limit ourselves to the `C` interface because it is the primary focus of this book and because the same libraries facilitate connection by a number of other languages.

## Connection Routines

The two steps involved in connecting to a `MySQL` database from `C` are:

- Initializing a connection handle

- Physically making the connection

First we'll use `mysql_init` to initialize our connection handle:

```c
*mysql_init (MYSQL *);
```
