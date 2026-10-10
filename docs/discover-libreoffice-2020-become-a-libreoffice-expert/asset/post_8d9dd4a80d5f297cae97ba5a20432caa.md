
## GETTING STARTED
### LibreOffice Base

![](img/e39350c3a7c0d527d71b0e4097a0ba66_42_0.png)

change the form directly with the mouse. In the *Data* tab, choose *Input required* | No. If this is not chosen, then you must declare an image before saving. The changes will take effect by closing the *Properties* dialog.

Now *Ctrl-click* the *ID input* field and open the *Properties dialog* via *Control* in the context menu. Select *General* | *Read-only* | Yes. The field should also be uniquely recognizable, such as by using a different color scheme.

To display a list box for the *Category/ID* input field, *Ctrl-click*, then right-click and choose *Replace with* | *List Box* from the context menu. In the *Data* tab of the *Properties dialog* for the list box, change *Type of list contents* to *Sql*. Clicking the button with the three dots by *List content* (Figure 5) starts the SQL command editor, in which you will define the content of the list field.

To begin, *Add the Category table* in the *Tables* section of the *Add Table* or *Query* dialog. A new *Category* box appears with a list of its fields. A double-click on the *Category* field turns it into the first query field (field 0 in database-speak). A double-click on the *ID* field makes this the second query field (Figure 6).

Next, click *Sort* | *ascending* for the *Category* field. Closing and saving the SQL command dialog, shows the new SQL query in the *List content* drop-down. Now switch to *General* | *Drop-down* | Yes so that the list box unfolds downward. Here, you can change the number of fields shown, as well.

*Right-clicking* on *PlaceID* in the table control field (subform) opens a context menu where you can select *Replace with* | *List Box*. Open the *PlaceID* context menu again and start with the *Column* properties. As before, the list content should be created in the SQL command query editor, where you *Add* the *Place* table. Now, double-click, one after another, *Room*, *Cupboard*, *Rack*, and *ID*. For further editing of the query, click the *Switch Design View On/Off* icon to view the SQL code (Figure 7):

```sql
SELECT "Room", "Cupboard", "Rack", "ID" FROM "Place"
```

The command would display all fields of the table separately in the order shown. A list field, however, can only display one field and only save the value of another field; therefore, the content of the first three fields has to be combined:

```sql
SELECT "Room" || "Cupboard" || "Rack", "ID" FROM "Place"
```

Now the *Room*, *Cupboard*, and *Rack* fields are shown one after another in one field. On the other hand, the value of *ID* is saved in the form, which is not optimal for displaying within a list box.

Changing the SQL command to

```sql
SELECT "Room" || ' - ' || "Cupboard" || ' - ' || "Rack" AS "", "ID" FROM "Place" ORDER BY ""
```

separates *Room*, *Cupboard*, and *Rack* fields with spaced dashes and assigns an alias with the `AS` statement, which is used to sort the content of the list box. Close and save the SQL command editor and the *Properties* box before continuing.

For the final modification, right-click *ArticleID* in the control table and select *Delete column* in the context menu. Although the form is now ready to use, the field sizes still need to be modified, and you can change the *CategoryID* and *PlaceID* labels, as well.

Navigating through the form, searching for data records, and so on can take place in the *Navigation Bar* at the bottom of the screen (Figure 8), which shows up automatically once data has been entered.

Sometimes a separate navigation bar next to an input field is desirable.

![](img/e39350c3a7c0d527d71b0e4097a0ba66_42_1.png)

![](img/e39350c3a7c0d527d71b0e4097a0ba66_42_2.png)

![](img/e39350c3a7c0d527d71b0e4097a0ba66_42_3.png)

To create this, you need to open the form for editing again. First click on a field in the main form and then on the *More Controls* icon toward the bottom of the left sidebar. By Ctrl-clicking *Navigation Bar* in the new controls, a new Navigation Bar appears in the form that contains nearly all the same fields as the Navigation Bar at the bottom of the screen.

## SEARCHING DATASETS

Base itself has a few search functions built in. Unfortunately, these functions are more difficult to manage while using a form. To change this, you have to go slightly deeper, where basic knowledge of *SQL* code is a must. For general help, you can refer to the downloadable Base manual.

To begin, create another table in which to save the search term with *Tables | Create Table in Design View* and add the fields:

- *ID* as *Yes/No* [BOOLEAN]
- *Search* as *Text* [VARCHAR]

Right-click the *ID* field to make it the primary key and save the table with the name *Search*. Insert "ID" = *true* in the first row of the table. This table should only save this one data set.

Open *Queries | Create Query in SQL View*, to enter code more quickly than in *Design View*, and type:

```sql
SELECT * FROM "Article"
WHERE "Article" LIKE COALESCE
(
  (SELECT "Search"
   FROM "Search"
   WHERE "ID" = TRUE
  ), "Article"
)
```

![](img/e39350c3a7c0d527d71b0e4097a0ba66_43_0.png)

Figure 9: The Form Navigator shows all the elements of a form.

The *COALESCE* function checks whether *Search* is empty; however, if *TRUE*, *Article* and *Article* should always have content and *Article* should always have the same as *Article*, this word now shows all *Article* table data. If a word is entered in *Search*, only *Article* items that match the entered value are shown. This query has to be improved a bit so that also parts of the search entry show results:

```sql
SELECT * FROM "Article"
WHERE "Article" LIKE COALESCE
( '%' ||
  (SELECT "Search"
   FROM "Search"
   WHERE "ID" = TRUE
  ) || '%', "Article"
)
```

To test the query, click the *Run Query* icon in the toolbar or press *F5*. All the data sets from the *Article* table are shown. The last line displays *AutoField* in the *ID* field.

Amend the code to look in the *Search* table for an entry with the value *Search* and compare it to the *Article* field in the *Article* table:

```sql
SELECT * FROM "Article"
WHERE "Article" LIKE
(
  SELECT "Search"
  FROM "Search"
  WHERE "ID" = TRUE
)
```

You will probably not see any values now, because the content of the *Search* field in the table *Search* is empty. Amend the code again to:

![](img/e39350c3a7c0d527d71b0e4097a0ba66_43_1.png)

Figure 10: Cycle only through the active record – no navigation bar, no new rows, ...

By using *%*, the hits on the search term can now contain any number of characters before and after the term. One input can therefore get multiple hits. The only downside is that it still distinguishes between lower- and uppercase. The following query now allows the entry of text contained somewhere in the *Article* field, regardless of upper- and lowercase:

```sql
SELECT * FROM "Article"
WHERE LOWER ( "Article" ) LIKE COALESCE
( '%' ||
  (
    SELECT LOWER ( "Search" )
    FROM "Search"
    WHERE "ID" = TRUE
  ) || '%', "Article"
)
```

Now save this query as *qrySearchArticle*, copy the form already created under Forms, paste the copy as a new form named *ArticleSearch*, and open this new form for editing by right-clicking and choosing *Edit*.

![](img/e39350c3a7c0d527d71b0e4097a0ba66_43_2.png)

Figure 11: Form with search function. Nine records were found with content *Meter*.

To add a *Search* input area to the existing form, you need to open the *Form Navigator* (Figure 9). In the dialog that opens, right-click *Forms* and choose *New | Form*. A new form is then added next to *MainForm*.

Open the properties of this form via its context menu. In the *Data* tab, choose *Search* in the *Content* drop-down. It is especially important to select *Cycle | Active record*. The remaining settings shown in Figure 10 ensure that the same data set, always, is edited and changed.

Next, select one of the available form fields in *MainForm* and bring up its *Properties* dialog, and have set in *Properties* | *General* | *Action* | *Refresh form*.

After closing the new form's *Properties* dialog, select *MainForm*. In the *Data* tab, select *Content type* to *Query* and *Content* to *qrySearchArticle*. Next, *Ctrl-click* the *Push Button* icon in the sidebar. This button should appear in *MainForm* (check the *Form Navigator*). In the button's *Properties* dialog in the *General* tab, choose *Action* | *Refresh form*. Now, with every click on this button, the form will be scanned again.

In the *Form Navigator*, select the new form for the *Search* table again and create an input area by choosing the *Text Box* icon and using the mouse to draw a box. Set *Data field* to *Search* and *Input required* to *No* in the *Data* tab of the *Properties* dialog for this box. The contents of this text field will now be saved automatically when the button in *MainForm* is clicked (Figure 11).

If you are happy with the form and do not want to make any design changes, you can save it now.

## CONCLUSION

At first, creating an internal Firebird database takes a lot more time than creating a table in Calc, but once the database is constructed, the data entry is a lot more accurate and fast than entering data in a spreadsheet. A further advantage is the possibility of generating reports.

Base also lets you connect to external databases (e.g., MySQL/MariaDB, PostgreSQL, e-mail address books, etc.) beyond the Base internal databases. Base then merely accesses the tables and provides a graphical user interface.

Because Base can access so many databases, a basic knowledge of SQL is always an advantage. Otherwise, access is limited very quickly to databases that comprise a single table and use only the built-in search functions of Base.

## INFO

- [1] LibreOffice Getting Started Guide: https://documentation.libreoffice.org/en/getting-started/getting-started-guide/
- [2] Base Handbook: https://documentation.libreoffice.org/en/documentation/base/

# IT Highlights at a Glance

![](img/e39350c3a7c0d527d71b0e4097a0ba66_44_0.png)

![](img/e39350c3a7c0d527d71b0e4097a0ba66_44_1.png)

Too busy to wade through press releases and chatty tech news sites? Let us deliver the most relevant news, technical articles, and tool tips – straight to your Inbox.

- • Linux Update • ADMIN Update • ADMIN HPC

Keep your finger on the pulse of the IT industry.

- ADMIN and HPC: bit.ly/HPC-ADMIN-Update
- Linux Update: bit.ly/Linux-Update
