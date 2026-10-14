Using the system shell—Log in as root and enter the following at the command line:
$mysqladmin create university

Using the MySQL shell—To log in to the MySQL shell, issue the command mysql in your shell and it will launch immediately. Read the section “Administering MySQL” later in this chapter for further information about logging in.

When you run the MySQL shell, your prompt will be mysql>. At this prompt, you can enter SQL commands and MySQL-specific commands. When you run the MySQL shell, you get a welcome message and some information such as the connection ID and MySQL version. At the MySQL prompt, enter the command create database followed by a database name to create a database. The following example shows how you can create a database called university:

```
bash$ mysql
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 18 to server version: 3.22.21
Type 'help' for help.
mysql>create database university;
```

# Creating Tables

Creating tables is accomplished by using normal SQL commands. Before you can create a table, you have to be connected to a database. Consider that you created a database called university:

```
mysql>connect university;
mysql>create table student (ID char (30) NOT NULL ,Name char (30) NOT NULL);
mysql>create table course (Number char (30) NOT NULL ,SID char (30) NOT NULL);
```

You have created two tables. The first table is called student and contains students’ names and IDs. The second table is called course and contains course numbers and IDs of students who are registered in the course.

# The show Command

The show command is an important command in MySQL. You can use the show command to check which databases exist, which tables exist, what the database status is, and other important information. For example, issue the following command:

```
mysql>show tables;
+-------------------+
| Tables in university |
+-------------------+
| course            |
| student           |
+-------------------+
2 rows in set (0.01 sec)
```