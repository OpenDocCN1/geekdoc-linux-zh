
## QUICK TAKES

comes with a command-line client program that is packed with features, allowing you to manipulate your database by sending SQL queries. I have become spoiled by some of the features of the PostgreSQL command line, such as the expanded output (\x). The command-line interfaces for both databases have grown more useful over time. Although the MySQL interface might appear to have fewer commands, that’s partly because MySQL has made some data available via SQL queries (for example, SHOW TABLES), which would require more complicated queries in PostgreSQL, leading to the creation of a shorthand command, \d. Both command-line interfaces use GNU readline, making it easy to edit and re-issue queries. Both also allow users to edit the previous query using the \e command.

Overall, it’s probably fair to say that PostgreSQL offers a superset of MySQL’s capabilities, aside from a few issues (for example, built-in text indexing). Those capabilities that PostgreSQL does not have, such as new data types and functions, are added into the system easily, without needing to recompile or otherwise modify the core PostgreSQL source. That said, I believe MySQL’s capabilities are nothing to sneeze at and are likely more than adequate for most applications you might be writing.

## Administration

Both MySQL and PostgreSQL are amazingly easy to administer, especially in small- and medium-size cases. You (optionally) change a few configuration options, start the server and then walk away. There’s really not much more to do than that. For anyone who has worked with a larger database system, such as Oracle, this is a refreshing change. However, there are slight differences in the ways the two systems operate.

PostgreSQL relies on several external UNIX-level commands to create and manage databases and users, as well as the activity of the PostgreSQL server. There is no central PostgreSQL administrative program. MySQL, by contrast, has a central mysqladmin program that handles most functions having to do with server startup and shutdown, as well as the creation and destruction of databases. The creation and management of users is handled by manipulating tables in the mysql database.

PostgreSQL’s counterparts to the mysql database are special system tables and views, all of which begin with the pg_ prefix. These tables, although necessary for the system to run, easily can be ignored by most programmers and come into play only when trying to tune the system or figure out how to optimize queries.

GUI-based administration tools are available for both programs, as well as Web-based tools written in PHP. To be honest, I haven’t used these two much during the years, given my familiarity with (and preference for) command-line systems for working with databases. However, my experience with both sets of GUI programs has been positive, and my impression is that they are both stable and secure, as well as useful.

Another aspect of administration unique to PostgreSQL is the need to “vacuum” dead rows from the database to return them to the operating system or to other rows that could benefit from the space. In addition, PostgreSQL’s vacuum function visits the rows of the dead and uses the statistics it collects to inform the optimizer and query planner. Nowadays, the auto-vacuum daemon takes care of this automatically for most people, removing the long-dreaded need to schedule it in cron.

One administrative area that is particularly hot right now is replication. Many Web sites and other applications are pushing the limits of their database servers, and it would be useful to split the work among multiple servers. Of course, this raises issues of data integrity and synchronization among distributed processes. The simple solution to the problem is to have a master/slave relationship among the different servers, with UPDATEs and INSERTs taking place only on the master server, and SELECTs taking place on the slave servers. Solutions for this exist under both MySQL and PostgreSQL, although the PostgreSQL solution (Slony) is external to the standard package and apparently can be difficult to install and configure.

A more complicated setup involves the use of two master database servers. MySQL appears to have taken the lead on this front with a relatively new clustering tool. But, PostgreSQL users, who have been clamoring for such tools for several years now, appear to be on the verge of getting their wishes fulfilled.

Finally, no database server would be worthwhile if it weren’t possible to perform regular backups. pg_dump and mysqldump are command-line programs that turn the current contents of a database into a text file. Such dump files are quite useful and can be used to rebuild the database when necessary.

I would argue that when it comes to administration, the two database servers are identical—unless you need replication, in which case I’d probably benefit from MySQL’s greater experience and replication integration.

## Performance

For years, one of the claims made in the MySQL/PostgreSQL flame war has had to do with speed. MySQL fans often have claimed that their system is faster, particularly for read-only tasks, making it a superior choice for Web sites where most data is read. PostgreSQL advocates, in contrast, claim that their system holds up to big loads much better than MySQL.

I haven’t conducted any benchmarks of my own, but my reluctance to do so is an admission that I am unqualified to create a good benchmark, and not that I believe the two systems are identical or that performance isn't important. Moreover, as I stated previously, I believe that performance is secondary to data integrity. I would much rather have a slow, reliable database than a fast one that occasionally will wreak havoc on my data.

From the benchmarks I've seen, it appears that MySQL is indeed faster than PostgreSQL when working with a small number of clients or with read-only data. However, all of the comparisons I've seen over the last few years indicate that as more clients are added to the system, PostgreSQL handles the load better.

Does this mean that PostgreSQL always will be faster? Of course not. But, it does mean that on particularly popular sites, PostgreSQL may hold up better.

Maybe I'm simply naive, but I decided several years ago that I would largely ignore the performance debate when it came to databases. Both MySQL and PostgreSQL have large followings and have been used on large-scale systems. The data seems to indicate that PostgreSQL has an advantage, but enough people are using MySQL on large Web sites that I have to assume it is working well enough for them.

### Resources

The PostgreSQL home page is **www.postgresql.org**. Similarly, the MySQL home page is **www.mysql.org**. Each has its latest manuals posted, as well as software, drivers and discussion lists.

A table comparing administration and programming of the two databases is available at **linuxboxadmin.com/articles/postgresql-for-mysql-users.php**.

A relatively recent comparison of the two databases’ performance is at **www.mysqlperformanceblog.com/2006/11/30/interesting-mysql-and-postgresql-benchmarks**, which points to the following: **tweakers.net/reviews/657**.

Finally, a comparison between the databases (but perhaps a bit out of date), along with Oracle, was conducted at CERN, the European center for particle physics, and is available at **dccdbpilot.cern.ch:8080/dcdb/archive/trace2y/db_compare/db_compare.html**.

### Support

Finally, no comparison would be complete without mentioning support. We might consider several types of support—from the strength of the Open Source community to the number and quality of companies supporting (and developing) the software to the number of third-party applications that support each database.

It is impossible to ignore the extremely large number of MySQL users in the world. This has led to an outpouring of books, tutorials and mailing lists for MySQL—some (but not all) of which have been sponsored by the MySQL company itself. If the community-based support is not enough, it is possible to buy commercial support for MySQL from a number of companies, including MySQL AB.

PostgreSQL has a smaller community, and a smaller number of books and tutorials available. However, my experience has been that the community is responsive to questions and suggestions, and that the lead developers often are quite willing to answer questions from all levels of users.

Many open-source packages support both MySQL and PostgreSQL, but it is rare to find a package that supports PostgreSQL exclusively, and it is easy to find packages that support MySQL alone. This has been a source of some frustration for members of the PostgreSQL community; however, there doesn't seem to be much anyone can do about it, short of asking for patches or contributing such patches.

A recent thread on the main PostgreSQL mailing list asked about CRM packages that support the database. Although there were a few, there was definitely some grumbling about the lack of PostgreSQL from other open-source projects. Those projects often are staffed by small groups of volunteers who rarely understand how they can make their SQL more portable and thus easier to use on multiple brands of databases.

The bottom line on support is that although PostgreSQL support is excellent, MySQL support is overwhelming. If there is a winner here, it's MySQL.

### Conclusions

So, should you pick MySQL or PostgreSQL for your next database task? All things being equal, I strongly recommend PostgreSQL. Its community might be smaller, and there are fewer resources available in print and on the Web. But, it has more features to ensure data integrity, its features are largely a superset of MySQL, and it always offers transactions and referential integrity, without having to specify a particular type of table.

That said, there are reasons to use MySQL: if you already are using it, if you need commercial or community support, if you need replication, or if you are using software that is incompatible with PostgreSQL, MySQL is a fine choice. Just make sure to use InnoDB tables, so that you can take advantage of what a database always was meant to do—ensure the quality of the data.

Reuven M. Lerner, a longtime Web/database consultant, is a PhD Candidate in Learning Sciences at Northwestern University in Evanston, Illinois. He currently lives with his wife and three children in Skokie, Illinois. You can read his Weblog at althedotnerd.co.il.

![](img/526fd434dcfcf1b461b94c24ea170f36_46_0.png)
