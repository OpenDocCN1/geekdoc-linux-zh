# Chapter 4

```
SELECT ma.make_name, mo.model_name, n.color, n.modelyear FROM Makes ma, Models mo, New_Vehicles n WHERE ma.make_id = mo.make_id AND mo.model_id = n.model_id;
```

Execute this query in your MySQL client, and it returns the following:

+-------------+-------------+------------------------+-------------+  
| make_name | model_name | color | modelyear |  
+-------------+-------------+------------------------+-------------+  
| Ford | Explorer | Dark Blue | 2005 |  
| Toyota | Tacoma | Radiant Red | 2005 |  
| Chevrolet | Corvette | Daytona Sunset Orange Metallic | 2005 |  
+-------------+-------------+------------------------+-------------+

As you can see, the exact same results were returned as when you used an explicit inner join. What would have happened if you had left off the items in the `WHERE` clause? Try out this query:

```
SELECT mo.model_name, n.color, n.modelyear FROM Models mo, New_Vehicles n;
```

Running this query against our vehicle inventory produces the following (note that the `Makes` table has been excluded):

+-------------+------------------------------------+-------------+  
| model_name | color | modelyear |  
+-------------+------------------------------------+-------------+  
| Accord | Dark Blue | 2005 |  
| Golf | Dark Blue | 2005 |  
| Tacoma | Dark Blue | 2005 |  
| Corvette | Dark Blue | 2005 |  
| Explorer | Dark Blue | 2005 |  
| Accord | Graphite Pearl | 2004 |  
| Golf | Graphite Pearl | 2004 |  
| Tacoma | Graphite Pearl | 2004 |  
| Corvette | Graphite Pearl | 2004 |  
| Explorer | Graphite Pearl | 2004 |  
| Accord | Radiant Red | 2005 |  
| Golf | Radiant Red | 2005 |  
| Tacoma | Radiant Red | 2005 |  
| Corvette | Radiant Red | 2005 |  
| Explorer | Radiant Red | 2005 |  
| Accord | Daytona Sunset Orange Metallic | 2005 |  
| Golf | Daytona Sunset Orange Metallic | 2005 |  
| Tacoma | Daytona Sunset Orange Metallic | 2005 |  
| Corvette | Daytona Sunset Orange Metallic | 2005 |  
| Explorer | Daytona Sunset Orange Metallic | 2005 |  
| Accord | Dark Blue | 2005 |  
| Golf | Dark Blue | 2005 |  
| Tacoma | Dark Blue | 2005 |  
| Corvette | Dark Blue | 2005 |  
| Explorer | Dark Blue | 2005 |  
+-------------+------------------------------------+-------------+