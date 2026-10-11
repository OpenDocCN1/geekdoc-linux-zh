can store text inside of TEXT columns in your tables, and then identify the column (and retrieve the text) without having to index it yourself.
If the included suite of functions doesn't suit your needs, you can always write one of your own. Recent versions of MySQL also offer the ability to create a stored procedure or function, which provides both increased speed and centralized control over commonly used functions. Stored procedures also can be invoked automatically when particular events occur, known as a trigger in database parlance. You also can write new functions in C or C++, loading them into MySQL at runtime.

# ### Table Types

So far, MySQL sounds like a nice, flexible relational database. You might be surprised, however, to find that there is a huge amount of pent-up frustration, and even hostility, toward MySQL in the Open Source and Database communities. Just look for a recent story on Slashdot about MySQL, and you will see many comments indicating that PostgreSQL, Firebird or nearly any other option would be a better solution.

Part of this stems from a time-honored tradition of rivalry in the computer world, and particularly in the Open Source community. Over the years, we have seen fights between Emacs and vi, Perl and Python, Linux and BSD, and countless other pairings.

But, part of the animosity toward MySQL stems from several design decisions that the authors made early on. For example, documentation for an old version of MySQL said that foreign keys are really unnecessary, and that such integrity checks could (and should) be handled in the application, rather than in the database. Many experienced database people see this and don't know whether to laugh or cry. The primary reason for using a database is for its reliability, not speed, and adding foreign-key checks is an easy way to increase the reliability of inserted data.

Similarly, old versions of MySQL failed to lock tables. If you wanted to be sure that no one would write to a table from which you were reading (or to which you were writing), you needed to lock the table explicitly at the application layer. Given the many years of research that has gone into row-level locking (and even more-advanced systems, such as multiversion concurrency control), this seemed to many like a step backward. MySQL's solution to these problems has been a novel one. Rather than add these features to the existing (MyISAM) table structure, it made it possible to choose from a number of different table structures, each with its own set of trade-offs. Much as Linux system administrators can choose from a variety of filesystems, MySQL administrators and programmers can choose from several different storage engines.

This approach has some problems, of course. The biggest problem from my perspective is that MyISAM remains the default storage engine, which means that many users effectively choose to go without foreign keys and sophisticated locking due to ignorance. Many other storage engines seem to be of more limited use or for particular applications, such as MEMORY (for in-memory databases), BDB (Berkeley DB-based) tables and even FEDERATED (for tables on remote servers).

A very popular storage engine, InnoDB, has a different problem associated with it---the company that develops InnoDB was purchased by Oracle earlier this year. This may have no effect on MySQL's open-source distribution, because Oracle continues to make InnoDB available under the GPL. But, it has raised some questions regarding MySQL's commercial version, given that an essential part of the commercial-grade toolbox is now owned by a major database rival.

Much has been made about MySQL's fast performance over the years, with little or no tuning of the server. The truth is a bit hazier than that, although MySQL is undoubtedly a fast database, many of those tests were made using MyISAM tables, which are inherently faster because of their lack of locks and integrity checks. (As an analogy, I often say that it's faster to leave your house without locking the door, but the extra speed is usually not worth the risk.)

# ### Scalability

Many of the features in recent versions of MySQL have been aimed at corporate customers, whose license purchases are helping drive MySQL development forward. One of the biggest bottlenecks that a database administrator can face, particularly as the data grows in size, is disk speed. Recent versions of MySQL thus provide both tablespaces (that is, allocation of disk space on a per-table basis) and partitions (that is, division of a table across several filesystems). Tablespaces are available only with InnoDB tables, but partitions are available for all storage engines. Moreover, tables can be partitioned based on column values, using a hash function to decide into which partition a particular row should be placed.
Another important aspect of MySQL has been replication and backup. These are crucial features for enterprise clients, who need their data to be available all the time and to have backups available at a moment's notice. The latest mode of MySQL has improved the replication engine and made it more flexible, making it possible to replicate tables even on a per-row basis.
Another feature I have been waiting to see for some time is Unicode support. Although not all string and regexp operations work with Unicode, this is a big boon to those who work with multiple languages.

# ## Perhaps the biggest asset that MySQL has going for it is a very large, very active community of users and developers.

# ### Community

Perhaps the biggest asset that MySQL has going for it is a very large, very active community of users and developers. The sheer number of books, Web sites, mailing lists, help forums and code snippets for MySQL is overwhelming.
For its part, MySQL AB has been doing an admirable job of updating the documentation on a regular basis and of moving forward with new features at an impressive rate. (This demonstrates that although open-source software can often be written by volunteers, having paid professionals work on a project can speed it up immensely.) In particular, I am impressed by the on-line documentation, which includes not only numerous examples, but also intelligently placed links to related subjects.

# ### Conclusion

MySQL has grown up quite a bit since I first began to use it more than ten years ago. Some of its quirks, such as using MyISAM tables by default, continue to rankle serious database users who would like to see transactions and foreign keys everywhere. But, especially with versions 5.0 and 5.1, MySQL is looking like a database that can advertise its depth of serious features, rather than claim its main advantage is speed.

*Rauwen M. Lerner, a longtime Webdatabase consultant, is a PhD candidate in Learning Sciences at Northwestern University in Evanston, Illinois. He currently lives with his wife and three children in Skokie, Illinois. You can read his Weblog at allread.me/lerner.cu.*