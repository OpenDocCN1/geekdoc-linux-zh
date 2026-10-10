```
    order by $y/zip
    return <li>{$y}</li>
}
</ul>
```

# Listing 2.17 - XQuery statement with the FLWOR expression returning HTML

The sample HTML returned would look as shown in *Listing 2.18*.

```
<ul>
<li>
<address>
    <street>9407 Los Gatos Blvd.</street>
    <city>Los Gatos</city>
    <state>ca</state>
    <zip>95302</zip>
</address>
</li>
<address>
    <street>4209 El Camino Real</street>
    <city>Mountain View</city>
    <state>CA</state>
    <zip>95302</zip>
</address>
</li>
...
</ul>
```

# Listing 2.18 - Output of the query ran in Listing 2.17

# Example 4

The following example shows how to embed SQL within XQuery by using the **db2-fn:sqlquery** function. The **db2-fn:sqlquery** function executes an SQL query and returns only the selected XML data. The SQL query passed to **db2-fn:sqlquery** must only return XML data. This XML data can then be further processed by XQuery. This is illustrated in *Listing 2.19*.

```
xquery
    for $y in
        db2-fn:sqlquery(
            'select comments from items where srp > 100')
    /Comments/Comment
    where $y/ResponseRequested='Yes'
    return (
```