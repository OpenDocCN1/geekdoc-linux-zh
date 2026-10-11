
## No Wizards for Me!

Before we move on to the next step, I want to touch on the subject of creating a table in design view. There’s no question that using the wizard is by far the easiest way to do this, but using the design view isn’t much more difficult. It does have the advantage of giving you greater control over the format of your tables, but you have to think about what fields you want, and what you want those fields to look like (see Figure 16-11). In that respect, I recommend it only if you already have some experience in database and table design.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_311_0.png)

## Creating Mailing Labels

Now that we have this great database of names, let’s create a sheet of mailing labels. We do this with Writer, the word processor I covered in Chapter 13, but not with OpenOffice.org Base.

To begin, click **File** on the OpenOffice.org menu bar, and select **Labels** from the **New** submenu. You don't have to be running Writer to do this. Any OpenOffice.org application is a perfect starting point for creating labels. A few seconds after making your selection, the Labels dialog appears (see Figure 16-12).

![](img/0e9cf4c65a042f4a9bea644dc50153a7_312_0.png)

**Figure 16–12** When creating a new sheet of labels, OpenOffice.org starts by asking you about the data source.

Start by looking on the right, under the **Database** heading. This is where registering the database, that little step we did at the beginning, pays off. OpenOffice.org Writer already knows about the various databases and can pick my **Mailing List** database from the drop-down list. Below that is another drop-down list labeled **Table**. Click here and select the table from which you will be pulling the information you need. At the bottom of the dialog, you can select the **Brand** label (for example, Avery Letter Size) and the **type** (for example, 5961 Address).

To the left, below **Label Text**, is where we build the label we will be printing. At this moment, there are no fields visible there. Look again to the right to the Database Field drop-down list. Click that list and you see all the fields that make up the records in your table. Select the Database Field you want, and then click the large arrow directly to the left. The field you selected appears in the Label Text window. Put a space after the field name, then select the last name, and click the arrow again. Press <Enter> to go to the next line in the Label Text window. Next is the address, city, and so on. You may want to put a comma between the city and province (or state). Line by line, transfer the fields that you want to have appearing in your finished label (see Figure 16–13).

![](img/0e9cf4c65a042f4a9bea644dc50153a7_313_0.png)

**Figure 16–13** As you select fields, they appear in the Label Text window to the left.

Before we move on, let's quickly have a look at the other two tabs, Format and Options. The Format tab allows you to fine-tune your label dimensions. This includes margins, columns, rows, and pitch. If you selected one of the commercial labels from the list, this information will be filled in for you and you shouldn't have to worry about changing anything. Use the Options tab to select whether you are printing a full page of labels or a single label. The most interesting item here is a check box labeled Synchronize Contents. Check this box and you can edit a single label and synchronize the contents of all other labels with a click.

Go back to the Labels tab and click New Document to create your label document. Each label is pre-created with the field labels you selected in the proper place. At this stage of the game, there are no names or addresses in any of the labels, just the data fields. To populate these labels from your Mailing List database, you need to tell the new document where to get its information. To do that, click View on the menu bar and select Data Sources (you can also just press <F4>). The top part of your label document now shows the databases and tables available. Make sure you select the Addresses table from the database list. When you do, the records in that table appear in the right side of the data sources pane (see Figure 16-14).

![](img/0e9cf4c65a042f4a9bea644dc50153a7_314_0.png)

**Figure 16-14** The data source for the labels appears directly above the actual label document, in the top-right pane.

To populate your label document, you should now select which records you want included from the Table view at the top right. The easiest way to select them all is to click the button to the left of the top record, press the <Shift> key, then click the last record. You can also select individual records by holding down the <Ctrl> key and clicking the records you want. When you have made your selections, look at the secondary icon bar, directly above the data sources. There's a button fourth from the right that displays a Data to Fields tooltip if you pause your mouse over it (see Figure 16-15).

![](img/0e9cf4c65a042f4a9bea644dc50153a7_315_0.png)

Click the Data to Fields button and your document is instantly populated with all of the selected records (see Figure 16-16). You can save this document for later use or you can print the page using your chosen label stock.

## Further Exploring

In this chapter, I introduced you to the basics of using OpenOffice.org Base and showed you how to use the database tables in a word processing document. Obviously, this is just the beginning. Using Base, you can create custom forms for data entry. Wizards make this easy but there is a manual forms creator as well. Simple or complex custom reports are also easily generated using the Report Wizard. You can perform queries, connect to external databases, build indexes, and more. OpenOffice.org Base provides useful database access tools for users at every level.

# Chapter 16 OpenOffice.org Base

![](img/0e9cf4c65a042f4a9bea644dc50153a7_316_0.png)

**Figure 16-16** With a click, all of the selected record data is transferred to the label form.

## Resources

BASE Home Page  
http://www.openoffice.org/product2/base.html

# **Chapter 17**  
# Digital Art  
## with the GIMP

![](img/0e9cf4c65a042f4a9bea644dc50153a7_317_0.png)

*Oddly enough, Linux applications that allow users to work with graphics are among some of the most highly developed in the world. To see the truth in this rather bold statement, turn your eyes to Hollywood. Blockbusters such as Titanic, Star Trek: Nemesis, Shrek, and others use Linux and Linux clusters to create the complex special effects.*

In terms of graphical design and photo editing, your Linux system comes with one of the most powerful, flexible, and easy-to-use packages there is, regardless of what OS you are running. It’s called the GIMP. Allow me to introduce you to some of its many features.

The GIMP is one of those programs that has helped create an identity for Linux. Of course, there are plenty of programs out there, as I’m sure I have demonstrated in the book, but the GIMP is special in some ways. The Linux community has used it to create images, buttons, desktop themes, window decorations, and more. Even the Linux mascot, Tux the Penguin, as created by Larry Ewing (the mascot’s best-known incarnation), was a product of the GIMP.

The GIMP is an amazingly powerful piece of software, yet its basic functions are easy-to-use as well. With a little bit of work, a lot of fun, and a hint of experimentation, anyone can use the GIMP to turn out a fantastic piece of professional quality art. You doubt me my words? Then follow along with me, and in just a few minutes, you’ll create a slick-looking logo for your Web page or your desktop. With time and practice, you may learn to wield the GIMP with the power of a Hollywood special effects master.

Play. Experiment. And don’t be afraid.

## Ladies and Gentlemen, Start Your GIMP

Click the Application menu on the top panel and select GIMP Image Editor from the Graphics submenu. You can also use your program quick-start by pressing <Alt+F2> and entering gimp into the command field.

When you run the GIMP for the first time, you will get a couple panels, aside from the GIMP’s main screen. You will also likely get the GIMP Tip of the Day. As with all such tips, you can elect not to have them appear each time the program starts—just uncheck the Show Tip Next Time GIMP Starts button before you hit Close, and you aren’t bothered with them again. What you are likely to see (minus that tip of the day) should look a bit like Figure 17-1.
