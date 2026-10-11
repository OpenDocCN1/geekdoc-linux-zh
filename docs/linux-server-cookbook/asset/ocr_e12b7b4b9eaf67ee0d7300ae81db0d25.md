```
test> db
 test
 test> show dbs
 admin 72.00 KiB
 config 72.00 KiB
 local 72.00 KiB
```

*Figure 11.36: Output example MongoDB*

It is possible to use another database with the syntax use **dbname**. If the **dbname** specified is not an existing database, a new one will be created. **MongoDB** stores documents in **collections**. These collections are analogous to tables in relation databases. If the **collection** indicated does not exist, it will be created. Figure 11.37 shows the creation of a new database and a new collection named *students* using the action **insertOne**.