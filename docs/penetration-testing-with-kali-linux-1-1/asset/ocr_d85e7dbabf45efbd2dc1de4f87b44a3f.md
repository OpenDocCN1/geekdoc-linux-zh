Again, the payload can by inserted into the **wp_sap** cookie value. As before, the value of the cookie starts after the "= " sign and ends with a semicolon.

![](bbox=[0.14, 0.18, 0.87, 0.55])

Figure 327: Querying for All Tables

The result includes a large list of tables, but the one that stands out to us most is **wp_users**, since it will most likely contain the WordPress user information.

Now that we have the table name, we can work on retrieving its column names. To do this, we query the **column_name** column within **information_schema.columns**, limiting the result to those where the table is **wp_users**. This can be done by updating our payload as shown in Listing 868.

```
"1569149780") OR 1=2 UNION SELECT 1,2,3,4,5,6,7,8,9,column_name,11 FROM information_schema.columns WHERE table_name='wp_users'#"
```

Listing 868 - List of all columns in the **wp_users** table