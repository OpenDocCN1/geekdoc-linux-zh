> **NOTE**
> 
> For both these connectivity packages, the examples describe queries being executed in *autocommit* mode, meaning that each query is sent to the database as soon as it is formulated (using `sdb->query` or `Sconn->exec`), and results are immediately available to `fetchrow` commands. Each package contains analogous commands that can be used to operate in a mode where queries are not automatically committed. This approach is often very useful for operations that must be *atomic* (that is, *treated as a single instruction that cannot be interrupted by other processes* that can potentially change the state of the database between the start and end of the operation). Atomic operations are considered much safer than nonatomic ones, and it’s good database coding practice to use them wherever possible. Refer to the per-IDC documentation for each package for details.

# Database Connectivity with Python

Python’s connectivity is built upon the Python Database API Specification 2.0. Apart from the details of the setup lines and how the connection itself is set up, the command syntax for accessing MySQL and PostgreSQL databases is exactly the same. First, build and install either the *py-MySQLdb* or the *py-pyPgSQL* ports, both in `/usr/ports/databases`, depending on which database you are using.

To set up a connection to a MySQL database, use the following initialization lines:

```
import MySQLdb
db = MySQLdb.connect(database="PictureArchive");
```

If you’re using PostgreSQL, the setup lines will look like this:

```
from pyPgSQL import PgSQL
db = PgSQL.connect(database="PictureArchive");
```

The preceding lines set up the connection to the database. Next, you can create a *cursor*, or statement handle, with the `db.cursor()` operator:

```
cur = db.cursor()
```

Now you can begin issuing queries. Python’s database API defaults to non-autocommit mode, so you can issue as many queries as you like before committing them, as shown here:

```
cur.execute ('INSERT INTO Users (FullName,Age) VALUES ('Joe Smith', '22')')
cur.execute ('INSERT INTO Users (FullName,Age) VALUES ('Alice Walker', '31')')
db.commit()
```