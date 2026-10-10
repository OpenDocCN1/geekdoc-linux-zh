
## 2.3.8 The TRANSFORM Expression

**copy clause**

```
|--copy--$VariableName--:=--CopySourceExpression--|
```

**modify clause**

```
|--modify--ModifyExpression--------------------|
```

**return clause**

```
|--return--ReturnExpression--------------------|
```

**Listing 2.26 - The syntax of the TRANSFORM expression**

The copy clause is used to assign to a variable the XML documents you want to process.

In the modify clause, you can invoke an insert, delete, rename, or replace expression. These expressions allow you to perform updates to your XML document.

For example:

- If you want to add new nodes to the document, you would use the insert expression.
- To delete nodes from an XML document, use the delete expression.
- To rename an element or attribute in the XML document, use the rename expression.
- To replace an existing node with a new node or sequence of nodes, use the replace expression. The replace value of the expression can only be used to change the value of an element or attribute.

The return clause returns the result of the transform expression.

*Listing 2.27* shows an example of an UPDATE statement using the TRANSFORM expression.

```sql
(1)-- UPDATE customers
(2)-- SET contactinfo = xmlquery( 'declare default element namespace
(3)--                          "http://posample.org";
(4)--                     transform
(5)--          copy $newinfo := $c
(6)--                 modify do insert <email2>my2email.gm.com</email2>
(7)--                      as last into $newinfo/customerinfo
(8)--          return $newinfo' passing contactinfo as "c")
(9)-- WHERE id = 100
```

**Listing 2.27 - An UPDATE using the TRANSFORM expression**

In the above example, lines (1), (2), and (9) are part of the SQL UPDATE syntax. In line (2), the XMLQUERY function is invoked, which calls the transform expression in line (4). The transform expression block goes from line (4) to line (8), and it is used to insert a new node into the XML document containing the **email2** element. Note that updating the elements in an XML document through a view is not supported.

Deleting entire XML documents from tables is as straightforward as when using the SELECT statement in SQL/XML. Use the SQL DELETE statement and specify any necessary WHERE predicates.

## 2.3.9 XML indexing

In an XML document, indexes can be created for elements, attributes, or for values (text nodes). Below are some examples. Assume the table below was created:

```sql
CREATE TABLE customer(info XML)
```

And assume the XML document in Listing 2.28 is one of the documents stored in the table.

```xml
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

**Listing 2.28 - The XML document to use in the examples related to XML indexes**

The statement shown in *Listing 2.29* creates an index on the attribute **cid**.

```sql
CREATE UNIQUE INDEX idx1 ON customer(info)
    GENERATE KEY USING
    xmlpattern '/customerinfo/@Cid'
    AS sql DOUBLE
```

**Listing 2.29 - An index on attribute Cid**

The statement shown in *Listing 2.30* creates an index on the element **name**.

```sql
CREATE INDEX idx2 ON customer(info)
    GENERATE KEY USING
        xmlpattern '/customerinfo/name'
        AS sql VARCHAR(40)
```

**Listing 2.30 - An index on element name**

The statement in *Listing 2.31* creates an index on all elements *name*.

```sql
CREATE INDEX idx3 ON customer(info)
    GENERATE KEY USING
        xmlpattern '//name'
        AS sql VARCHAR(40);
```

**Listing 2.31 - An index on all elements name**

The statement in *Listing 2.32* creates an index on all text nodes (all values). This is not recommended, as it would be too expensive to maintain the index for update, delete and insert operations, and the index would be too large.

```sql
CREATE INDEX idx4 ON customer(info)
    GENERATE KEY USING
        xmlpattern '//text()'
        AS sql VARCHAR(40);
```

**Listing 2.32 - An index on all text nodes (Not recommended)**

## 2.4 Working with XML Schemas

DB2 allows you to insert an XML document into the database if it is well-formed. If it’s not, you will receive an error at insertion time. On the other hand, DB2 does not force you to validate a XML document. If you wish to have an XML document validated, you have several alternatives as we will discuss in this section.

### 2.4.1 Registering your XML Schemas

XML Schemas are stored in the DB2 databases in what is called an XML Schema repository. To add an XML Schema to a repository, you use the REGISTER XMLSCHEMA command.

For example, let’s say you have an XML document stored in file *order.xml* as shown in *Figure 2.10*.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<po:PurchaseOrder xmlns:po="http://www.test.com/po">
    <Header>
        <Id>1</Id>
        <date>2004-01-29</date>
        <description>purchase order</description>
        <value>20</value>
        <status>shipped</status>
    </Header>
    <Items>
        <Item>
            <ItemDescription color="red" weight="5">
                <Name>Widget C</Name>
                <SKU>1</SKU>
                <Price>50</Price>
                <Comment>no comment</Comment>
            </ItemDescription>
            <NumberOrdered>1</NumberOrdered>
        </Item>
    </Items>
    <Customer type="regular">
        <Name>Manoj K Sardana</Name>
        <Address>ring road, bangalore</Address>
        <Phone>918051055109</Phone>
        <email>msardana@in.ibm.com</email>
    </Customer>
</po:PurchaseOrder>
```

**Figure 2.10 - The order.xml file containing an XML document**

Now, let’s say you have an XML Schema document stored in file order.xsd as shown in Figure 2.11.

```xsd
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"    
        targetNamespace="http://www.test.com/po" 
          xmlns:po="http://www.test.com/po"
          xmlns:head="http://www.test.com/header"
          xmlns:prod = "http://www.test.com/product" 
          xmlns:cust = "http://www.test.com/customer">

<xsd:import namespace="http://www.test.com/product" schemaLocation="product.xsd"/>
<xsd:import namespace="http://www.test.com/customer" schemaLocation="customer.xsd" />
<xsd:import namespace="http://www.test.com/header" schemaLocation="header.xsd" />

<xsd:complexType name="itemType">
  <xsd:sequence>
    <xsd:element name="Item" minOccurs="1" maxOccurs="unbounded" >
        <xsd:complexType>
          <xsd:sequence>
            <xsd:element name="ItemDescription" type="prod:prodType" />
            <xsd:element name="NumberOrdered" type="xsd:integer" />
          </xsd:sequence>
        </xsd:complexType>
    </xsd:element>
  </xsd:sequence>
</xsd:complexType>

<xsd:complexType name="potype">
  <xsd:sequence>
    <xsd:element name="Header"    type="head:headerType" />
    <xsd:element name="Items"     type="po:itemType" />
    <xsd:element name="Customer"  type="cust:customerType" />
  </xsd:sequence>
</xsd:complexType>

<xsd:element name="PurchaseOrder" type="po:potype" />

</xsd:schema>
```

**Figure 2.11 - The order.xsd file containing an XML schema**

In this XML Schema document we highlight with an ellipse the following:

- `<xsd:schema ...>`: Indicates it’s a XML Schema document.
- `<xsd:import ...>`: We import other xsd files (other XML Schemas) that would be part of this bigger XML Schema.
- `minOccurs="1"`: An example of an XML Schema “rule”, where for element Item we say that it should occur at least one time, or in other words, there should be at least one Item element.

Next, in order to register the XML Schema to the database, a script similar to the one shown in Listing 2.33 below could be used. The script includes comments that make it self-explanatory.

```sql
-- CONNECT TO THE DATABASE
CONNECT TO SAMPLE;

-- REGISTER THE MAIN XML SCHEMA
REGISTER XMLSCHEMA http://www.test.com/order FROM D:\example3\order.xsd AS
```
