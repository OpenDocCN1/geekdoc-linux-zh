```
(9)-- WHERE id = 100
```

# Listing 2.27 - An UPDATE using the TRANSFORM expression

In the above example, lines (1), (2), and (9) are part of the SQL UPDATE syntax. In Line (2) the XMLQUERY function is invoked, which calls the transform expression in line (4). The transform expression block goes from line (4) to line (8), and it is used to insert a new node into the XML document containing the **email2** element. Note that updating the elements in an XML document through a view is not supported.

Deleting entire XML documents from tables is as straightforward as when using the SELECT statement in SQL/XML. Use the SQL DELETE statement and specify any necessary WHERE predicates.

# 2.3.9 XML indexing

In an XML document, indexes can be created for elements, attributes, or for values (text nodes). Below are some examples. Assume the table below was created:

```
CREATE TABLE customer(info XML)
```

And assume the XML document in Listing 2.28 is one of the documents stored in the table.

```
<customerinfo Cid="1004">
    <name>Matt Foreman</name>
    <addr country="Canada">
        <street>1596 Baseline</street>
        <city>Toronto</city>
        <state>Ontario</state>
        <pcode>M3Z-5H9</pcode>
    </addr>
    <phone type="work">905-555-4789</phone>
    <phone type="home">416-555-3376</phone>
    <assistant>
        <name>Peter Smith</name>
        <phone type="home">416-555-3426</phone>
    </assistant>
</customerinfo>
```

# Listing 2.28 - The XML document to use in the examples related to XML indexes

The statement shown in *Listing 2.29* creates an index on the attribute **cid**.

```
CREATE UNIQUE INDEX idx1 ON customer(info)
    GENERATE KEY USING
    xmlpattern '/customerinfo/@Cid'
    AS sql DOUBLE
```

# Listing 2.29 - An index on attribute Cid

The statement shown in *Listing 2.30* creates an index on the element **name**.