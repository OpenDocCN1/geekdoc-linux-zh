Since Rails 2.0, Rails utilizes the SQLite3 database system by default to store data values. The SQLite3 database system uses a single file to store all tables in a database. Part of the Rails process is to create the database file used for the application.

If you prefer to use a MySQL server to store your Rails project database, you must ensure that MySQL is installed on your Ubuntu server, either by installing the LAMP server in Ubuntu server (see Chapter 21, "LAMP Server") or just the MySQL server package, if you don't want to install Apache and PHP as well.

After ensuring you have the MySQL server installed, you have to add the MySQL Rails library file, called libmysql-ruby from Synaptic or apt-get. This allows Rails to access the MySQL database server from the project code.

After your Rails and MySQL environments are installed, you can specify the MySQL database on your rails command line:

```
rails -d mysql addressbook
```

The Rails application creates a file called database.yml in the config folder created for the Rails project. You'll need to edit this file to add the password for the MySQL root user account for your MySQL server.

After creating the Rails project environment, you're ready to create your application code. First, you'll need to be in the newly created application folder that was created by the rails command:

```
rich@testbox:~$ cd addressbook
rich@testbox:~/addressbook$
```

The Rails framework creates a series of Ruby scripts you use to interact with the Rails environment. The generate script creates the model, controller, and view code files automatically.

Rails also includes a special generate option called scaffold. The scaffold option creates the model and controller code files, along with all of the required view code files to implement a complete CRUD web application for a table you define in the command line.

You just define the controller name, along with the data fields and data types you want in the table. Here's how to do that: From the newly created addressbook folder (make sure you're in the addressbook folder or this procedure won't work), enter this command (on one line):

```
rich@testbox:~/addressbook$ ruby script/generate scaffold person lastname:string firstname:string address:string city:string state:string zip:string phone:string comments:text
```

This command is just one statement and should all be on one command line. It generates all of the MVC files required to implement the person controller and interface with a database table called people (Rails makes all table names plural from the model names).