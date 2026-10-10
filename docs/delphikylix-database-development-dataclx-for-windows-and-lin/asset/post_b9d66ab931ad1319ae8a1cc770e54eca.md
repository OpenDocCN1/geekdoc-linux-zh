
# ## Ordering Data Returned from the Server

There are two ways to order the data returned from the server. One way relates to the TSQLTable component, and the other is used with the TSQLQuery and TSQLDataSet components. I’ll address the TSQLTable component first.

# ## Ordering Data from a Table

If you are using a TSQLTable, you can set the component’s IndexName or IndexFieldNames property before opening the dataset. IndexName refers to the name of an index as it is stored in the underlying database. For example, in the ConMan database, I have defined an index, named IX_CONMANE, which is composed of the LAST and FIRST columns (in that order).

```
SQLTable1.IndexName := 'IX_CONMANE';
```

If you don’t know the name of the underlying index, you can set the IndexFieldNames property instead. IndexFieldNames is a semicolon-delimited list of fields that make up the index.

```
SQLTable1.IndexFieldNames := 'LAST;FIRST';
```

> **NOTE**
>
> You do not need to ensure that there is an index defined on the fields that you set in the IndexFieldNames property. Behind the scenes, TSQLTable creates an ORDER BY clause for the SQL statement that it passes to the database (based on the fields listed in IndexFieldNames).

# ## Ordering Data from a Query

If you’re using a `TSQLQuery` or `TSQLDataSet` component, the method used to order the result set is more straightforward: You simply add an `ORDER BY` clause to the SQL statement yourself, like this:

```
SQLDataSet1.CommandText := 'SELECT * FROM CONTACTS ORDER BY LAST, FIRST';
```

If there is an index defined in the database that supports the `ORDER BY` clause, the underlying database engine uses the index for increased speed. If not, the database engine sorts the data in the requested order before it is returned to the application.

# ## Master/Detail Relationships

Although standalone datasets are useful, datasets are commonly related to other datasets in master/detail relationships. A master/detail relationship (also known as a one-to-many relationship) is one in which a single record in one dataset corresponds to one, or more, records in another dataset.

The most commonly cited example of a master/detail relationship uses customers, orders, and items as its datasets. A single customer can place more than one order with a given vendor. In turn, a single order can contain more than one item. Figure 2.3 shows a graphic representation of typical customer, order, and item datasets.

![](img/52a35759a0f10dade27a840504be5d82_87_0.png)

**FIGURE 2.3**
*Master/Detail relationships can have multiple levels.*

In the ConMan database, the CONTACT and ACTIVITIES tables are joined in a master/detail relationship on the ContactID field.

To create this master/detail link in an application, you would perform the following steps:

1. Place a TSQLConnection component on a form and connect it to the ConMan database.
2. Drop a TSQLDataSet on the form and set its TSQLConnection property to the TSQLConnection component that you created in step 1. Set the Name property to sqlContacts and the CommandText property to SELECT * FROM CONTACTS. This is the master dataset.
3. Drop a TDataSource on the form, set its Name property to dsContacts, and set its DataSet property to sqlContacts.
4. Drop another TSQLDataSet on the form. Set the Name property to sqlActivities and the DataSource property to dsContacts. This is the detail dataset.
5. Set sqlActivities.CommandText to SELECT * FROM ACTIVITIES WHERE ContactID = :ContactID.

That's all that's required to establish a master/detail relationship in your program code. You should note the following points:

- The detail dataset's CommandText property is always a parameterized query. The parameter names actually refer to column names in the master dataset.
- Whenever the master dataset changes records, the detail dataset automatically retrieves the records that are associated with the current master record.

The first point deserves a little more explanation.

You'll recall from the section titled “Parameterized Queries” that when using parameterized queries, you typically make calls to TSQLDataSet.ParamByName to set the parameters.

With a detail dataset, parameter substitution is a bit more automated. VCL/CLX notices that the detail dataset's DataSource parameter is assigned, so it looks to the data source's dataset as the source of parameter values.

For example, in the CONTACT/ACTIVITIES example, sqlActivities.CommandText contains a single parameter: ContactID. When Delphi assigns the value of the ContactID parameter, it looks to the master dataset for a column named ContactID. Because the master dataset does, indeed, contain a column named ContactID, the value of the parameter is taken from that column.

**NOTE**

You can create a detail dataset that gets only some of its parameter values from the master dataset. In this case, you must set the values of the other parameters manually. For example, given the SQL statement SELECT * FROM ACTIVITIES WHERE (ContactID = :ContactID) AND (SCHEDULED > :Earliest), the detail dataset would get the value for the ContactID parameter from the master dataset. You would make a call to sqlActivities.ParamByName to set the Earliest parameter.

As you scroll through the master dataset, the detail dataset automatically updates itself to stay in sync with the master.

Listing 2.3 shows the complete source code for an application that makes use of parameterized queries, master/detail relationships, and BLOB fields.

**LISTING 2.3** Advanced—MainForm.pas

```
unit MainForm;

interface

uses
  Types, SysUtils, Variants, Classes, QGraphics, QControls, QForms,
  QDialogs, DBXpress, DB, SqlExpr, QStdCtrls, QComCtrls, QExtCtrls, FMTBcd,
  QDBCtrls;

type
  TfrmMain = class(TForm)
    pnClient: TPanel;
    pnBottom: TPanel;
    btnConnect: TButton;
    btnDisconnect: TButton;
    Label1: TLabel;
    DBImage1: TDBImage;
    DBText1: TDBText;
    Label12: TLabel;
    Label13: TLabel;
    Label14: TLabel;
    Label15: TLabel;
    Label16: TLabel;
    Label17: TLabel;
    Label18: TLabel;
    Label19: TLabel;
    DBText2: TDBText;
    DBText3: TDBText;
    DBText4: TDBText;
    DBText5: TDBText;
    DBText6: TDBText;
    DBText7: TDBText;
    DBText8: TDBText;
    DBText9: TDBText;
    DBNavigator1: TDBNavigator;
    Bevel1: TBevel;
    Label10: TLabel;
    lvActivities: TListView;
    Label11: TLabel;
    bcCountry: TComboBox;
    btnRetrieve: TButton;
    conn: TSQLConnection;
    sqlContacts: TSQLDataSet;
    sqlContactsFIRST: TStringField;
    sqlContactsLAST: TStringField;
    sqlContactsDEAR: TStringField;
    sqlContactsTITLE: TStringField;
    sqlContactsCOMPANYNAME: TStringField;
    sqlContactsADDRESS1: TStringField;
    sqlContactsADDRESS2: TStringField;
    sqlContactsCITY: TStringField;
    sqlContactsSTATE: TStringField;
    sqlContactsPOSTALCODE: TStringField;
    sqlContactsCOUNTRY: TStringField;
    sqlContactsPHONE: TStringField;
    sqlContactsFAX: TStringField;
    sqlContactsCELLULAR: TStringField;
    sqlContactsPAGER: TStringField;
    sqlContactsEMAIL: TStringField;
    sqlContactsIMAGE: TBlobField;
    sqlContactsNOTES: TMemoField;
    DataSource1: TDataSource;
    sqlActivities: TSQLDataSet;
    sqlActivitiesCONTACTID: TIntegerField;
    sqlActivitiesDESCRIPTION: TStringField;
    sqlActivitiesSCHEDULED: TSQLTimeStampField;
    sqlActivitiesCOMPLETED: TSQLTimeStampField;
    sqlContactsCONTACTID: TIntegerField;
    sqlActivitiesTODOID: TIntegerField;

    procedure btnConnectClick(Sender: TObject);
    procedure btnNextClick(Sender: TObject);
    procedure btnDisconnectClick(Sender: TObject);
    procedure btnRetrieveClick(Sender: TObject);
    procedure connAfterDisconnect(Sender: TObject);
    procedure connAfterConnect(Sender: TObject);
    procedure FormClose(Sender: TObject; var Action: TCloseAction);
    procedure sqlContactsAfterScroll(DataSet: TDataSet);

  private
    { Private declarations }
  public
    { Public declarations }
  end;
```
