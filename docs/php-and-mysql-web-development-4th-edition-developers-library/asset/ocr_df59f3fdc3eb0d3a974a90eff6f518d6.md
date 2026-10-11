You can execute this statement a couple of ways. Either enter it manually by typing it in, or use the prewritten statement that is contained in the create_president.sql file of the sampDB distribution.

If you want to type in the statement yourself, invoke mysql, making sampDB the default database:

```
% mysql sampDB
```

Then enter the CREATE TABLE statement as just shown, including the trailing semicolon so that mysql can tell where the statement ends. Indentation doesn't matter, and you need not put the line breaks in the same places. For example, you can enter the statement as one long line if you want.

To create the president table using a prewritten description, use the create_president.sql file from the sampDB distribution. This file is located in the sampDB directory that is created when you unpack the distribution. Change location into that directory, and then run the following command:

```
% mysql sampDB < create_president.sql
```

Whichever way you invoke mysql, specify any connection parameters you might need (hostname, username, or password) on the command line after the command name.

Now let's look more closely at the CREATE TABLE statement. Each column specification in the statement consists of the column name, the data type (the kind of values the column will hold), and possibly some column attributes.

The two data types used in the president table are VARCHAR and DATE. VARCHAR(n) means the column contains variable-length character values, with a maximum length of n characters each. That is, they contain strings that might vary in size, but with an upper bound on their length. You choose the value of n according to how long you expect your values to be. state is defined as VARCHAR(2); that's all we need for entering states by their two-character abbreviations. The other string-valued columns need to be wider to accommodate longer values.

The other data type we've used is DATE. This type indicates, not surprisingly, that the column holds date values. However, what might surprise you is the format in which dates are represented. MySQL expects dates to be written in 'CCYY-MM-DD' format, where CC, YY, MM, and DD represent the century, year within the century, month, and day of the month. This is the SQL standard for date representation (also known as "ISO 8601 format"). For example, to specify a date of "July 18, 2005" in MySQL, you use '2005-07-18', not '07-18-2005' or '18-07-2005'.

The only attributes we're using for the columns in the president table are NULL (values can be missing) and NOT NULL (values must be filled in). Most columns are NOT NULL, because we'll always require a value for them. The two columns that can have NULL values are suffix (most names don't have one), and death (for living presidents, there is no date of death).