# How Does a Schema Differ from a DTD?

Three main data types for holding text are built in to XML Schema:

+   - string
- CDATA
- token

If you're familiar with programming, you know that a string is a group of alphanumeric characters. The CDATA data type is already familiar because even the DTD supports that data type. The token data type handles character data but is more restrictive than the string and CDATA data types. A token cannot hold two or more spaces in a row, or carriage feeds or tab characters.

> Without getting bogged down in details, it might be of interest to note that the token data type is derived from the CDATA data type, but it is defined by its restrictions. In other words, the token data type is a subset of the CDATA data type. Many of the built-in Schema data types are derived from other data types but are more restrictive about what they may contain. The original data type is known as a primitive data type.

![](bbox=[0.815, 0.423, 0.915, 0.493])

NOTE

# Numeric Data Types

The Schema specification allows for a number of numeric data types:

+   - decimal
- float
- double
- binary
- integer
- nonPositiveInteger
- negativeInteger
- long
- int
- short
- byte
- unsignedbyte
- unsignedInt
- unsignedLong
- unsignedShort