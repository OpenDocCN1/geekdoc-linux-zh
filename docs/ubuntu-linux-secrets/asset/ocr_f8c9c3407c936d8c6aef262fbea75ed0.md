The model code includes code to interact with the database table, as well as create the database table. Before you can use the new code, you need to use the rake command to build the actual database in the database server from the model code. Again, from the addressbook folder, enter these commands:

```
rich@testbox:~/addressbook$ rake db:migrate
(in /home/rich/addressbook)
== 20081111220445 CreatePeople: migrating ====================
-- create_table(:people)
-> 0.0262s
== 20081111220445 CreatePeople: migrated (0.0295s) ====================

rich@testbox:~/addressbook$
```

The db:migrate command builds the new table for the person model. You can use the sqlite3 program installed in Ubuntu to take a peek at the database table created here.

The database file is located in the db folder under the addressbook folder:

```
rich@testbox:~/addressbook$ cd db
rich@testbox:~/addressbook/db$ ls -l
total 16
-rw-r--r-- 1 rich rich 5120 2008-12-21 16:13 development.sqlite3
drwxr-xr-x 2 rich rich 4096 2008-12-21 16:12 migrate
-rw-r--r-- 1 rich rich 1082 2008-12-21 16:13 schema.rb
rich@testbox:~/addressbook$
```

Rails creates separate databases for the development, test, and production environments. It creates the default database for the development environment and calls it development.sqlite3. You can use the sqlite3 command to look at what's inside:

```
rich@testbox:~/addressbook/db$ sqlite3 development.sqlite3
SQLite version 3.5.9
Enter ".help" for instructions
sqlite> .tables
people schema_migrations
sqlite> .dump people
BEGIN TRANSACTION;
CREATE TABLE "people" ("id" INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
"lastname" varchar(255) DEFAULT NULL NULL, "firstname" varchar(255) DEFAULT NULL NULL, "address" varchar(255) DEFAULT NULL NULL, "city" varchar(255) DEFAULT NULL NULL, "state" varchar(255) DEFAULT NULL NULL, "zip" varchar(255) DEFAULT NULL NULL, "phone" varchar(255) DEFAULT NULL NULL, "comment" text DEFAULT NULL NULL, "created_at" datetime DEFAULT NULL NULL, "updated_at" datetime DEFAULT NULL NULL);
COMMIT;
sqlite> .exit
rich@testbox:~/addressbook/db$
```

The rake command created the people table in the database, using the data field names supplied, plus a few extra data fields to track information specifically for Rails.

Believe it or not, you're now ready to test out your Rails project!