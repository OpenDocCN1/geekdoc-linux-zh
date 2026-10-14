
![](img/afd38ba98c33e56aa8435c9f1db6bed0_42_0.png)

## OpenOffice.org – Base

### 3 OpenDocument format

All databases in Base are actually just files, so they need to be stored somewhere on your computer. In common with the other OpenOffice.org applications, Base uses OpenDocument format by default. Save your database as cdcollection in your documents folder.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_42_1.png)

### 4 Start work

And now you’re in – Base has created the database and you’re ready to start working. Along the side are the four main views: Tables, Queries, Forms and Reports. Tables are where all your data is stored, so click that tab now.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_42_2.png)

### 5 Ignore wizard

In the Table tab there are three links at the top that are important: Create Table In Design View, Use Wizard to Create Table, Create View. The second option might sound easier, but it’s a bit long-winded – just click Create Table In Design View for now.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_42_3.png)

### 6 Table design views

This is the table design view. It’s split into three columns: the name of your fields, the type of data they hold, and their description (you can ignore that last one). Field names are things like First Name, Address, etc.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_42_4.png)

### 7 First four fields

Type these names into the first four fields: ID, Name, Artist and Rating. By default, Base will set these to have the TEXT [VARCHAR] data type, which means it holds variable-length text. That is, Name could hold “Hello” or “Supercalifragilistic-expialidocious”.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_42_5.png)

### 8 Set Integer

Click the field type for ID and set it to Integer [INTEGER]. This holds whole numbers, such as 3, 9 and 349083439. Change Rating to be Tiny Integer [INTEGER]. This holds whole numbers up to 127.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_42_6.png)

### 9 Unique numbering

That ID field will hold a number that’s unique to every CD we add to this collection, so we don’t really want to be entering it ourselves. So click that field, then look at the boxes of the bottom – change the AutoValue value from No to Yes.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_42_7.png)

### 10 Primary key

Every table should have a ‘primary key’, which is a unique value that identifies a row. For example, if you have two versions of the same album, the primary key lets you specify exactly which one you mean. Fortunately, our ID value is exactly this, so right-click on the green triangle next to the ID field and click Primary Key.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_42_8.png)

### 11 Name your table

That’s your table design done, so click the little disk in the toolbar to save your work. This prompts you to give your table a name within the database, so enter “CDs”, then click OK. Note: this is not a filename – it’s just internal to your database.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_43_0.png)

### 12 Save table

When your table is saved, you can just close the design window to get back to the main Impress window from earlier. Except now you’ll see your CDs table listed under the Tables pane. Double-click that to open it up for editing.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_43_1.png)

### 13 Table editing view

This is the table editing view, which lets you type data into your CDs table. You can resize the columns at the top to make them bigger and easier to work with, which is particularly helpful if you want to type a lot into your fields.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_43_2.png)

### 14 New row

Type "Mind Bomb" into the Name field for the first row, then "The" into Artist. Notice that Base has <AutoField> in the ID row, because that takes care of itself. You’ll also notice that it automatically creates a new row for you, so you can add more fields easily.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_43_3.png)

### 15 Save value

Now try entering "Fizz" for the rating for this CD. Once you press Enter to save the value, Base will automatically change that "Fizz" to be 0. This is because we told Base to accept a Tiny Integer value, which means it only accepts numbers -127 to 127 – not text.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_43_4.png)

### 16 Enter more data

Go ahead and type a few more fields in there so that we have something to work with. Make sure you have at least two CDs with the same rating, because we’ll be using that shortly. Remember, the ID number takes care of itself – you only need to fill in the Name, Artist and Rating fields.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_43_5.png)

### 17 Sort it out!

Once you’ve added all your data, select the Name field (do this by clicking the title "Name" above the first row), then click the toolbar button that shows an A over a Z with a down-pointing arrow. This sorts the table alphabetically by the name of the CD.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_43_6.png)

### 18 AutoFilter

Now try clicking on one of the ratings. For example, I gave Moby’s Play album 4/5, so I would click on the 4 in his row. Now click the toolbar icon marked with a funnel and a magic wand – this is the AutoFilter button. This filters by the current selection, so you’ll only see CDs with a 4/5 rating.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_43_7.png)

### 19 Hidden rows

Don’t worry – the other rows are just hidden, rather than being deleted! If you want to get back to the original view of your table, which means removing any filter or sorting, you can click the button that shows a picture of a filter with a cross over it.

![](img/afd38ba98c33e56aa8435c9f1db6bed0_43_8.png)

### 20 Deleting forever... careful!

If there’s a row you don’t want, you can delete it by right-clicking on the grey bar on its left and choosing Delete Rows. Remember, deleting a row is permanent: once it’s deleted, it’s gone forever!
