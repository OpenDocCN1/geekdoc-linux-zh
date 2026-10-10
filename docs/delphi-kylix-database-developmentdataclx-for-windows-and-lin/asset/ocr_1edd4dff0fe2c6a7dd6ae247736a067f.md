You can also retrieve multiple savepoints, like this:

```
```
var
  Baseline1: Integer;
  Baseline2: Integer;
begin
  Baseline1 := ClientDataSet.SavePoint;
  // Perform more dataset work here
  Baseline2 := ClientDataSet.SavePoint;
```
```

Be careful when using SavePoint along with RevertRecord or UndoLastChange. If you retrieve a SavePoint, and then undo your most recent modifications past the point of the save, an exception is raised. The following code, shown in Listing 4.6, is just asking for trouble:

# **LISTING 4.6** Incorrect Use of SavePoints

```
```
ClientDataSet1.First;
ClientDataSet1.Next;
ClientDataSet1.Edit;
ClientDataSet1.FieldByName('Last').AsString := 'Williams';  // Change 1
ClientDataSet1.Post;

ClientDataSet1.First;
ClientDataSet1.Edit;
ClientDataSet1.FieldByName('Last').AsString := 'Carter';   // Change 2
ClientDataSet1.Post;

Baseline := ClientDataSet1.SavePoint;  // 2 changes on the "stack"

ClientDataSet1.Next;
ClientDataSet1.Edit;
ClientDataSet1.FieldByName('First').AsString := 'Sam';    // Change 3
ClientDataSet1.Post;

ClientDataSet1.UndoLastChange(True);  // 2 changes on the "stack"
ClientDataSet1.UndoLastChange(True);  // 1 change on the "stack"
ClientDataSet1.SavePoint := Baseline;  // Exception is raised here
```
```

In this code snippet, two changes are made, and then a baseline is established. Next, a third change is made, and then the third and second changes are undone. Finally, the code attempts to revert to the save point. Because the change log has been reversed past the point of the save point, Delphi raises an exception.