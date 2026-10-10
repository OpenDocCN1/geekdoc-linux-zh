
## `TfrmMain.GetColTypeString`

```pascal
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
```

## `TfrmMain.GetColDataTypeString`

```pascal
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
```

## `TfrmMain.GetColSubTypeString`

```pascal
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
```

## `TfrmMain.GetIndexTypeString`

```pascal
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
```

```pascal
Check(eSQLSysProcedure, 'System');
if Result = '' then
  Result := '$' + IntToHex(ProcType, 2);
end;
```
