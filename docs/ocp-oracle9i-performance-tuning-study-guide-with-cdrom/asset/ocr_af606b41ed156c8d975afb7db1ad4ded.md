Table 4.4 describes the values that can be assigned to the `CURSOR_SHARING` parameter.

# **TABLE 4.4** Values for `CURSOR_SHARING` Parameter


| **Value** | **Description** |
| :--- | :--- |
| **FORCE** | Allows two SQL statements, which differ only by a literal value, to share parsed code cached in the Shared Pool. The difference in the literal values must not change the meaning of the statement. This value was introduced in Oracle8i. |
| **SIMILAR** | Allows two SQL statements, which differ only by a literal value, to share parsed code cached in the Shared Pool. The difference in the literal values must not change the meaning of the statement or its cached execution plan. This value is new in Oracle9i. |
| **EXACT** | Two SQL statements must match exactly in order to share the parsed code cached in the Shared Pool. This is the default value for `CURSOR_SHARING`. |


For example, suppose application user Bob issues the following SQL statement:

```
SQL> SELECT order_id, customer_id FROM orders WHERE
order_id = 1001;
```

This SQL statement would be parsed and stored in the Shared Pool using the process described earlier in the chapter. Now, suppose application user Linda issues the following SQL statement:

```
SQL> SELECT order_id, customer_id FROM orders WHERE
order_id = 1299;
```

Because these two statements are not identical, Linda would not have a cache hit on the Shared Pool and would instead have to parse her statement. However, these two statements are essentially identical with the exception of the literal values for `order_id` (i.e., 1001 in Bob’s query and 1299 in Linda’s query). By setting `CURSOR_SHARING` to a value of `SIMILAR` or `FORCE`, Oracle would consider these two similar SQL statements to be identical.