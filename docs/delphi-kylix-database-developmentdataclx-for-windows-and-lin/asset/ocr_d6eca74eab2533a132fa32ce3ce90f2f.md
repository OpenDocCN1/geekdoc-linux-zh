Pass the table name for which you want to retrieve field names in the first parameter. The second parameter indicates the list in which the resulting field names are to be loaded. Any existing strings in the list are deleted.

```
GetFieldNames(`CONTACTS`, ListBox1.Items);
```

# GetIndexNames

Similar to GetFieldNames, GetIndexNames is used to retrieve the names of all indexes defined on a given table. GetIndexNames is defined as follows:

```
procedure GetIndexNames(const TableName: string; List: TStrings);
```

As with GetFieldNames, TableName represents the table that you want to get index names for. List indicates the list in which the resulting index names are to be loaded. Any existing strings in the list are deleted.

```
GetIndexNames(`CONTACTS`, ListBox1.Items);
```

# GetProcedureNames

To retrieve a list of stored procedures in a database, call the GetProcedureNames method. GetProcedureNames is defined like this:

```
procedure GetProcedureNames(List: TStrings);
```

Upon return from the procedure, List contains the list of stored procedure names. Any information previously stored in the list is deleted.

```
GetProcedureNames(ListBox1.Items);
```

# GetProcedureParams

GetProcedureParams returns a list of parameters for a given stored procedure. It is defined like this:

```
procedure GetProcedureParams(ProcedureName:string; List: TList);
```

The first parameter, ProcedureName, specifies the name of the stored procedure that you want to retrieve parameter names for. The second parameter refers to a precreated TList in which the procedure parameters are returned. Upon return from the procedure, List contains a list of parameters for the stored procedure.

List itself is not directly usable. You should call the helper function, LoadParamListItems, to convert the TList to a TParams object, which is a much easier structure to inspect.

The following code snippet shows how to correctly retrieve parameters for the stored procedure named CONTACTSBYSTATE.