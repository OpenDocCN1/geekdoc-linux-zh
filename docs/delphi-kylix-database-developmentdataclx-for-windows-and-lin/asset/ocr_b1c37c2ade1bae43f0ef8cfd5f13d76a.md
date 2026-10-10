# ## Adding Fields to a Client Dataset

To add fields to a client dataset at runtime, you use the client dataset's `FieldDefs` property.  
`FieldDefs` supports two methods for adding fields: `AddFieldDef` and `Add`.

# ### **AddFieldDef**

`TFieldDefs.AddFieldDef` is defined like this:

```
```
function AddFieldDef: TFieldDef;
```
```

As you can see, `AddFieldDef` takes no parameters and returns a `TFieldDef` object. When you have the `TFieldDef` object, you can set its properties, as the following code snippet shows.

```
```
var
  FieldDef: TFieldDef;
begin
  FieldDef := ClientDataSet1.FieldDefs.AddFieldDef;
  FieldDef.Name := 'Name';
  FieldDef.DataType := ftString;
  FieldDef.Size := 20;
  FieldDef.Required := True;
end;
```
```

# ### **Add**

A quicker way to add fields to a client dataset is to use the `TFieldDefs.Add` method, which is defined like this:

```
```
procedure Add(const Name: string; DataType: TFieldType; Size: Integer = 0;
  Required: Boolean = False);
```
```

The `Add` method takes the field name, the data type, the size (for string fields), and a flag indicating whether the field is required as parameters. By using `Add`, the preceding code snippet becomes the following single line of code:

```
```
ClientDataSet1.FieldDefs.Add('Name', ftString, 20, True);
```
```

Why would you ever want to use `AddFieldDef` when you could use `Add`? One reason is that `TFieldDef` contains several more advanced properties (such as field precision, whether or not it's read-only, and a few other attributes) in addition to the four supported by `Add`. If you want to set these properties for a field, you need to go through the `TFieldDef`. You should refer to the Delphi documentation for `TFieldDef` for more details.

# ## Creating the Dataset

After you create the field definitions, you need to create the empty dataset in memory. To do this, call `TClientDataSet.CreateDataSet`, like this:

```
```
ClientDataSet1.CreateDataSet;
```
```