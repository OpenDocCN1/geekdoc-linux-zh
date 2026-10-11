```
mysql> SELECT * FROM y_table;
+-------+
| Y     |
+-------+
| 2068 |
| 2069 |
| 1999 |
| 0000 |
| 2000 |
+-------+
```

Observe that 00 is converted to 0000, not to 2000. That's because, as a number, 00 is the same as 0, and is a perfectly legal value for the YEAR type. If you insert a numeric zero, that's what you get. To get 2000 using a value that does not contain the century, insert the string '0' or '00'. You can make sure that MySQL sees a string and not a number by inserting YEAR values using CAST(value AS CHAR) to produce a string result uniformly regardless of whether value is a string or a number.

Keep in mind that the rules for converting two-digit to four-digit year values provide only a reasonable guess. There is no way for MySQL to be certain about the meaning of a two-digit year when the century is unspecified. MySQL's conversion rules are adequate for many situations, but if they don't produce the values that you want, it is necessary to provide unambiguous data with four-digit years. For example, to enter birth and death dates into the president table, which lists U.S. presidents back into the 1700s, four-digit year values are in order. Values in these columns span several centuries, so letting MySQL guess the century from a two-digit year is definitely the wrong thing to do.

# 3.2.7 Spatial Data Types

Spatial values enable representation of values such as points, lines, and polygons. These data types are implemented per the OpenGIS specification, which is available at the Open Geospatial Consortium Web site (http://www.opengis.net/). Table 3.17 lists the spatial data types that MySQL supports.

Table 3.17 Spatial Data Types

| Type Name | Meaning |
| :--- | :--- |
| GEOMETRY | A spatial value of any type |
| POINT | A point (a pair of X,Y coordinates) |
| LINESTRING | A curve (one or more POINT values) |
| POLYGON | A polygon |
| GEOMETRYCOLLECTION | A collection of GEOMETRY values |
| MULTILINESTRING | A collection of LINESTRING values |
| MULTIPOINT | A collection of POINT values |
| MULTIPOLYGON | A collection of POLYGON values |