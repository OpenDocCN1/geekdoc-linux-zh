```
PictureArchive=# EXPLAIN SELECT Artists.Name, Pictures.name FROM Artists
LEFT JOIN Pictures ON Artists.ID=Pictures.Artist_ID;
NOTICE: QUERY PLAN:

Merge Join (cost=823.39..1012.89 rows=10000 width=32)
-> Index Scan using Artists_pkey on Artists (cost=0.00..52.00 rows=1000 width=16)
-> Sort (cost=823.39..823.39 rows=10000 width=16)
-> Seq Scan on Pictures (cost=0.00..159.00 rows=10000 width=16)
EXPLAIN
```

Here, you see a join being performed between the Artists and Pictures tables, but there is no key in Pictures to help the database engine search for the elements upon which to perform the join. Costs of each operation are summed upward; as you work your way up the tree, you can see the overall cost of the query increasing. The sequential scan and sort operation at the bottom of the tree is causing a significant hit on system performance. If you had an index on the Artist_ID key in Pictures, the database wouldn't have to do a sequential scan and could instead do an index scan, which is much faster, as shown in this example:

```
PictureArchive=# CREATE INDEX Pictures_Artist_ID_key ON Pictures ( Artist_ID );
CREATE
PictureArchive=# EXPLAIN SELECT Artists.Name, Pictures.Name FROM Artists
LEFT JOIN Pictures ON Artists.ID=Pictures.Artist_ID;
NOTICE: QUERY PLAN:

Merge Join (cost=0.00..628.56 rows=10000 width=32)
-> Index Scan using Artists_pkey on Artists (cost=0.00..52.00 rows=1000 width=16)
-> Index Scan using Pictures_Artist_ID_key on Pictures (cost=0.00..439.06 rows=10000 width=16)
EXPLAIN
```

Here, the overall cost range is reduced from 823.39 through 1012.89 down to to 0.00 through 628.56. (These units aren't very meaningful outside of the database context but can be compared internally very effectively.) It seems this maneuver has gained some very positive results.

# Creating Temporary Tables

This may not seem obvious at first blush, but sometimes it's more efficient to create a temporary table than to do a complex join. Programmatically, it may appear that the most