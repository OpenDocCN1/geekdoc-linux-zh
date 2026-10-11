+   - MongoDB databases
+   	- MongoDB client and tasks

# Relational databases

Relation databases is a popular solution for most of the applications that require to store structured data, such as Web applications or services. A relational database is based on a *relational model*. In this model, the data is organized into one or more tables. Each table will contain rows and columns. The rows are usually called *records*, and the columns *attributes*. Each row will contain several attributes and will have a unique key to identify each row. Refer to *figure 11.1*:

![](bbox=[0.15, 0.32, 0.85, 0.59])

*Figure 11.1: Relation between record and attributes*

Each column (*attribute*) will have assigned a name, a type of the data expected (for example, number or string), and the maximum size. A column will indicate if it is mandatory to introduce data and if it requires to be unique in the table. The data assigned in a column for a record is called *field*. The common columns types available are described in *table 11.1*:

| Type | Description |
| :--- | :--- |
| CHAR | Fixed width *n*-character string. |
| VARCHAR | Variable width string with a maximum size of *n* characters. |
| BOOLEAN | Can store values *TRUE* and *FALSE*. |
| INTEGER | Numerical types for integer numbers. |
| FLOAT / DOUBLE | Numerical types for floating point numbers. |