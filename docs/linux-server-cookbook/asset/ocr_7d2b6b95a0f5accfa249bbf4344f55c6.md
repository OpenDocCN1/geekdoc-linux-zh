![](bbox=[0.35, 0.09, 0.65, 0.11])

SQL syntax is case-insensitive. The statements can be written in lower case, upper case, or combination. A recommendation for easy readability is to use upper case for the SQL keywords and lower case for the objects and the data provided. Some useful commands syntax are described as follows.

# CREATE statement

This statement is used to create objects of the specified type. The syntax is the following:

```
CREATE [ OR REPLACE ] <object_type> [ IF NOT EXISTS ] <object_name> [ <object_type_properties> ] [ <object_type_params> ]
```

For example, to create a new database named school, which will contain tables and other objects, the syntax is as follows:

```
CREATE DATABASE school;
```

To create a table, it is required to define the columns and the definition for each column. The following example creates a table called students with three columns, one of them defined as PRIMARY KEY.

```
CREATE TABLE students (id INTEGER PRIMARY KEY, name CHAR(20), lastname CHAR(50));
```

# DROP statement

This statement is used to delete objects of the specified type. The syntax is the following:

```
DROP <object_type> [ IF EXISTS ] <identifier> [ CASCADE | RESTRICT ]
```

For example, to delete the table previously created named students, the following syntax should be used:

```
DROP TABLE students;
```

# ALTER statement

This statement is used to modify an object. The syntax is as follows:

```
ALTER <object_type> <object_name> <actions>
```