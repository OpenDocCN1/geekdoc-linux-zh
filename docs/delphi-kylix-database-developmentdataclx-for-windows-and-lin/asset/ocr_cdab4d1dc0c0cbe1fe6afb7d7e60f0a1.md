# Disabling Data-Aware Components

This topic actually applies to all Delphi datasets, but I’m discussing it within the context of client datasets because you typically don’t connect data-aware components directly to a dbExpress dataset. Usually, data-aware components are connected to a client dataset.

As you’ve learned in this chapter, data-aware components actively track the current record in the dataset that they’re connected to. Although this is usually a good thing, at times you want to prevent data-aware components from updating. This happens most often when you are scrolling through a dataset to perform an operation on the records, and you don’t want to see all the data-aware components rapidly updating as you do. For example, take a look at the following code snippet:

```
var
    Bookmark: TBookmarkStr;
begin
    Bookmark := ClientDataSet1.Bookmark;
    try
        ClientDataSet1.First;
        while not ClientDataSet1.EOF do begin
            if ClientDataSet1.FieldName('Salary').AsFloat < 30000.0 then begin
                ClientDataSet1.Edit;
                ClientDataSet1.FieldName('Salary') :=
                    ClientDataSet1.FieldName('Salary').AsFloat * 1.05;
                ClientDataSet1.Post;
            end;
            ClientDataSet1.Next;
        end;
    finally
        ClientDataSet1.Bookmark := Bookmark);
    end;
end;
```

This code loops through all records in the dataset, giving anyone who makes less than $30,000 per year a 5% raise.

There is nothing wrong with this code from the standpoint that it does what it is intended to do. It even remembers the current record so that it can reposition the dataset correctly when it’s finished.

The problem with this code is that it’s slow. If you run it against the 10,000 record employee dataset that we created in the preceding chapter, you’ll see the grid scroll through all the records in the dataset as they are updated. (The example application at the end of this section shows this effect.)