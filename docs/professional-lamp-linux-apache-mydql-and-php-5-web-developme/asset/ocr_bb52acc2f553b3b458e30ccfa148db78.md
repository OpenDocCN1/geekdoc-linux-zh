```
************************* 2. row *************************
vehicle_id: 2
model_id: NULL
price: NULL
color: Graphite Pearl
description: Last of the 2004 stock! Must sell! Loaded, all options!
modelyear: 2004
************************* 3. row *************************
vehicle_id: 3
model_id: 4
price: NULL
color: Radiant Red
description: Come drive this popular truck! 4WD, extended cab, many options.
modelyear: 2005
************************* 4. row *************************
vehicle_id: 4
model_id: 5
price: NULL
color: Daytona Sunset Orange Metallic
description: The all new C6 Corvette, the next generation of classic American sports cars. 400HP V8; Very fast!
modelyear: 2005
```

# Converting Back to MyISAM from InnoDB

You’ve given InnoDB tables and foreign keys a whirl, but you’ve decided that you’d much rather have full-text searching instead. Changing back to MyISAM is a relatively painless process. Usually it will involve only two steps: removing any InnoDB-specific features, such as foreign keys, and changing the storage engine type back to MyISAM with ALTER TABLE. To convert the New_Vehicles table back to MyISAM, do the following:

```
ALTER TABLE New_Vehicles DROP FOREIGN KEY refmid1;
ALTER TABLE New_Vehicles ENGINE=MyISAM;
```

At this point, the New_Vehicles table is back to using the MyISAM storage engine and you once again have the ability to add and use full-text indexing on that table.

# Controlling Access

One of the most important jobs you’ll have as a MySQL database administrator is controlling who can access the system and what resources they can access. In most situations, you’ll need only a handful of user accounts for each database, and those that you do need to create should only be given the minimal access required to perform their task. Luckily, MySQL provides you with a handful of ways to control who has access to your systems and to what resources exactly.

# User Administration

In order to help control the user accounts in your database, MySQL provides a couple of ways to main- tain user accounts. Whether it’s an account for a co-developer, a tech-savvy client, or a web-based front end to the system, each user needs to have access specifically granted for the resources they require.