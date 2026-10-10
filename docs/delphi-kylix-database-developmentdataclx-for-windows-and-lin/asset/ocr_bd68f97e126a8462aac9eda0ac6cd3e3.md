The results of this test are impressive. The baseline test (which doesn’t disable controls) takes about 19.6 seconds to run on my 1.4GHz Pentium 4. With the additional five lines to disable and re-enable data-aware components, the code takes a mere 560ms to execute (and has no annoying screen activity, to boot).

# # BLOBs

BLOBs, or Binary Large Objects, are a fundamental part of many modern database applications. Whether you want to store images, formatted and unformatted notes, streamed components, or any other chunk of bytes; BLOBs are an essential part of your database-programming repertoire.

In this section, I’ll show you how to effectvively store BLOBs in a client dataset and how to retrieve them later. In the pages to follow, I’ll focus specifically on notes, images, streamed components, and generic BLOB storage.

As with other field types, you can create BLOB fields either at design time or at runtime. The following code snippet shows how to create a BLOB field at runtime:

```
ClienDataSet1.FieldDefs.Add( 'Notes' , ftBLOB );
```

This code creates a field named **Notes**, of type **ftBLOB**.

# ## Notes

One of the most common ways to use a BLOB field is to store notes, or free-format text. For small amounts of text a string field typically suffices, but if you want to store entire memos, you need to use a BLOB field.

Accessing a BLOB as a string is particularly easy. You can simply call the **AsString** method on the field, like this:

```
Memo1.Text := ClienDataSet1.FieldByName('Notes').AsString;
```

Similarly, to store the memo back to the field, you would write code like the following:

```
ClienDataSet1.FieldByName( 'Notes' ).AsString := Memo1.Text ;
```

# ## Images

Another common use of BLOB fields is to store images. You might want to write a Delphi application to catalog the pictures you’ve taken on your digital camera, or you might want to track scanned documents in a paperness office. Either way, a BLOB field provides the necessary support to store these images in a database.