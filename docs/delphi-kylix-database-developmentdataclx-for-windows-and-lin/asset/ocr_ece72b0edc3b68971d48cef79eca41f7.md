# UndoLastChange

You can undo the most recent change to the dataset (regardless of the record it was made to) by calling UndoLastChange.

UndoLastChange takes a single Booleean parameter (FollowChange) that indicates whether the dataset should position itself to the record that was affected by the undo operation. If FollowChange is True, the client dataset positions its cursor to the record that was undone or restored. If FollowChange is False, the most recently modified record is still restored, but the current record is not changed.

```
ClientDataSet1.First;
ClientDataSet1.Next;
ClientDataSet1.Edit;
ClientDataSet1.FieldNameByName( 'Last' ).AsString := 'Williams';
ClientDataSet1.Post;

ClientDataSet1.First;
ClientDataSet1.Next;
ClientDataSet1.Edit;
ClientDataSet1.FieldNameByName( 'Last' ).AsString := 'Carter';
ClientDataSet1.Post;

ClientDataSet1.Next;
ClientDataSet1.Edit;
ClientDataSet1.FieldNameByName( 'First' ).AsString := 'Sam';
ClientDataSet1.Post;

ClientDataSet.Last;

ClientDataSet1.UndoLastChange(True);
```

The preceding code snippet first modifies the second record in the dataset, then modifies the first record in the dataset, and then modifies the second record again. Finally, it moves to the end of the dataset. The call to UndoLastChange undoes only the second change to the second record, and repositions the dataset at the second record (because True was passed to UndoLastChange).

If you were to issue a second call to UndoLastChange, the modification to the first record in the dataset would be undone. A third call to UndoLastChange would undo the first modification to the second record.

# RevertRecord

RevertRecord undoes all changes to the current record in the dataset. Modifying the preceding code snippet slightly, we get the following: