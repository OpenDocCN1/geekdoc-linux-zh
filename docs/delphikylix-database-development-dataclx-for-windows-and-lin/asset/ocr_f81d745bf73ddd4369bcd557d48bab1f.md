![](bbox=[0.32, 0.12, 0.58, 0.29])

# FIGURE 1.7
Transactions may be nested or overlapped.

Not all databases support multiple transactions. Unfortunately, to determine whether a database supports multiple transactions, you can't check a simple property. TSQLConnection contains a private field named fSupportsMultiTrans, but there is no public access to it. All is not lost, however, as you can use the following function to retrieve the value of this property:

```
function SupportsMultiTrans(conn: TSQLConnection): Boolean;
var
  Supported: LongBool;
  PropSize: SmallInt;
begin
  conn.MetaData.GetOption(eMetaSupportsTransactions, @Supported,
    SizeOf(Integer), PropSize);
  Result := Supported;
end;
```

If the database does not support multiple transactions, you want to refrain from calling StartTransaction while a transaction is active. You can test to see whether a transaction is currently active by checking the InTransaction property, like this:

```
if not SQLConnection.InTransaction then
  // Safe to start a transaction
```

If the database supports multiple transactions, you can nest them, as the following code snippet shows:

```
var
  TransOuter: TTransactionDesc;
  TransInner: TTransactionDesc;
begin
  TransOuter.TransactionID := 1;
  TransOuter.IsolationLevel := x1READCOMMITTED;
  SQLConnection.StartTransaction(TransOuter);
  try
```