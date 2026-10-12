These limitations obviously make the flat-file database unsuitable for any kind of serious work in even a small business—much less in an enterprise environment. Relational data-bases, or relational database management systems (RDBMS) to give them their full name, are good at finding the relationships between individual pieces of data. An RDBMS stores data in tables with fields much like those in spreadsheets, making the data searchable and sortable. RDBMSs are the focus of this chapter.

Oracle, DB2, Microsoft SQL Server, and the freely available PostgreSQL and MySQL are all examples of RDBMS. The following sections discuss how relational databases work and provide a closer look at some of the basic processes involved in administering and using databases. You will also learn about SQL, the standard language used to store, retrieve, and manipulate database data.

# How Relational Databases Work

An RDBMS stores data in tables, which you can visualize as spreadsheets. Each column in the table is a *field*; for example, a column might contain a name or an address. Each row in the table is an individual record. The table itself has a name you use to refer to that table when you want to get data out of it or put data into it. Figure 22.1 shows an example of a simple relational database that stores name and address information.

| last_name | first_name | address | city | state | zip | phone |
|---|---|---|---|---|---|---|
| Doe | John | 501 Somestreet | Anytown | NY | 55011 | 555-555-1212 |
| Doe | Jane | 501 Somestreet | Anytown | NY | 55011 | 555-555-1212 |
| Palmer | John | 205 Anystreet | Sometown | NY | 55055 | 123-456-7890 |
| Johnson | Robert | 100 Eastystreet | Eastytown | CT | 12345 | 111-222-3333 |

![](bbox=[0.07, 0.6, 0.83, 0.67])

In the example shown in Figure 22.1, the database contains only a single table. Most RDBMS setups are much more complex than this, with a single database containing multiple tables. Figure 22.2 shows an example of a database named sample_database that contains two tables.

In the sample_database example, the phonebook table contains four records (rows) and each record hold three fields (columns) of data. The cd_collection table holds eight records, divided into five fields of data.

If you are thinking that there is no logical relationship between the phonebook table and the cd_collection table in the sample_database example, you are correct. In a relational database, users can store multiple tables of data in a single database—even if the data in one table is unrelated to the data in others.