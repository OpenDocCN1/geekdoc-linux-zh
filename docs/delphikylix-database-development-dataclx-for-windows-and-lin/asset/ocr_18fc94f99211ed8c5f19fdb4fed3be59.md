# Creating and Deleting Indexes at Runtime

In contrast to field definitions (which you usually create at design-time), index definitions are something that you frequently create at runtime. There are a couple of very good reasons for this:

+   * Indexes can be quickly and easily created and destroyed. So, if you only need an index for a short period of time (to print a report in a certain order, for example), creating and destroying the index on an as-needed basis helps conserve memory.
+   * Index information is not saved to a file or a stream when you persist a client dataset. When you load a client database from a file or a stream, you *must* re-create any indexes in your code.

To create an index, you use the client dataset's AddIndex method. AddIndex takes three mandatory parameters, as well as three optional parameters, and is defined like this:

```
```
procedure AddIndex(const Name, Fields: string; Options: TIndexOptions;
  const DescFields: string = ''; const CaseInsFields: string = '';
  const GroupingLevel: Integer = 0);
```
```

The parameters correspond to the TIndexDef properties listed in Table 3.2. The following code snippet shows how to create a unique index by last and first names:

```
`ClientDataSet1.AddIndex('byName', 'Last;First', [ixUnique]);`
```

When you decide that you no longer need an index (remember, you can always re-create it if you need it later), you can delete it using DeleteIndex. DeleteIndex takes a single parameter: the name of the index being deleted. The following line of code shows how to delete the index created in the preceding code snippet:

```
`ClientDataSet1.DeleteIndex('byName');`
```

# Using Indexes

Creating an index doesn't perform any actual sorting of the dataset. It simply creates an available index to the data. After you create an index, you make it active by setting the dataset's IndexName property, like this:

```
`ClientDataSet1.IndexName := 'byName';`
```

If you have two or more indexes defined on a dataset, you can quickly switch back and forth by changing the value of the IndexName property. If you want to discontinue the use of an index and revert to the default record order, you can set the IndexName property to an empty string, as the following code snippet illustrates:

```
```
// Do something in name order
ClientDataSet1.IndexName := 'byName';
```
```