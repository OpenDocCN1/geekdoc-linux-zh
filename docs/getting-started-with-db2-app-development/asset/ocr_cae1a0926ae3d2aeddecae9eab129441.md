Host variables follow normal Java variable syntax. Some data types that map to database data types in Java applications can be seen in *Figure 4.5* extracted from the DB2 Information Center.

| **Java data type** | **Database data type** |
| :--- | :--- |
| short | SMALLINT |
| boolean1 , byte , java.lang.Boolean | SMALLINT |
| int, java.lang.Integer | INTEGER |
| long, java.lang.Long | BIGINT 2 |
| float, java.lang.Float | REAL |
| double, java.lang.Double | DOUBLE |
| java.math.BigDecimal | DECIMAL(p,s) 2 |
| java.math.BigDecimal | DECFLOAT(n) 3,4 |
| java.lang.String | CHAR(n) 5 |
| java.lang.String | GRAPHIC(m) 5 |
| java.lang.String | VARCHAR(n) 7 |
| java.lang.String | VARGRAPHIC(n) 6,8 |

**Figure 4.5 - Mapping of Java data types with DB2 data types**

The full mapping list can be found at:
[http://publib.boulder.ibm.com/infocenter/db2luw/v9r7/topic/com.ibm.db2.luw.apdv.java.doc/doc/rjv4data.html](http://publib.boulder.ibm.com/infocenter/db2luw/v9r7/topic/com.ibm.db2.luw.apdv.java.doc/doc/rjv4data.html)

The **DCLGEN** (Declarations generator) utility in DB2 allows you to create structures for host variables. The languages supported are C, Java, COBOL, and FORTRAN.

For example, to generate the declaration statements for the table *employee* in the **SAMPLE** database for the Java language you can use:

```
db2dclgen -D sample -T employee -L Java
```

The output would be stored in a file *employee.java* with content as shown in *Listing 4.3* below.

```
``
java.sql.Date        hiredate;
java.lang.String      job;
short                 edlevel;
java.lang.String      sex;
java.sql.Date         birthdate;
java.math.BigDecimal  salary;
```

Listing 4.3 - Output of DCLGEN for the employee table using the Java language
```

# 4.3.2.2 The Statement interface