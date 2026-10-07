# CHAPTER 17 Administering Database Services in Red Hat Linux

few values and they aren't in sequential order), you can specify which columns you want the data to go in, using the following syntax:

```
INSERT table_name (column1,column4) VALUES('value1', 'value2');
```

You can also fill multiple rows with a single INSERT statement, using syntax such as the following:

```
INSERT INTO table_name VALUES('value1', 'value2'),('value3', 'value4');
```

In this statement, value1 and value2 are inserted into the first row, and value3 and value4 are inserted into the second row.

The following example shows how you would insert the African lion entry into the serengeti_mammal database:

```
INSERT INTO serengeti_mammal VALUES('African Lion', 'Carnivora', 'Felidae', 'Panthera', 'leo', NULL);
```

MySQL requires the NULL value for the last column (sub_species) if you do not want to include a subspecies. PostgreSQL on the other hand, lets you get away with just omitting the last column. Of course, if you had columns in the middle that were null, you would need to explicitly state NULL in the INSERT statement.

Normally, INSERT statements are coded into a front-end program so that users adding data to the database don't have to worry about the SQL statements involved.

# Retrieving Data from a Database

Of course, the main reason for storing data in a database is so you can later look up, sort, and generate reports on that data. Basic retrieval is done with the SELECT statement, which has the following syntax:

```
SELECT column(s) FROM table_name WHERE search_criteria;
```

The first two parts of the statement—the SELECT and FROM parts—are required. The WHERE portion of the statement is optional. If it is omitted, all rows in the table table_name are returned.

columns(s) indicates the name of the columns that you want to see. If you want to see multiple columns, you can list them, separated by commas. If you want to see all columns, you can also use the wildcard * to show all columns that match the search criteria. For example, the following statement would display all columns from the records that match the search criteria:

```
SELECT * FROM serengeti_mammal;
```