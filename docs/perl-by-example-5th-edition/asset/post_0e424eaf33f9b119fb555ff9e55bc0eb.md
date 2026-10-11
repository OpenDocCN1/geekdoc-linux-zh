
Although SQL commands are not case sensitive, by convention, SQL keywords are capitalized for clarity, whereas only the first letter of the field, table, and database names is capitalized.

```
SELECT * FROM Persons WHERE FirstName='John'
```

When performing pattern matching with the LIKE and NOT LIKE commands, the pattern being searched for is case sensitive when using MySQL.

## The Result Set

A result set is just another table created to hold the results from a SQL query. Most database software systems even allow you to perform operations on the result set with functions, such as Move-To-First-Record, Get-Record-Content, Move-To-Next-Record, and so forth. In the example shown in Figure 15.12, the result set is the table created by asking MySQL to show all the fields in the table called shippers.

![](img/8556abcb353c0991f12099420ec28735_559_0.png)

Figure 15.12 The result set is just a table produced from a query.

## 15.3 Getting Started with MySQL

MySQL is an open-source, full-featured relational database management system and has been ported to most platforms, including Linux, Windows, OS/X, HP/UX, AIX, and more. MySQL is portable, fast, reliable, scalable, and easy to use. It is the world's second most widely used relational database management system, said to be installed in more than 10 million computers all over the world, including Antarctica.1

There are two versions, one in which you buy a commercial license and one that is free (*‘free’* meaning you can use MySQL in any application as long as you don’t copy, modify, or distribute the MySQL software). MySQL supports a number of APIs (application programming interfaces), including Perl, PHP, TCL, Python, C/C++, Java, and others.

When working with MySQL, a number of like-name terms are used. Table 15.2 is provided to help clarify the use of these terms.

4. MySQL is free use for those who are 100 percent GPL. See [http://www.mysql.com/company/legal/licensing/opensource-license.html](http://www.mysql.com/company/legal/licensing/opensource-license.html) for details.

### Table 15.2 The Terms in MySQL

| Term | Definition |
| --- | --- |
| MySQL | The actual software for the database management system |
| mysqld | The MySQL daemon, or server process |
| *mysql monitor* | The monitor where MySQL commands are issued (command-line interpreter) |
| *mysql* | The name of the database MySQL uses to manage access privileges |
| *mysqladmin* | A MySQL utility program for administrating the database |

### 15.3.1 Installing MySQL

Here, we assume you have installed a database server and it is running. Downloading and installing MySQL is usually a straightforward process. You can get MySQL from the *mysql.com* Web site or use integrated applications, such as XAMPP or WAMP. XAMPP (for Windows, Linux, Mac OS, and Solaris) is a free, easy-to-install Apache distribution containing MySQL, PHP, and Perl. All you have to do is download, extract, and start it up. For details, go to [http://www.apachefriends.org/en/xampp.html](http://www.apachefriends.org/en/xampp.html).

For complete installation instructions, go to [http://dev.mysql.com](http://dev.mysql.com) (see Figure 15.13).

![](img/8556abcb353c0991f12099420ec28735_560_0.png)

**Figure 15.13** The MySQL installation documentation.

### 15.3.2 Connecting to MySQL

The MySQL database system uses the client/server model described in Section 15.2.1, “Client/Server Databases.” You are the client connecting to the database from the command line, a graphical user interface, or from a program. Before connecting to the database from a Perl program, we will first use the MySQL command-line client.

The MySQL command-line client comes with the MySQL installation and is universally available. It is a *mysql* program located in the *bin* folder of your MySQL installation. To run this command-line application, you must start the command-line prompt.

- On Windows, go to the *Start* menu, choose the *Run...* option, and then type *cmd* in the run window.
- On Mac OS X, go to the *Applications* folder in your *Finder* and then navigate to *Utilities*. You will find the *Terminal* application there. You should navigate to the location where you installed MySQL and find the *bin* folder.
- With UNIX, type commands at the shell prompt in a terminal window.

The MySQL client executable is normally located in the *bin* folder.

To connect to a database using this client, you will enter information similar to the following line:

```
mysql --user=root --password=my_password --host=localhost
```

Regardless of the type of client you choose, you may be required to specify the user name and the host machine to which you are connecting. Most configurations expect you to have a password, although if just working by yourself, it is not required. You have the option to specify the default database as well.

Once you are successfully connected, you will get the *mysql>* prompt instead of your standard DOS/UNIX prompt (see Figure 15.14). This means you are now sending commands to the MySQL database server and not to your local computer's operating system.

![](img/8556abcb353c0991f12099420ec28735_561_0.png)

**Figure 15.14 The MySQL client.**

**Editing Keys at the MySQL Console**. MySQL supports input-line editing. The up-arrow and down-arrow keys enable you to move up and down through previous input lines, and the left-arrow and right-arrow keys let you move back and forth within a line. The Backspace and Delete keys are used to erase characters from the line and type in new characters at the cursor position. To submit an edited line, press Enter. For UNIX users, MySQL also supports tab completion, allowing you to enter part of a keyword or identifier and complete it using the Tab key.

**Setting a Password**. When you download MySQL, on some installations, you may be asked to enter a password for user *root*. Even if you are not forced to create a password, it is a good idea to set one to protect the security of your database. To set a password, go to the MySQL console and type the following MySQL command. Replace `'MyNewPassword'` with your password.

```
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('MyNewPassword');
```

After setting the password, you can stop the MySQL server and then restart it in normal mode again. If you run the server as a service, start it from the Windows Services window. If you start the server manually, use whatever command you normally use. You should be able to connect using the new password.

The following example shows how to set the password at the *mysql* prompt.

# EXAMPLE 15.1

```
1       $ mysql -u root
        ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO)
        $ 
        $ mysql -u root -p
        Enter password: ********
        Welcome to the MySQL monitor.  Commands end with ; or \g.
        Your MySQL connection id is 91 to server version: 5.0.21-community-nt

        Type 'help;' or '\h' for help.  Type '\c' to clear the current buffer.
```

### 15.3.3 Graphical User Tools

**The MySQL Query Browser.** The MySQL Query Browser is a graphical user interface (GUI) client available from *mysql.com* used to connect to the MySQL database server. Once you download it and follow the simple installation wizard, you can start the application from the *Start* menu under Windows.

The MySQL Query Browser then displays a connection dialog box (see Figure 15.15). You must specify the MySQL server where you want to connect, the credentials needed for authorization on that server, which machine that server runs on (and which port it listens to), and the default database (called the **schema**) you will be using. There are also a number of additional options you can specify if necessary.

You must choose a default database in order to issue queries. Although it is possible to choose a default database after connecting to the server, setting the default from the connection dialog can save time on subsequent connections.

![](img/8556abcb353c0991f12099420ec28735_563_0.png)

The information to enter is very similar to the command-line client: **user name**, **password**, and the server host where the database server is running. You can optionally enter the database name and port number (3306 is the default for MySQL) and save the connection information as a bookmark under the *Stored Connection* section.

By using the familiar tree-like navigation structure on the right-hand side of the application window, you can also navigate the various databases in the MySQL Query Browser (see Figure 15.16).
