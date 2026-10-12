Or perhaps, you want a listing of all the mileages for cars older than the 2001 model year:

```
SELECT mileage, modelyear FROM Used_Vehicles WHERE modelyear < 2001;
```

Running this query shows the following:

| +---------------------------------------------------------------+
| | mileage | modelyear |
| +---------------------------------------------------------------+
| |     64800 |    2000 |
| |    152000 |    1993 |
| +---------------------------------------------------------------+ |

Simple enough, but what if you spotted an error, and wanted to change an existing record?

# Updating Information

To update information you use the UPDATE statement. The generic form of an UPDATE statement looks like this:

```
UPDATE [table] SET [column]= (value) WHERE [criteria]
```

Returning to the vehicle inventory example, say that one day the manager of the car lot was out looking through the inventory, and noticed the mileage was incorrectly recorded for one of the vehicles. To change it to the proper value, you might use the following query:

```
UPDATE Used_Vehicles SET mileage=66000 WHERE vehicle_id=1;
```

In this case, the vehicle ID of 1 corresponds to the automatically incremented ID assigned to the used Ford Explorer you added in a previous INSERT statement.

# Removing Information

Sales are starting to increase at the hypothetical car lot, and some recent sales require the removal of some vehicles from your database. In this situation, you will use the DELETE statement:

```
DELETE FROM [table] WHERE [criteria];
```

That used Ford Explorer that had its incorrect mileage fixed in the previous example sold today. To remove it from the Used_Vehicles table, you would simply do the following:

```
DELETE FROM Used_Vehicles WHERE vehicle_id=1;
```

That should cover the basics of MySQL usage, so it's time to move on to more powerful queries.

# Querying Multiple Tables

You've got your vehicle inventory set up, and you can use the basics to perform simple queries against one table at a time. But you'd like to see a little more—maybe even a query that links the make and model of each car to its individual record. For this, you'd use joins.