Thus, depending on your background, if you are an SQL person you may see DB2 as a world class RDBMS that also supports XML. If you are an XML person, you would see DB2 as a world class XML repository that also supports SQL.

Note that IBM uses the term *pureXML* instead of *native XML* to describe this technology. While other vendors still use the old technologies of CLOB/varchar or shredding to store XML documents, they call those old technologies “native XML”. To avoid confusion, IBM decided to use the new term pureXML, and to trademark this name so that no other database or XML vendor could use this same term to denote some differing technology. pureXML support is provided for databases created as Unicode or non-Unicode.

# ## 2.3.1 pureXML technology advantages

Many advantages are provided by pureXML technology.

+   1.  You can seamlessly leverage your relational investment, given that XML documents are stored in columns of tables using the new XML data type.
+   2.  You can reduce code complexity. For example, Figure 2.5 illustrates a PHP script written with and without using pureXML. Using pureXML (the smaller box on the left side) the lines of code are reduced. This not only means that the code is less complex, but the overall performance is improved as there are fewer lines to parse and maintain in the code.

![](bbox=[0.22, 0.52, 0.94, 0.8])

Figure 2.5 – Code complexity with and without pureXML