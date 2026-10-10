

# 列表 2.4

```pascal
else if dataset.Fields[Index].FieldName = 'INDEX_TYPE' then
  ListItem.SubItems.Add(GetIndexTypeString(
    dataset.Fields[Index].AsInteger))
else
  ListItem.SubItems.Add(dataset.Fields[Index].AsString);
end;

dataset.Next;
end;
finally
  lvColumns.Columns.EndUpdate;
end;
finally
  lvColumns.Items.EndUpdate;
end;
finally
  conn.Close;
end;
end;

function TfrmMain.GetTableTypeString(TableType: Integer): string;

procedure Check(SQLTableType: Integer; const Desc: string);
begin
  if (TableType and SQLTableType) <> 0 then begin
    if Result <> '' then
      Result := Result + ', ';
    Result := Result + Desc;
  end;
end;

begin
  Result := '';

  Check(eSQLTable, 'Table');
  Check(eSQLView, 'View');
  Check(eSQLSynonym, 'Synonym');
  Check(eSQLSystemTable, 'System');
  Check(eSQLTempTable, 'Temp');
  Check(eSQLLocal, 'Local');

  if Result = '' then
    Result := '$' + IntToHex(TableType, 2);
end;

function TfrmMain.GetProcTypeString(ProcType: Integer): string;

procedure Check(SQLProcType: Integer; const Desc: string);
begin
  if (ProcType and SQLProcType) <> 0 then begin
    if Result <> '' then
      Result := Result + ', ';
    Result := Result + Desc;
  end;
end;
begin
  Result := '';

  Check(eSQLProcedure, 'Procedure');
  Check(eSQLFunction, 'Function');
  Check(eSQLPackage, 'Package');
  Check(eSQLSysProcedure, 'System');

  if Result = '' then
    Result := '$' + IntToHex(ProcType, 2);
end;

function TfrmMain.GetColTypeString(ColType: Integer): string;

procedure Check(SQLColType: Integer; const Desc: string);
begin
  if (ColType and SQLColType) <> 0 then begin
    if Result <> '' then
      Result := Result + ', ';
    Result := Result + Desc;
  end;
end;
begin
  Result := '';

  Check(eSQLRowId, 'Row Id');
  Check(eSQLRowVersion, 'Row Version');
  Check(eSQLAutoIncr, 'Auto Incr');
  Check(eSQLDefault, 'Default');

  if Result = '' then
    Result := '$' + IntToHex(ColType, 2);
end;

function TfrmMain.GetColDataTypeString(ColDataType: Integer): string;
begin
    case ColDataType of
        fldUNKNOWN:  Result := 'Unknown';
        fldZSTRING:  Result := 'ZString';
        fldDATE:     Result := 'Date';
        fldBLOB:     Result := 'BLOB';
        fldBOOL:     Result := 'Bool';
        fldINT16:    Result := 'Int16';
        fldINT32:    Result := 'Int32';
        fldFLOAT:    Result := 'Float';
        fldBCD:      Result := 'BCD';
        fldBYTES:    Result := 'Bytes';
        fldTIME:     Result := 'Time';
        fldTIMESTAMP: Result := 'Timestamp';
        fldUINT16:   Result := 'UInt16';
        fldUINT32:   Result := 'UInt32';
        fldFLOATIEEE: Result := 'FloatIEEE';
        fldVARBYTES: Result := 'VarBytes';
        fldLOCKINFO: Result := 'LockInfo';
        fldCURSOR:   Result := 'Cursor';
        fldINT64:    Result := 'Int64';
        fldUINT64:   Result := 'UInt64';
        fldADT:      Result := 'ADT';
        fldARRAY:    Result := 'Array';
        fldREF:      Result := 'RefADT';
        fldTABLE:    Result := 'Table';
        fldDATETIME: Result := 'DateTime';
        fldFMTBCD:   Result := 'FmtBCD';
        else          Result := '$' + IntToHex(ColDataType, 2);
    end;
end;

function TfrmMain.GetColSubTypeString(ColSubType: Integer): string;
begin
    case ColSubType of
        fldstMONEY:    Result := 'Money';
        fldstMEMO:     Result := 'Memo';
        fldstBINARY:   Result := 'Binary';
        fldstFMTMEMO:  Result := 'Fmt Memo';
        fldstOLEOBJ:   Result := 'Pdox OLE';
        fldstGRAPHIC:  Result := 'Graphic';
        fldstDBSOLEOBJ:      Result := 'dBase OLE';
        fldstTYPEDBBINARY:   Result := 'Typed Binary';
        fldstACCOLEOBJ:      Result := 'Access OLE';
        fldstTHMEMO:         Result := 'CLOB';
        fldstHBINARY:        Result := 'BLOB';
        fldstBFILE:          Result := 'BFILE';
        fldstPASSWORD:       Result := 'Password';
        fldstFIXED:          Result := 'Char';
        fldstUNICODE:        Result := 'Unicode';
        fldstAUTOINC:        Result := 'AutoInc';
        fldstADTNestedTable: Result := 'ADT Nest';
        fldstADTDATE:        Result := '$' + IntToHex(ColSubType, 2);
    else
    end;
end;

function TfrmMain.GetIndexTypeString(IndexType: Integer): string;

procedure Check(SQLIndexType: Integer; const Desc: string);
begin
    if (IndexType and SQLIndexType) <> 0 then begin
        if Result <> '' then
            Result := Result + ',';
        Result := Result + Desc;
    end;
end;

begin
    Result := '';

    Check(eSQLNonUnique, 'Non-unique');
    Check(eSQLUnique,    'Unique');
    Check(eSQLPrimaryKey, 'Primary');

    if Result = '' then
        Result := '$' + IntToHex(IndexType, 2);
end;

end.
```

![](img/52a35759a0f10dade27a840504be5d82_100_0.png)

Schema 应用程序的核心包含在单个方法中：`btnRetrieveClick`。`btnRetrieveClick` 确定用户选择了哪种 schema 类型，并确保如果请求的 schema 类型是列、索引或存储过程参数，用户必须输入一个对象名称。

当 schema 类型确定后，调用适当的 `SetSchemaInfo`、打开数据集并使用 schema 信息加载列表视图就变得很简单了。某些列（即 `TABLE_TYPE`、`PROC_TYPE`、`COLUMN_TYPE`、`COLUMN_DATATYPE`、`COLUMN_SUBTYPE` 和 `INDEX_TYPE`）是位图数值列。该程序调用一系列辅助例程以显示这些值的文本表示形式。其余的列则按原样显示。

你会发现，当运行此应用程序时，不同的 schema 类型返回不同的数据字段。表 2.3-2.7 解释了这些 schema 类型中每一个所返回的列。

表 2.3 列出了针对 `stTables` 或 `stSystemTables` schema 类型返回的列。

### 表 2.3 stTables 和 stSystemTables Schema 列

| 列名 | 描述 |
| :--- | :--- |
| RECO | 绝对记录号。第一条记录为 1，第二条为 2，依此类推。 |
| CATALOG_NAME | 包含该表的目录或数据库的名称。 |
| SCHEMA_NAME | 该表的所有者。 |
| TABLE_NAME | 表名。 |
| TABLE_TYPE | 表示表类型的位图值。有关此字段可能值的解释，请参见列表 2.4 或 DBXpress.pas 的源代码。 |

表 2.4 列出了针对 `stProcedures` schema 类型返回的列。

### 表 2.4 stProcedures Schema 列

| 列名 | 描述 |
| :--- | :--- |
| RECO | 绝对记录号。第一条记录为 1，第二条为 2，依此类推。 |
| CATALOG_NAME | 包含该存储过程的目录或数据库的名称。 |
| SCHEMA_NAME | 该存储过程的所有者。 |
| PROC_NAME | 存储过程名称。 |
| PROC_TYPE | 表示存储过程类型的位图值。有关此字段可能值的解释，请参见列表 2.4 或 DBXpress.pas 的源代码。 |
| IN_PARAMS | 存储过程的输入参数数量。 |
| OUT_PARAMS | 存储过程的输出参数数量。 |

表 2.5 列出了针对 *stColumns* schema 类型返回的列。

### 表 2.5 stColumns Schema 列

| 列名 | 描述 |
| :--- | :--- |
| RECO | 绝对记录号。第一条记录为 1，第二条为 2，依此类推。 |
| CATALOG_NAME | 包含该表的目录或数据库的名称。 |
| SCHEMA_NAME | 该列的所有者。 |
| TABLE_NAME | 包含该列的表名。 |
| COLUMN_NAME | 列名。 |
| COLUMN_POSITION | 列在表定义中基于零的位置。 |
| COLUMN_TYPE | 表示列类型的位图值。有关此字段可能值的解释，请参见列表 2.4 或 DBXpress.pas 的源代码。 |
| COLUMN_DATATYPE | 逻辑字段类型。有关此字段可能值的解释，请参见列表 2.4 或 DBXpress.pas 的源代码。 |
| COLUMN_TYPENAME | SQL 列类型（*VARCHAR*、*BLOB* 等）。 |
| COLUMN_SUBTYPE | 逻辑字段子类型。有关此字段可能值的解释，请参见列表 2.4 或 DBXpress.pas 的源代码。 |
| COLUMN_LENGTH | 列的字节大小。 |
| COLUMN_PRECISION | 列的精度。其值因列类型而异。例如，对于字符串，它是字符数；对于 BCD 值，它是有效数字的位数。 |
| COLUMN_SCALE | 数值比例。对于 BCD 列，它是小数点右边的位数。 |
| COLUMN_NULLABLE | 如果列可以包含 *NULL* 值，则为 1；如果不能包含 *NULL* 值，则为 0。 |

表 2.6 列出了针对 *stProcedureParams* schema 类型返回的列。

### 表 2.6 stProcedureParams Schema 列

| 列名 | 描述 |
| :--- | :--- |
| RECO | 绝对记录号。第一条记录为 1，第二条为 2，依此类推。 |
| CATALOG_NAME | 包含该存储过程的目录或数据库的名称。 |

