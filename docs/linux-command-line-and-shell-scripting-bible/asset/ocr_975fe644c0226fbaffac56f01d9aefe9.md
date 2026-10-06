# Using a Database

The psql program displays the output from each command directly to STDOUT in the order of
you specify them.

Of course, you're not limited to just retrieving data from the tables. You can use any type of SQL
command in your script, such as an INSERT statement:

```
cat mest4
!/bin/bash
# send data to the table in the MySQL database

MYSQL=`which mysql`

if [ $ -ne 4 ]
then
  echo "Usage: mest4 empid lastname firstname salary" ($1, '$2', '$3', '$4')
else
  statement="INSERT INTO employees VALUES ($1, '$2', '$3', '$4')"
  $MYSQL - test << EOF
  $Statement
EOF
if [ $? -eq 0 ]
then
  echo Data successfully added
else
  echo Problem adding data
fi
./mest4
Usage: mest4 empid lastname firstname salary
./mest4 5 Blum Jasper 100000
Data added successfully
$
./mest4 5 Blum Jasper 100000
ERROR 1062 (23000) at line 1: Duplicate entry '5' for key 1
Problem adding data
```

This example demonstrates a few things about using this technique. When you specify the end of
file string, it must be the only thing on the.line, and the line must start with the string. If I had
entented the EOF text to match the rest of the if-then indentation, it wouldn't work.

Also, notice how I used the special $? variable to test the exit status of the mysql program. The
helps determine whether the command failed or not.

Just sending output from the commands to STDOUT is not the easiest way to manage and manip-
ulate the data. The next section shows you some tricks you can use to help your scripts capture
data retrieved from the database.