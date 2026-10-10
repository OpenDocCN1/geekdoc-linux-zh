When the schema type is known, it is a simple matter to make the appropriate call to `SetSchemaInfo`, open the dataset, and load the list view with the schema information. Certain columns (namely TABLE\_TYPE, PROC\_TYPE, COLUMN\_TYPE, COLUMN\_DATATYPE, COLUMN\_SUBTYPE, and INDEX\_TYPE) are bitmapped numeric columns. The program makes calls to a handful of helper routines to display a textual representation of these values. The rest of the columns are displayed as is.

You will notice that you run this application that different schema types return different data fields. Tables 2.3\~2.7 explain the columns that are returned for each of these schema types.

Table 2.3 lists the columns that are returned for a schema type of `stTables` or `stSystemTables`.

TABLE 2.3 stTables and stSystemTables Schema Columns

| Column | Description |
| :--- | :--- |
| RECO | The absolute record number. It is one for the first record, two for the second, and so on. |
| CATALOG\_NAME | The name of the catalog, or database, that contains the table. |
| SCHEMA\_NAME | The owner of the table. |
| TABLE\_NAME | The table name. |
| TABLE\_TYPE | A bitmapped value that represents the type of table. See Listing 2.4, or the source code for DBXpress.pas, for an explanation of the possible values for this field. |

Table 2.4 lists the columns that are returned for a schema type of `stProcedures`.

TABLE 2.4 stProcedures Schema Columns

| Column | Description |
| :--- | :--- |
| RECO | The absolute record number. It is one for the first record, two for the second, and so on. |
| CATALOG\_NAME | The name of the catalog, or database, that contains the stored procedure. |
| SCHEMA\_NAME | The owner of the stored procedure. |
| PROC\_NAME | The name of the stored procedure. |
| PROC\_TYPE | A bitmapped value that represents the type of stored procedure. See Listing 2.4, or the source code for DBXpress.pas, for an explanation of the possible values for this field. |
| IN\_PARAMS | The number of input parameters to the stored procedure. |
| OUT\_PARAMS | The number of output parameters from the stored procedure. |