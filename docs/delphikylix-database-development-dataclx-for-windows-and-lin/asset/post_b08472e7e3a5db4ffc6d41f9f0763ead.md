
By default, fields are returned in the order in which they were declared. By passing `sONAME` as the final parameter to `GetFieldNames`, the field names are returned in alphabetical order.

## Retrieving Additional Field Metadata

If you want to retrieve additional metadata for a field, call `TSQLMetaData.GetFieldMetaData`, which is defined like this:

```pascal
function GetFieldMetaData(const ATableName,
  AColNameName: string): TFieldMetaData;
```

This method takes the table name and field name as parameters and returns a `TFieldMetaData` record containing information about the field in question. `TFieldMetaData` is defined like this:

```pascal
TFieldMetaData = record
  ColumnName: string;
  ColumnPosition: LongInt;
  ColumnDataType: LongInt;
  ColumnTypeName: string;
  ColumnSubType: LongInt;
  ColumnLength: LongInt;
  ColumnPrecision: LongInt;
  ColumnScale: LongInt;
  ColumnNulable: LongInt;  // 1=Not Null, 0=Null
end;
```

As you can see, it specifies the column (or field) name, the zero-based index, the type of data contained in the column, and other pertinent information about the field.

## Retrieving Index Data

One useful method that `TSQLMetaData` provides is a way to get information about an index on a table. Two forms are provided. The first form retrieves information about any index, given its name. Two methods are provided for this use.

```pascal
procedure GetIndexFieldNames(const ATableName, AIndexName: string;
  AList: TStrings);
```

`GetIndexFieldNames` returns a string list composed of the fields that make up the index `AIndexName` on table `ATableName`.

```pascal
function GetIndexFields(const ATableName, AIndexName: string): string;
```

`GetIndexFields` returns the same list as a semicolon-delimited list.

The second form of index data retrieval is to retrieve data about the primary key, rather than an arbitrary index. To retrieve a list of fields that make up the primary key, you could pass in the primary key name either to `GetIndexFieldNames` or `GetIndexFields`. However, you might not know the name of the primary key. In that case, you can call either **GetPrimaryKeyFieldNames** or **GetPrimaryKeyFields**.

```pascal
procedure GetPrimaryKeyFieldNames(const ATableName: string;
    AList: TStrings);
function GetPrimaryKeyFields(const ATableName: string): string;
```

These two methods perform the same service as **GetIndexFieldNames** and **GetIndexFields**, except that they always work on the primary key.

### Additional Methods

**TSQLMetaData** also provides a collection of methods to return the INSERT, UPDATE, and SELECT SQL statements for a given table. The three methods are listed next:

```pascal
function GetInsertStatement(const ATableName: string;
    ASQL: TStrings): Integer;
function GetUpdateStatement(const ATableName: string;
    ASQL: TStrings): Integer;
function GetSelectStatement(const ATableName: string;
    ASQL: TStrings): Integer;
```

Given a table name, these three methods return the corresponding INSERT, UPDATE, or SELECT SQL statement in the `ASQL` parameter.

### Data Pumping

**TSQLDataPump** provides an answer to the BDE’s **TBatchMove** component, allowing you to easily move data from one table to another.

To do this, **TSQLDataPump** publishes **SQLMetaDataSource** and **SQLMetaDataDestination** properties, which reference the **TSQLMetaData** components that point to the source and destination database connections, respectively.

After you specify the source and destination databases, set the **SQLSource** property to a valid SELECT statement for the source database, such as:

```sql
SELECT EMP_NO, FIRST_NAME, LAST_NAME, PHONE_EXT, HIRE_DATE, DEPT_NO,
JOB_CODE, JOB_GRADE, JOB_COUNTRY, SALARY FROM EMPLOYEE
```

Next, set the **DestinationTable** property to the name of the table in the destination database, and then double-click the **DestinationFields** property, which allows you to set up a mapping between the fields in the source table and the fields in the destination table.

Finally, set the **DataMoveMode** to the appropriate action to perform. Table B.1 lists the modes that may be used.

![](img/52a35759a0f10dade27a840504be5d82_396_0.png)

**Table B.1** Valid DataMoveMode Values

| Value | Description |
| :--- | :--- |
| dmAlwaysInsert | Inserts all selected records into the destination table. |
| DmAppend | Appends selected records to the destination table. |
| dmAppendUpdate | Updates the record if it already exists in the destination table. Otherwise, appends the record to the destination table. |
| DmDelete | Deletes matching records from the destination table. |
| DmUpdate | Updates matching records in the destination table. |

At this point, all the required properties are set, so you need to call only `TSQLDataPump.Execute` to perform the batch move operation.

## For More Information

This has been only a brief overview of the capabilities provided by dbExpress Plus. Because it is an open source project, it stands to reason that the code may grow to provide more functionality than that discussed here. The dbExpress Plus download also comes with a demo application that shows how to use many of the methods discussed in this appendix.

# INDEX

# SYMBOLS

- `+` (Addition) operator, 128
- `*` (asterisk) operator, 129
- `\` (backslash), 210
- `/` (data separator), 210
- `.` (decimal point), 207
- `#` (digit placeholder), 207
- `0` (digit placeholder), 207
- `[db]` (Division) operator, 128
- `"` (double quotation mark), 207
- `=` (equality test) operator, 127
- `!` (exclamation point), 210
- `>` (greater than) operator, 127
- `>=` (greater than or equal to) operator, 127
- `>` (greater than sign), 210
- `<>` (greater than/less than sign), 210
- `<>` (inequality test) operator, 127
- `<` (less than) operator, 127
- `<=` (less than or equal to) operator, 127
- `<` (less than sign), 210
- `[ts]` (multiplication) operator, 128
- `#` (pound sign), 209
- `;` (separator character), 207, 210
- `'` (single quotation mark), 207
- `0` specifier, 209
- `9` specifier, 209
- `–` (Subtraction) operator, 128
- `,` (thousands separator), 207
- `:` (time separator), 210
- `_` (underscore), 210

# A

- A specifier, 209
- accessing
  - fields (client datasets), 103
  - *nonpersistent* fields, 104-105
  - *persistent* fields, 103
  - Fields objects, 64
  - providers on different form, 308
- ACID (Atomic, Consistent, Isolated, Durable)
  - properties, 37
  - action handlers, 228
- activating indexes
  - (client datasets), 121
- Active property, 60
- Add Connection button, 10
- Add method, 102
- Add to Interface command (remote data module context menu), 324
- Add To Interface dialog box, 324
- AddFieldDef method, 102
- AddIndex method, 121
- adding
  - fields (client datasets), 102
  - modules (remote data modules), 324
- Addition (+) operator, 128
- Address property, 331
- Advanced application (MainForm.pas), code listing, 76-79
- advantages
  - client datasets, 94-95
  - ConMan, 373
- AfterApplyUpdates event, 295
- AfterCancel event, 150
- AfterClose event, 150
- AfterConnect event, 14
- AfterDisconnect event, 14
- AfterEdit event, 150
- AfterExecute event, 295
- AfterGetParams event, 295
- AfterGetRecords event, 295, 342
- AfterInsert event, 150
- AfterOpen event, 150
- AfterPost event, 150
- AfterRowRequest event, 295
- AfterScroll event, 150
- AfterUpdateRecord event, 295
- aggregate expressions, 195
- aggregate fields, 96
- aggregate types, 195
- aggregates
  - across datasets, 196-197
  - determining position of record, 197
  - enabling/disabling, 197
  - grouped, 196
  - maintained, 192-193
  - *creating at design time*, 193-195
  - *creating at runtime*, 195
- Aggregates property, 194-195
- Alignment property, 242-244
- AllowDelete property, 267
- AllowInsert property, 267
- And operator, 128
- Apartment value, 321
- Append method, 105
- application servers
  - ConMan, 352-353
  - creating, 318
  - testing, 328-329
- applications. See also individual applications
  - client
    - ConMan, 358, 361-362, 371-372
    - CORBA connections, 335
    - creating, 329-330
    - DCOM connections, 333
    - HTTP connections, 334
    - *intercepting data packets*, 333
    - *multiple connection types*, 343-344
