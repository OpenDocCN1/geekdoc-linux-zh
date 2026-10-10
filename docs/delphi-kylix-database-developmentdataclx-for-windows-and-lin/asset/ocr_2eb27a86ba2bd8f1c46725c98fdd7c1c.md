![](bbox=[0.32, 0.12, 0.68, 0.4])

# **Figure 2.4**
Advanced displays contact data and related activities.

SchemaType refers to the type of schema data to return, and must be one of the values listed in Table 2.2.

| **TABLE 2.2 TSchemaType Values** |  |
|---|---|
| *Value* | *Schema Information Returned* |
| stNoSchema | No schema information. The dataset returns the results of the query or stored procedure rather than schema information for that object. |
| stTables | Information about the tables in the database that match the object name and pattern. |
| stSysTables | Information about the system tables in the database. |
| stProcedures | Information about the stored procedures in the database. |
| stColumns | Information about the columns for a single table. |
| stProcedureParams | Information about the parameters for a single stored procedure. |
| stIndexes | Information about the indexes for a single table. |

SchemaObjectName specifies the name of the table or stored procedure to return data for. It is only used for schema types of stColumns, stProcedureParams, and stIndexes. If the schema type is stColumns or stIndexes, SchemaObjectName specifies the table to return column or index information for. If the schema type is stProcedureParams, SchemaObjectName specifies the name of the stored procedure to return parameter information for.