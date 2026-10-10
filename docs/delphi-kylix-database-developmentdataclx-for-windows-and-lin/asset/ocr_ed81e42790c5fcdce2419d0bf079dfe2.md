To clone a dataset, create a second client dataset, and then call the second dataset's CloneCursor method, like this:

```
var
  cdsClone: TClientDataSet;
begin
  cdsClone := TClientDataSet.Create(nil);
  try
    cdsClone.CloneCursor(ClientDataSet1, False, False);

    // Perform some operations on the clone here.
  finally
    cdsClone.Free;
  end;
end;
```

This code snippnet creates a clone of ClientDataSet1, performs some operation(s) on the clone, and then frees the clone. Any Insert, Edit, or Delete operations performed on the clone are automatically reflected in ClientDataSet1.

CloneCursor is defined like this:

```
procedure CloneCursor(Source: TCustomClientDataSet; Reset: Boolean;
  KeepSettings: Boolean = False); virtual;
```

Source refers to the client dataset that you want to clone. You can't clone a nonclient dataset, such as a BDE dataset or a dbExpress dataset.

Reset and KeepSettings work hand in hand, and determine how the clone handles the following attributes:

+   * Filter, Filtered, FilterOptions, OnFilterRecord
+   * IndexName
+   * MasterSource, MasterFields
+   * ReadOnly
+   * RemoteServer, ProviderName

If Reset and KeepSettings are set to False, all the previous properties are copied from the original dataset to the clone. If Reset is False and KeepSettings is True, the previous properties are not changed for the clone. If Reset is True (regardless of the value of KeepSettings), the previous properties are cleared on the clone. Table 4.5 depicts this relationship.