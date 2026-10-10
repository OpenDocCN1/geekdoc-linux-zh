The column1, column2, column3 indicates the name of the columns you want to see. If you want to see all columns, you can also use the wildcard `*` to show all the columns that match the search criteria. For example, the following statement displays all columns from the cd_collection table:

```
SELECT * FROM cd_collection;
```

If you wanted to see only the titles of all the CDs in the table, you would use a statement such as the following:

```
SELECT title FROM cd_collection;
```

To select the title and year of a CD, you would use the following:

```
SELECT title, year FROM cd_collection;
```

If you want something a little fancier, you can use SQL to print the CD title followed by the year in parentheses, as is the convention. Both MySQL and PostgreSQL provide string concatenation functions to handle problems such as this. However, the syntax is different in the two systems.

In MySQL, you can use the CONCAT() function to combine the title and year columns into one output column, along with parentheses. The following statement is an example:

```
SELECT CONCAT(title, " (", year, ")") AS TitleYear FROM cd_collection;
```

That statement lists both the title and year under one column that has the label TitleYear. Note that there are two strings in the CONCAT() function along with the fields—these add whitespace and the parentheses.

In PostgreSQL, the string concatenation function is simply a double pipe (||). The following command is the PostgreSQL equivalent of the preceding MySQL command:

```
SELECT (genus||' ('||species||')') AS TitleYear FROM cd_collection;
```

Note that the parentheses are optional, but they make the statement easier to read. Once again, the strings in the middle and at the end (note the space between the quotes) are used to insert spacing and parentheses between the title and year.

Of course, more often than not, you do not want a list of every single row in the database. Rather, you want to find only rows that match certain characteristics. For this, you add the WHERE statement to the SELECT statement. For example, suppose that you want to find all the CDs in the cd_collection table that have a rating of 5. You would use a statement like the following: