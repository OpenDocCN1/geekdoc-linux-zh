
| Product | Description |
| :--- | :--- |
| | and grouping of data, and extensive customization (both at design time and at runtime). For more information, visit www.dexpexpress.com. |
| TopGrid | Provides both data-aware and non-data-aware versions of its powerful grid component, which allow display and editing of multiline notes, cells that contain controls (such as combo boxes and check boxes), and numerous customization features. You can find TopGrid at www.objectsight.com/TopGridOverview.htm. |
| Others | Numerous other freeware, shareware, and commercial grids are available to Delphi and Kylix programmers. The ones listed in this table are just some of the more popular and more widely known grids that are commercially available today. |

## Summary

This chapter continued the discussion of data-aware components with an overview of data-aware grids, which allow multiple rows of a dataset to be displayed on the screen at the same time. Specifically, this chapter taught you the following:

- You can create a quick and dirty grid by dropping a `TDBGrid` component on a form and using the default values. To customize the columns in the resulting grid, use the `Columns` property.
- Various grid options exist for altering the look and feel of the grid. (See Table 6.4 for a summary.)
- You can use various grid events to gain control over what happens when the user clicks a cell or performs some other action. (See Table 6.5 for a summary.)
- For the ultimate control over how the grid looks, use the `OnDrawColumnCell` event.
- `TClientDataSetGrid` is a free component that you can use for automatic column sorting and additional column customization.
- `TDBCtrlGrid` is a VCL-specific component that offers the capability to arrange data for a single record in a nonlinear format.

In addition, this chapter showed how to deal with several commonly encountered grid issues, such as detecting when a column is moved and persisting column states.

The following chapter begins a two-chapter exploration of client datasets.

# Dataset Providers

CHAPTER 7

## IN THIS CHAPTER

- What Is a Dataset Provider? 274
- Connecting to a Dataset 275
- Resolving Changes to Data 276
- Provider Options 293
- Provider Events 295
- Changing Field Values on the Server 297
- Intercepting Data 298
- Optional Parameters 300
- Master/Detail Relationships 301
- Providing and Resolving Data from Stored Procedures and Joins 302
- Connecting to a Local Database 308

Earlier in this book, you learned about dbExpress—a high-performance, low-overhead database technology. You learned that it is read-only and unidirectional, making it cumbersome to use directly for most interactive database applications.

Later, I introduced you to client datasets. Client datasets are especially well suited to database application front ends because they are fast, flexible, and powerful. However, they are inherently single user because they are RAM-based. Also, they read from and write to a proprietary file format.

So far, these may seem like disparate technologies used to solve different types of programming problems. This chapter and the next tie them together, showing you how you can use client datasets to read and write data using dbExpress as the underlying database technology.

This chapter shows you how to use providers to create multitier database applications.

## What Is a Dataset Provider?

A dataset provider forms a conduit between a client dataset and an external data store—typically another dataset, such as a TSQLDataSet. It provides data to the client dataset on request and sends data back to the underlying data store when the client changes it—a technique called *resolving*.

The component used to accomplish this is TDataSetProvider, found on the Data Access tab of the component palette.

**Note**

> Nothing about dataset providers ties them to dbExpress specifically. The information presented in this chapter is applicable to other database technologies as well, such as BDE and dbGo (formerly called ADOExpress).
>
> For a dataset to be compatible with TDataSetProvider, it must support the IProviderSupport interface, defined in DB.pas like this:

```pascal
IProviderSupport = interface
  procedure PSEndTransaction(Commit: Boolean);
  procedure PSExecute;
  function PSExecuteStatement(const ASQL: string; AParams: TParams;
    ResultSet: Pointer = nil): Integer;
  procedure PSEGetAttributes(List: TList);
  function PSEGetDefaultOrder: TIndexDef;
  function PSEGetKeyFields: string;
  function PSEGetParams: TParams;
  function PSEGetQuoteChar: string;
  function PSEGetTableName: string;
  function PSGetIndexDefs(IndexTypes: TIndexOptions =
[ixPrimary, ixNonMaintained]): TIndexDefs;
  function PSGetUpdateException(E: Exception;
  Prev: EUpdateError): EUpdateError;
  function PSInTransaction: Boolean;
  function PSISQLBased: Boolean;
  function PSISQLSupported: Boolean;
  procedure PSReset;
  procedure PSSetParams(AParams: TParams);
  procedure PSSetCommandText(const CommandText: string);
  procedure PSSStartTransaction;
  function PSUpdateRecord(UpdateKind: UpdateKind;
  Delta: TDataSet): Boolean;
end;
```

TDataSet implements stub functions for these methods, which generally do nothing or raise an exception. The datasets included with Delphi (BDE, dbExpress, and dbGo) override these methods to provide a specific implementation.

## Connecting to a Dataset

In this section I'll show you how to connect a client dataset to another dataset. To do so, follow these steps:

1. Start a new application and drop a `TSQLConnection` and `TSQLDataSet` on the main form. Connect these components to a database, using the techniques discussed in Chapters 1 and 2.
2. Drop a `TDataSetProvider` on the main form. Set the `DataSet` property to the `TSQLDataSet` component. For now, leave all other properties set to their default values.
3. Drop a `TClientDataSet` on the main form. Set its `ProviderName` property to the dataset provider you created in the previous step.
4. Connect a `TDataSource` component to the client dataset and hook up a `TDBGrid` component to the data source.
5. Create an event handler for the form's `FormCreate` event and add the following line of code to it:
   `C1ClientDataSet1.Open;`
6. Run the application.

If you set everything up correctly, you should see the data from the dbExpress database displayed in the grid. Notice that you can scroll forward and backward through the data, and you can make changes to the data. However, if you leave the application and run it again, none of your changes have been saved to the database. We'll remedy that situation in the next section. For now, I just want you to see how easy it is to establish the relationship between a client dataset and another dataset. This relationship is important because dbExpress datasets don't support editing or bidirectional scrolling on their own—they must be connected to a client dataset to provide these capabilities.

Figure 7.1 shows the results of the preceding steps after connecting to the CONMAN database.

![](img/52a35759a0f10dade27a840504be5d82_289_0.png)

### FIGURE 7.1
Sample application at design time and runtime.

You should leave this sample application loaded in Delphi or save it to disk somewhere; we'll embellish on it in the following sections.

## Resolving Changes to Data

If you'll recall from Chapter 4, client datasets store changes to data in a change log rather than applying changes to the underlying data immediately. Because of that, when you changed the grid's data in the preceding section, those changes didn't get reflected in the underlying database.

### Applying Updates

To save changes to the database permanently, you need to call the client dataset's ApplyUpdates method. ApplyUpdates detects that the dataset is connected to a provider and takes care of sending changes back through the provider to the database.
