![](bbox=[0.0, 0.0, 0.8, 0.4])

FIGURE 18.3 You can use three related tables to track customers, orders, and outstanding invoices.

# ## Understanding SQL Basics

SQL (pronounced “S-Q-L”) is a database query language understood by virtually all RDBMS available today. You use SQL statements to get data into and retrieve data from a database. As with statements in any language, SQL statements have a defined structure that determines their meanings and functions.

As a DBA, you should understand the basics of SQL, even if you will not be doing any of the actual programming yourself. Fortunately, SQL is similar to standard English, so learning the basics is simple.

# ### Creating Tables

As mentioned previously, an RDBMS stores data in tables that look similar to spreadsheets. Of course, before you can store any data in a database, you need to create the necessary tables and columns to store the data. You do this by using the CREATE statement. For example, the cd_collection table from Figure 18.2 has five columns, or fields: id, title, artist, year, and rating.

SQL provides several column types for data that define what kind of data will be stored in the column. Some of the available types are INT, FLOAT, CHAR, and VARCHAR. Both CHAR and VARCHAR hold text strings, with the difference being that CHAR holds a fixed-length string, whereas VARCHAR holds a variable-length string.