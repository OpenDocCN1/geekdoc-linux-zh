
LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id) \G

Run this and you’ll see the following:

```
*************************** 1. row ***************************
make_name: Ford
model_name: Explorer
color: Dark Blue
modelyear: 2005
price: NULL
description: Popular SUV; great for moving people or cargo across town, or wherever your adventures may take you.
NULL: NULL
1: 1
*************************** 2. row ***************************
make_name: NULL
model_name: NULL
color: Graphite Pearl
modelyear: 2004
price: NULL
description: Last of the 2004 stock! Must sell! Loaded, all options!
NULL: NULL
1: 1
*************************** 3. row ***************************
make_name: Toyota
model_name: Tacoma
color: Radiant Red
modelyear: 2005
price: NULL
description: Come drive this terrific truck! 4WD, extended cab, many options.
NULL: NULL
1: 1
*************************** 4. row ***************************
make_name: Chevrolet
model_name: Corvette
color: Daytona Sunset Orange Metallic
modelyear: 2005
price: NULL
description: The all new C6 Corvette, the next generation of classic American sportscars. 400HP V8; Very fast!
NULL: NULL
1: 1
*************************** 5. row ***************************
make_name: Honda
model_name: Accord
color: Deep Green Pearl
modelyear: 2003
price: NULL
description: Excellent condition, off-lease vehicle; Must see!
NULL: 0
1: 1
*************************** 6. row ***************************
make_name: Volkswagen
model_name: Golf
color: Reflex Silver
modelyear: 2004
price: NULL
description: R32 Limited edition; Low miles; Understated and suprisingly functional; Loaded.
    NULL: 1
    1: 1
******************* 7. row *********************
make_name: Toyota
model_name: Tacoma
color: Red
modelyear: 1993
price: NULL
description: Runs decent; 4WD; Tinted windows, aftermarket stereo; Needs a little TLC.
    NULL: 0
    1: 0
```

The first thing you'll notice is that it looks a little different than your previous results. This is because of the `\G` terminator at the end of the query, which causes MySQL to display results vertically (otherwise, the tables would be far too wide for this book). Aside from that, every bit of information is present and accounted for. The `NULL` value specified for the missing “certified” column in the New_Vehicles table is present, as well as the placeholder value you specified as 1, since all new cars have a warranty. You send the changes back to the client, and they are pleased (for the time being at least).

## Full-Text Searching

The owners of the car lot have been impressed so far with your ability to query exactly what they need, give the various listings to help increase the productivity of their sales staff—but they still want more. What they'd like now is a way to search through the car inventories by keyword. Their search needs aren't too complex, but a simple `LIKE` comparison in a `WHERE` clause just isn't going to get the job done.

What you need just happens to be built into MySQL—full-text searching. Full-text search, which is enabled by default in MySQL, allows you to perform a natural-language search on any text column you specify. You can't just go out and start full-text searching at will in your database, though — you have to do some preparation first.

### Enabling Full-Text Searching

Enabling full text searching in MySQL involves simply creating an index on a column or columns for a table. You can do this one of two ways: when the table is created, as part of the `CREATE TABLE` command, or later on in the life of the table.

#### Creating a New Table with Full-Text Search Enabled

The first full-text index you're going to create will be part of a brand new table. To specify a full-text index at table-creation time, all you have to do is specify a full-text index and the list of indexed columns at the end of the column specifications:

```
CREATE TABLE tablename (column_specs, FULLTEXT (columns_to_index))
```

You can specify a single column in the FULLTEXT column list, or multiple columns in a comma-delimited list. It’s time to actually create a table with full-text searching in the VehicleInventory database:

```
CREATE TABLE testft (testint int, testvc varchar(50), testtxt text, FULLTEXT (testvc, testxt));
```

You’ve just created a new table with a full-text index on the testvc and testtxt columns.

#### Altering an Existing Table to Support Full-Text Search

Modifying an existing table to support full-text searching is a little bit trickier, but not by much. To add full-text search capability for an existing table, you use MySQL’s ALTER TABLE command, like so:

```
ALTER TABLE tablename ADD FULLTEXT (columns)
```

Now add a full-text index to the New_Vehicles table:

```
ALTER TABLE New_Vehicles ADD FULLTEXT (description);
```

Once that’s done, it’s time to put these indexes to good use.

## Querying Using Full-Text Search

Searching through a table in MySQL with full-text indexing enabled is a relatively painless process. All you need to do is use the MATCH() function in a WHERE clause, like so:

```
SELECT [columns] FROM [table] WHERE MATCH ([indexed_columns]) AGAINST (‘keyword’)
```

Inside the parameter list for MATCH, you can specify any number of columns, as long as they are part of a full-text index.

Returning to the vehicle inventory database, it’s time to perform a search on the list of new vehicles. To search for the word “options,” you can use the following:

```
SELECT vehicle_id, description FROM New_Vehicles WHERE MATCH (description) AGAINST (‘options’);
```

Which should return the following:

| vehicle_id | description |
| :--- | :--- |
| 2 | Last of the 2004 stock! Must sell! Loaded, all options! |
| 3 | Come drive this popular truck! 4WD, extended cab, many options. |

Another neat trick that full-text searching can do is order the items by relevance, and return the relevance as well. To utilize relevance data, you can use the MATCH()...AGAINST() functions in both the SELECT list and the ORDER BY clause, like so:

```
SELECT MATCH (description) AGAINST('options') AS relevance, description FROM
New_Vehicles WHERE MATCH (description) AGAINST ('options') ORDER BY MATCH
(description) AGAINST('options') \G
```

Which returns the following:

```
*************************** 1. row **********************
relevance: 0.38341856002808
description: Last of the 2004 stock! Must sell! Loaded, all options!
*************************** 2. row **********************
relevance: 0.38341856002808
description: Come drive this popular truck! 4WD, extended cab, many options.
```

## Limitations

When using full-text search, there are a few limitations you must keep in mind. First, MySQL supports only full-text indexes on MyISAM table types (covered in the next section). Second, in most situations, if you create a full-text index on more than one column, the list of columns you provide to MATCH() must be the exact same list you specified when you created the full-text index. Last, MySQL has a default minimum word/token length of four characters. If you try to match a full-text search against a keyword that has three or fewer letters, no results will be returned.

To change the default minimum full-text word length, make sure the following exists in your MySQL configuration file *my.cnf*:

```
[mysqld]
ft_min_word_len=3
```

You may use any integer for the minimum length (set to 3 in this example).

## InnoDB Tables

One of the advantages to using MySQL is that you’re not limited to a certain storage engine for your data. What’s a storage engine? MySQL, as a server, provides the user with a consistent interface and querying language, but is only loosely coupled with the way it actually stores the data on the disk. The different storage engines in MySQL provide differing ways to store and access the data, from the trusty default MyISAM, to the sizzling speed of in-memory Heap tables, and all stops in between. One of the most flexible and powerful table types you can use is InnoDB. The InnoDB storage engine, created by Innobase Oy in Helsinki, Finland, provides MySQL with a safe and efficient way to store and process data, and gives MySQL some additional functionality not present with MyISAM or most of the other table types.

## InnoDB Advantages

Although the default MyISAM table type gives you a mature and speedy way to store simple data structures, it is lacking a handful of the features that many developers want—and InnoDB can provide. Available by default since MySQL 4.0, InnoDB tables give you the ability to use transactions, row-level locking, and best of all, foreign key constraints.
