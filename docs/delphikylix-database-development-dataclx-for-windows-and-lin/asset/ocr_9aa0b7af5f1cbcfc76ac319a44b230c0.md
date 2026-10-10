The cdsContactsNewRecord and cdsTodosNewRecord events make a call to the local method GetNextID. GetNextID clones the dataset in question and moves to the first record in the dataset. The first record is the record with the lowest numbered ID. It then assigns the next lower number to the ID of that record, ensuring that the record has a negative primary key.

The reason this is done is to ensure that all records that have not yet been added to the database have a negative ID. The server-side data module checks for a negative ID and then calls the database' GEN ID stored procedure to assign a unique ID. This ensures that all added records receive a unique ID, regardless of what computer they were added from. (Remember that multiple users may be running this application at the same time.)

# Note

An alternative to using the cloned dataset to retrieve the next negative ID is to set up a private variable and retrieve the next ID at program startup. That way you can simply decrement the variable to obtain the next ID. The reason I don't do this is because real-world applications I sometimes have 40 or 50 datasets in my data module. I don't like to set up 40 or 50 variables— one for each dataset. Instead, I use the common function to retrieve the next ID on the fly.

Note that cloning a dataset does temporarily require a small amount of memory, and also takes a small amount of time to do. If you need to generate temporary IDs as quickly as possible, you should consider using a private variable instead.

Listing 9.5 contains the source code for the client' main form, which is where the bulk of the code for this application lies.

```
LISTING 9.5  ConMan—MainForm.pas

```pascal
unit MainForm;

interface

uses
  Windows, Messages, SysUtils, Variants, Classes, Graphics, Controls, Forms,
  Dialogs, DBActsns, StdCtrls, ActnList, ImgList, ActnCtrls, ToolWin,
  ActnMan, ActnMenus, ComCtrls, BandActn, ExtCtrls, Menus, Grids, DBGrids,
  DB, StdCtrls, OBCtrls, Mask, ExtDlgs;

type
  TFormMain = class(TForm)
    StatusBar1: TStatusBar;
    ImageList1: TImageList;
```

```