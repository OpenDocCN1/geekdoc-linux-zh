![](bbox=[0.13, 0.11, 0.23, 0.2])

All index-organized tables must have a primary key constraint defined on the column that will be the basis of the index. An IOT cannot contain unique constraints or be clustered. Clusterering is discussed in a subsequent section.

The important parts of the CREATE TABLE syntax that are related to IOT creation are summarized in Table 3.22.

# **TABLE 3.22** Syntax for Index IOT Creation

| Clause | Description |
| :--- | :--- |
| ORGANIZATION INDEX | Specifies that this table is an IOT. |
| PCTTHRESHOLD | Specifies what percentage of the entire data block to hold open in order to store the row data associated with a primary key value, which must be between 0 and 50 (default 50). |
| INCLUDING | Specifies at which column to break a row into two pieces when a row's length exceeds the size set aside in PCTTHRESHOLD. |
| OVERFLOW TABLESPACE | Specifies the tablespace where the second half of the row data will be stored when the row's length exceeds the size set aside in PCTTHRESHOLD. |
| MAPPING TABLE | Causes the creation of an associated mapping table that is needed when creating bitmap indexes on the IOT. Mapping tables are described in more detail at the end of this section. |

After populating this table with data, the contents might look something like those shown in Figure 3.18.