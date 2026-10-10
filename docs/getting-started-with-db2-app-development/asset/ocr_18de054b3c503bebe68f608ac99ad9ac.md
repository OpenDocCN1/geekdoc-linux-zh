+   4. After successfully running the script, use the DB2 Control Center, or IBM Data Studio to verify that the **items** and **clients** tables are created and that they contain 4 and 7 rows respectively.

+   5. With the **mydb** database created and with the two tables loaded, you can now connect to it, and perform the queries shown in *Listings 2.7 through 2.19*

# 2.6 Summary

This chapter introduced you to XML and pureXML technology. XML document usage is growing exponentially due to Web 2.0 tools and techniques as well as SOA. By storing XML documents in a DB2 database you can take advantage of security, performance, and coding flexibility using pureXML. pureXML is a technology that allows you to store the XML documents in parsed-hierarchical format, as a tree, and this is done at database insertion time. At query time, there is no need to parse the XML document in order to build a tree before processing. The tree for the XML document was already built and stored in the database. In addition, pureXML technology uses a native XML engine that understands XQuery; therefore, there is no need to map XQuery to SQL which is what is done in other RDBMS products.

The chapter also talked about how to insert, delete, update and query XML documents using SQL/XML and XQuery. It also discussed XML indexes, XML Schema, and other features such as compression and XML Schema evolution.

# 2.7 Review questions

+   1. Why is it a good idea to store XML documents in a database as opposed to files?

+   2. What are the two types of databases for storing XML data?

+   3. What are the two main characteristics of pureXML?

+   4. Why would using pureXML be better for application performance?

+   5. How can you insert an XML document into a DB2 database?

+   6. Which of the following can be used to retrieve XML data in DB2?
+   A. SQL
+   B. SQL/XML
+   C. XQuery
+   D. B and C
+   E. All of the above

+   7. Which of the following is not a SQL/XML function?
+   A. XMLQUERY