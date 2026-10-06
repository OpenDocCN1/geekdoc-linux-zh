```
sqlite .mode column
sqlite .header off
sqlite SELECT 'String 1', 'String 2';
string 1 string 2
```

As we saw before, SELECT can produce calculated values.

```
sqlite>.header on
sqlite SELECT 2 + 2;
2 + 2
$
SELECT COUNT(file), AVG(size_bytes) FROM Package_Files;
count(file) avg(size_bytes)
-------------------------------------------
153506 33370.3488658424
```

To make complicated expressions more readable, we can assign their results by aliases using the AS clause.

```
SELECT COUNT(file) AS Files,
...> AVG(size_bytes) AS 'Average Size'
... FROM Package_Files;
... Average Size
-------------------------------------------
153506 33370.3488658424
```

An important feature of SELECT is ability to produce results by combining data from multiple tables. This process is done by performing joins and subqueries. joins a little later, but now let's count on subqueries. SELECT allows us to include another SELECT statement as an output. To demonstrate this, we produce a table that includes columns for package name, number of files in the package, and the total size of the package. The SELECT statement to do this is rather formidable. We will open our text editor and create a file named subquery_demol.sql with the following:

```
-- subquery_demol.sql

-- Query to list 20 packages with the greatest number of files

.mode column
.header on
.width 20 40 10 10
SELECT package_name, description,
(SELECT COUNT(file)
    FROM Package_Files
    WHERE Package_Descriptions.package_name = Package_Files.package_name),
    (SELECT SUM(size_bytes)
    FROM Package_Files
    WHERE Package_Descriptions.package_name = Package_Files.package_name)
AS size
FROM Package_Descriptions ORDER BY files DESC LIMIT 20;
```

We'll run this query and view the results.

```
me@linuxbox:~/adventure-sql$ sqlite3 adv-sql.sql < subquery_demol.sql
package_name description size
-----------------------------------------------------------
```

# 230 SQL