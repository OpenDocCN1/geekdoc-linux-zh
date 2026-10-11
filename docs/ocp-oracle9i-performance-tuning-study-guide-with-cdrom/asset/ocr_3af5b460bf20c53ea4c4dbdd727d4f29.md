**TABLE 3.19 Materialized View init.ora Parameters (continued)**
| Parameter | Description |
| :--- | :--- |
| QUERY_REWRITE_ | Determines the degree to which the data consistency is to be adhered to when accessing materialized views. Options are: ENFORCED: Query rewrites only occur when Oracle can guarantee data currencty (default); TRUSTED: Query rewrites can occur when declared relationships exist, but without complete data currency; STALE_TOLERATED: Query rewrites can occur even when the view's data and the underlying table data are not current. |
| OPTIMIZER_MODE | Must be set to one of the cost-based optimizer modes. |

The QUERY_REWRITE_ENABLED and QUERY_REWRITE_INTEGRITY parameters can also be set at the session level using the ALTER SESSION command. The system privilege GLOBAL QUERY REWRITE and/or QUERY REWRITE must be granted to users who wish to alter their session in this manner. There are also two SQL hints, REWRITE and NOREWRITE, which can also be used to turn on and off the dynamic rewriting of queries when using materialized views.

![](bbox=[0.17, 0.57, 0.26, 0.63])

Users need privileges only on the base tables underlying the materialized view in order to use it, not on the view itself.

# ### Creating Materialized Views

Once you have identified the SQL statements for which you would like to create materialized views, you are ready to build the materialized views. The sample code below shows how a materialized view would be built on the DISTRICT, DISTRIBUTOR, and EMPLOYEE tables:

```
SQL> CREATE MATERIALIZED VIEW EMP_BY_DISTRICT
2    TABLESPACE MVIEW_DATA
3    BUILD IMMEDIATE
4    REFRESH FAST
```