
```sql
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `students` (
  `id` int(11) NOT NULL,
  `name` char(20) DEFAULT NULL,
  `lastname` char(50) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `students`
--

LOCK TABLES `students` WRITE;
/*!40000 ALTER TABLE `students` DISABLE KEYS */;
INSERT INTO `students` VALUES (1, 'Alberto', 'Gonzalez');
/*!40000 ALTER TABLE `students` ENABLE KEYS */;
UNLOCK TABLES;
```

The command **mariadb** ( **mysql** ) allows to use the **standard input** to specify the actions to be performed. *Figure 11.28* shows how to use **mariadb-dump** to export the database content to be recreated, the usage of the **standard input** to drop the existing table, and the use of redirection to import the content from a file.

```bash
[agonzalez@rhel ~]$ mariadb-dump -pP@ssw0rd -h192.168.122.43 school > school.sql
[agonzalez@rhel ~]$ echo "DROP TABLE students;" | mariadb -p -h192.168.122.43 school
Enter password:
[agonzalez@rhel ~]$ echo "SHOW TABLES;" | mariadb -p -h192.168.122.43 school
Enter password:
[agonzalez@rhel ~]$ mariadb -pP@ssw0rd -h192.168.122.43 school < school.sql
[agonzalez@rhel ~]$ echo "SHOW TABLES;" | mariadb -p -h192.168.122.43 school
Enter password:
Tables_in_school
students
```

> Figure 11.28: Output example operating with mariadb-dump and mariadb commands

## SQLite

The database engine **SQLite** is a library to be used as embedded for the applications. With this solution, it is not needed to have a database server running. The database will be using a file that can be distributed. Users can use the command `sqlite` to operate with the databases, and the applications using the library available would be able to access the database file.

The command **sqlite** is part of the package **sqlite3** (in Debian and derivatives distributions) or part of the package **sqlite** (Red Hat Enterprise Linux and derivatives). The package is less than 1 megabyte in size. The command can be executed without any argument, but the common usage is to specify an existing file that contains the database and the data or an empty file that will be used and initialized as a database file.

**SQLite** clients can work in interactive and using the standard input. Most of the *SQL statements* explained during this chapter can be used inside the client. Figure 11.29 illustrates the creation of a new database file and the creation of a table inside.

```bash
root@ubuntu:~# sqlite3 school.db
SQLite version 3.37.2 2022-01-06 13:25:41
Enter ".help" for usage hints.
sqlite> CREATE TABLE students (id INTEGER PRIMARY KEY, name CHAR(20), lastname CHAR(50));
sqlite> INSERT INTO students VALUES(1, "Alberto", "Gonzalez");
sqlite> SELECT * from students;
1|Alberto|Gonzalez
```

*Figure 11.29: Output example SQLite*

In the interactive mode, it is possible to type .help to obtain the actions possible using the client. Some of the popular options able to perform are described in table 11.6:

| **Action** | **Description** |
| :--- | :--- |
| .backup FILE | Backup DB to FILE |
| .changes on/off | Show the number of rows changed by SQL |
| .dbinfo | Show status information about the database |
| .dump ?OBJECTS? | Render database content as SQL |
| .headers on/off | Turn the display of headers on or off |
| .show | Show the current values for various settings |
| .tables | List names of tables |

*Table 11.6: Common actions for the interactive mode for SQLite.*

The advantages of using **SQLite** are as follows:

- It is not required to have a server running a database engine.
- The database file can be distributed to different systems that are not required to perform backup and restore.
- Lightweight database with most of the basic database functions.

The command `sqlite` has different options to specify the output format desired. Some of the options are: `--json`, `--list`, and `--table`. **Figure 11.30** illustrates the usage of `sqlite` client with the standard input.

```bash
root@ubuntu:~# echo '.tables' | sqlite3 school.db
students
root@ubuntu:~# echo "SELECT * from students;" | sqlite3 --table school.db
+----+---------+----------+
| id | name | lastname |
+----+---------+----------+
| 1 | Alberto | Gonzalez |
+----+---------+----------+
root@ubuntu:~# echo "SELECT * from students;" | sqlite3 --json school.db
[{"id":1,"name":"Alberto","lastname":"Gonzalez"}]
```

*Figure 11.30: Output example SQLite*

## NoSQL databases

A **NoSQL** (also known as **non-only-SQL** or **non-relation**) database stores the data differently than relational tables. These databases are called *non-tabular databases* and contain a variety of types based on their data model. The popular data structure are as follows:

- **key-value pair:** The simplest type, each object is assigned to a unique key. To obtain the value, it is needed to specify the key.
- **wide column:** It uses tables, rows, and columns, but the names and format of the columns can vary from row to row.
- **graph:** Uses a graph structure for semantic queries with *nodes, edges*, and properties to represent and store data.
- **document:** It stores the data in *JSON* or *XML* format.

NoSQL databases are getting popular for applications generation big quantities of data due to their performance being better than relational databases. Applications used in big data and real-time Web (such as analytics) are some of the main use cases for NoSQL databases. Its unique features are as follows:

- **Flexible schemas:** They do not require to have the same set of fields and the data type for a field.
- **Horizontal scaling:** Adding nodes to share the load is a simple task in *NoSQL*.
- **Fast queries:** Querying a *NoSQL* is faster than a relational database.
- **Ease of use for developers:** For developers, it is easier to use *NoSQL* to store structured or unstructured data.

Some of the popular open-source database *NoSQL* solutions available are as follows:

- **MongoDB**: A document database with the scalability and flexibility that you want with the querying and indexing that you need.
- **Apache Cassandra**: A database designed to store data for applications that require fast read and write performance.
- **Apache CouchDB**: A document database that collects and stores data in JSON-based document formats.
- **Apache Hbase**: A distributed big data store.
- **Redis**: An in-memory key-value data structure store that can be used as a database, cache, or message broker.
- **Neo4j**: A graph database management system.

## MongoDB databases

MongoDB is one of the most popular NoSQL databases used on Linux systems. MongoDB has the following three different editions:

- **Community Server**: It is free and available for Windows, Linux, and macOS.
- **Enterprise Server**: It is free and available for Windows, Linux, and macOS.
- **Atlas**: It is available as an on-demand fully managed service. MongoDB Atlas runs on AWS, Microsoft Azure, and Google Cloud Platform.

The installation of the *Community* version on Ubuntu requires the following steps:

1. Import the public key to use *MongoDB’s* package repository. The following command shows perform it:

```bash
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo tee /etc/apt/trusted.gpg.d/mongodb.asc
```

2. Create a repository file inside `/etc/apt/source.list.d/` with the repository URL. The following command will create the file **mongodb-org-6.0.list:**

```bash
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
```

3. Reload the local package database by running the following command:

```bash
sudo apt-get update
```

4. Install the package `mongodb-org` with the following command:

```bash
sudo apt-get install -y mongodb-org
```

*Figure 11.31* shows the partial output of the installation process:

```bash
root@ubuntu:~# apt-get install -y mongodb-org | tail
Adding user mongodb to group mongodb
Done.
Setting up mongodb-org-shell (6.0.1) ...
Setting up mongodb-database-tools (100.6.0) ...
Setting up mongodb-org-mongos (6.0.1) ...
Setting up mongodb-org-database-tools-extra (6.0.1) ...
Setting up mongodb-org-database (6.0.1) ...
Setting up mongodb-org-tools (6.0.1) ...
Setting up mongodb-org (6.0.1) ...
Processing triggers for man-db (2.10.2-1) ...
```

*Figure 11.31: Output example installing MongoDB*

The installation on Red Hat Enterprise Linux requires to configure a repository in the system similar to the *Ubuntu* steps. The steps are as follows:

1. Create a file `/etc/yum.repos.d/mongodb-org-6.0.repo` with the following content:

```ini
[mongodb-org-6.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/6.0/x86_64/
gpgcheck=1
enabled=1
```
