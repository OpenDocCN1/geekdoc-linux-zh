
# 176 Databases

Everything from the second line is on what aspell displays. When aspell finds a misspelled word (any word that does not appear in its dictionary), it displays the sentence with the misspelled word (consensus) and highlights the word by enclosing it in a pair of asterisks. Below that sentence, aspell lists possible corrections, numbering them sequentially from i. In this case, aspell lists consensus — the right choice — as the first correction for consensus.

After the sentence, aspell displays a list of 16 options — 10 numbered through 9 and 6 labeled with single letters i, r, I, R and x — followed by a question mark prompt. You have to press one of the numbers or letters from the list shown in the output to indicate what you want aspell to do. The numbered options show 10 possible replacement words for the misspelled word. Here are the meanings of the letter options:

- + Space accept the word time.
- i ignores the misspelled word.
- I ignores all occurrences of the word.
- r replace this occurrence (you have to type a replacement word).
- R replace all occurrences (you have to type a replacement word).
- a accept the word and add it to your dictionary.
- x means save the rest of the file and exit, ignoring misspellings.

These options are sensitive. Make sure you don't have Caps Lock engaged. img/d9230b719dc0ef80851f363d8c6f571.png

Fedora Core comes with two relational databases — PostgreSQL and MySQL. Briefly show how to use PostgreSQL (pronounced Postgres), a powerful and popular relational database (the type of database that works as a collection of tables). You can use Structured Query Language (SQL) to work with the database.

PostgreSQL is developed by a team of developers and distributed under the BSD open-source license. The license has no restrictions on how source code may be used. To keep up with the latest developments, visit PostgreSQL.org.

To check whether PostgreSQL is installed on your system, type rpm -qa. See at least three RPMs — postgresql, postgresql-libs, and postgresql-server. If a message informs you that packages are not installed, you can install them using these steps:

1. Log in as root and insert the DVD into the drive. If you are GNOME or KDE, the DVD mounts automatically. If not, type the following command in a terminal to mount the DVD:
```
mount /mnt/cdrom
```
If you have a primary CD-ROM drive and added a second DVD/CD drive, type mount /mnt/cdrom to mount.

2. Type the following commands to install PostgreSQL:
```
cd /mnt/cdrom
rpm -ivh postgresql*
```
To use PostgreSQL, you have to first log in as root and start the database server with the following command:
```
service postgresql start
```
The PostgreSQL server process starts, called postmaster. The server is a daemon (a background process that runs continuously) that accepts database queries from clients and performs database tasks (such as adding tables). If you want the database server to start whenever you start, type the following command to turn it on:
```
chkconfig postgresql on
```
Now you have to design database, create database in PostgreSQL, and load it with data. To illustrate how to create and load a database, set up a simple catalog database.

PostgreSQL has its own concept of users, separate from Linux accounts. To enable a user to access PostgreSQL databases on your system, you have to add that username as a PostgreSQL user. img/d9230b719dc0ef80851f363d8c6f571.png

To add a PostgreSQL user, follow these steps:

1. Log in as root. Then type the following command in a terminal window:
```
su - postgres
```
You log in as postgres — the username under which the PostgreSQL database server runs. Perform PostgreSQL administrative tasks under this username.

2. Type the following command in a terminal window:
```
createuser
```
This utility program enables you to add PostgreSQL users. The program prompts for a username to add:
Enter name of user to add:

3. Type the Linux username of the user to whom you are giving database privileges. For example, to add myself as a user, type my Linux username `naba`.

4. Answer the two prompts:
```
Shall the new user be allowed to create databases?
(y/n)
Shall the new user be allowed to create more new users?
(y/n)
```
Typically, you don't want a user to create databases or add new users, so you press N to these prompts. You can use this procedure to run `createuser` and add as many database users as you need.

Follow this basic sequence of steps to build a database:

- 1. Design the database. This step involves defining the tables and attributes that will be used to store the information.
- 2. Create an empty database. Before you can add tables, database systems require you to build an empty database.
- 3. Create the tables in the database. In this step, you define the tables using the CREATE TABLE statement of SQL.
- 4. Load the tables with any fixed data. For example, if you have a table of manufacturer names or publisher names (in the case of books), you want to load that table with information that is already known.
- 5. Back up the initial database. This step is necessary to ensure that you can create the database from scratch.
- 6. Load the data into tables. You may either load data from an earlier dump of the database or actively through forms.
- 7. Use the database. Make queries, update records, or insert new records using SQL commands.

My simple example doesn't follow all the possible steps of database building. For the example, the database-design step is trivial because my book-catalog database includes only a single table. The attributes of table are as follows:

- Book title with 50 characters
- Name of first author with up to 20 characters
- Name of second author (if any) with 20 characters
- Name of publisher with 30 characters
- Page count as a number
- Year as a number (such as 2002)
- International Book Number (ISBN), as 10-character text (such as 076456934)

I store the ISBN without the dashes in a typical book. I also use the ISBN as the primary key of the table because the ISBN is a worldwide identification system for books. That means each book entry must have a unique ISBN, which is true for books.

To create an empty database in PostgreSQL, use the createdb command. You have to log in root and then become the postgres user to run the createdb program. Type the following commands to assume the postgres username:
```
su
(Enter the root password)
- postgres
```
After becoming postgres, you can create the database. For example, to create a database named books, which the database user naba owns, I type the following commands:
```
createdb -0 naba books
```
When you no longer need a database, run the dropdb command under the postgres username to remove it. To learn more about the createdb and dropdb commands, type the following commands:
```
man createdb
man dropdb
```

After you create the empty database, all of your interactions with the database are through the psql program — the PostgreSQL interactive terminal acts as a client to the database server. You have to run psql with the name of a database as an argument. The psql program prompts you for input. Here is an example (the first line is what you type):

```
psql books
Welcome to psql 7.4, the PostgreSQL interactive terminal.

\copyright for distribution terms
\h for help with SQL commands
\? for help on internal slash commands
\g or terminate with semicolon to execute query
\q to quit
```

```
books=>
```

When creating tables or loading data into tables, a typical approach is to place the SQL statements (along with psql commands such as \g) in a file
