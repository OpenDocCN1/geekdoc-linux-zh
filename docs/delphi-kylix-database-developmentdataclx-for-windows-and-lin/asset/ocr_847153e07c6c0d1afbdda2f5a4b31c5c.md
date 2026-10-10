If you are not using persistent field objects, you would do this instead:

```
ClientDataSet1.Edit;
ClientDataSet1.FieldName('FirstName').AsString := 'John';
```

The important thing to remember is to call the dataset's `Edit` method before attempting to set the field value. If the dataset is already in edit or insert mode, the redundant call to `Edit` doesn't have any adverse effects. If for some reason the dataset can't be edited (for example, if the dataset's `ReadOnly` property is set to `True`), the call to `Edit` raises an exception, which you should be prepared to handle gracefully.

# Controlling When the User Is Allowed to Edit Data

By default, as soon as the user starts typing into a data-aware component, VCL/CLX puts the associated dataset into edit mode. If you want to control the user's ability to make edits from within your code, you have four options:

+   * Set the dataset's `ReadOnly` property to `True`, preventing the user from changing any values in the dataset. This also prevents any changes being made to the data through code.
+   * Set the underlying field's `ReadOnly` property to `True`. This prevents the user from modifying the field, and also prevents the field from being modified through code.
+   * Set the data-aware component's `ReadOnly` property to `True`, preventing the user from changing a single value in the dataset. Note that this has no effect on any changes that you make in your code using the method described in the preceding section. Setting the component's `ReadOnly` property does not in any way make the field itself read-only. It merely prevents the user from making direct modifications to the data through the component.
+   * Set the data source's `AutoEdit` property to `False`, preventing the dataset from automatically entering an edit state when the user starts typing into a data-aware component. If you go this route, you will typically provide a menu item or a button on the form, which the user clicks to put the dataset into edit mode. Alternatively, you can use a `TDBNavigator`, which is discussed later in this chapter.

# Formatting and Editing Field Values

Data-aware components don't have a built-in mechanism for controlling the formatting of field values during input and output, so at first glance, you might assume that there is no way to display nicely formatted numeric and string data. However, it turns out that data formatting is taken care of at the field level rather than at the component level. For this reason, you can set a specific output format for a field, and the same format will be used anywhere that a data-aware component is used to display that field.