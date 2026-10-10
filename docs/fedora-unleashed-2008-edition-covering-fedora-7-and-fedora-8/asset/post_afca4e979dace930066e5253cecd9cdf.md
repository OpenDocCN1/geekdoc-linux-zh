
vastly more expensive rival. In this section, you learn how to get started with Writer and make use of some of its powerful formatting and layout tools.

# NOTE

You might be interested to know that Writer was the primary word processor chosen to write and edit this book.

# Getting Started

You can access Writer either through its shortcut on the panel or by going to the Applications, Office menu and selecting Word Processor. After a few seconds, Writer opens with a blank document and a blinking cursor awaiting your command. It can be tempting to just dive in and start typing your document, but it can be worthwhile to do some initial configuration before, so you are properly prepared for work.

First of all, make sure that the options are set to your requirements. Click the Tools menu and select Options to bring up the Options dialog box, as shown in Figure 6.2. The initial screen enables you to personalize OpenOffice.org with your name, address, and contact details, but there are options to configure features that you might also want to alter. First of all, check that your default paths are correct by clicking the Paths option. You might want to alter the My Documents path, as shown in Figure 6.3, to something a little more specific than just your home directory.

![](img/34e72348d53ca54c2a1d9c871316691b_159_0.png)

FIGURE 6.3 Click the Edit button to choose your default documents directory.

You might also want to change OpenOffice.org so that it saves in Microsoft Word format by default, should you so require. This can be done under the Load/Save General options shown in Figure 6.4, and it is a good idea if you value your work to change the Autorecovery settings so that it saves every couple of minutes.

![](img/34e72348d53ca54c2a1d9c871316691b_160_0.png)

**FIGURE 6.4** Make sure that you are working with most appropriate file formats for you.

Also shown in Figure 6.4 is a set of options that are specific to Writer. From top to bottom, they are

- **General**—Specify options that affect the general use of Writer.
- **View**—Specify what you want Writer to display.
- **Formatting Aids**—Specify whether you want to see nonprinting characters.
- **Grid**—Create a grid that you can use to snap frames and images in place.
- **Basic Fonts**—Select your default fonts for your document here.
- **Print**—Specify exactly what you want Writer to output when you print your document.
- **Table**—Set options for drawing tables within Writer.
- **Changes**—Define how Writer handles changes to documents.
- **Compatibility**—A set of rules that Writer uses to ensure close compatibility with earlier versions of Writer
- **AutoCaption**—Create automatic captions for images, charts, and other objects.

A little bit of time working through these options can give you a highly personalized and extremely productive environment.

# Working with Styles and Formatting

One of the significant benefits of using Writer is the ability you have to easily apply formatting and styles to extremely complex documents. Depending on the types of documents you work with, you might want to consider creating your own styles beyond the 20 included by default. You can access styles through either the Style drop-down box in the toolbar or the Styles and Formatting window shown in Figure 6.5. If you cannot see the window, press the F11 key to display it.

The easiest way to work with the Styles and Formatting tool is to highlight the text you want to style and double-click the required style in the window. There are quite a few to choose from, but you might find them restrictive if you have more specialized needs. To start defining your own styles, press Ctrl+F11 to bring up the Style Catalog, shown in Figure 6.6, where you add, modify, and delete styles for pages, paragraphs, lists, characters, and frames.

![](img/34e72348d53ca54c2a1d9c871316691b_161_0.png)

FIGURE 6.5  Writer's quick and easy-to-use Styles and Formatting tool.

![](img/34e72348d53ca54c2a1d9c871316691b_161_1.png)

FIGURE 6.6  Writer's powerful Style Catalog gives you control over every aspect of styling.

# Working with OpenOffice.org Calc

The spreadsheet component of OpenOffice.org is named Calc, and is a very capable Excel alternative.

Calc is used for storing numeric information that you need to analyze in some way. So, for instance, you could use it to help you budget month by month. It can take care of the calculations for you, as long as you tell Calc what you want it to do. Anyone with experience in Excel will feel right at home with Calc.

In this section, we show you how to get started with Calc, including entering formulas and formatting. We also take a look at some of the more advanced features of Calc, including the Data Pilot feature, which allows you to easily summarize information.

## Getting Started

You can either click the shortcut icon that is located on the top GNOME panel, or select Spreadsheet from the Office menu under the Applications main menu. Whichever route you take, the result is the same and Calc starts to load.

By default, Calc loads with a blank spreadsheet just waiting for you to enter information into it. In Figure 6.7, you can see that we have already started to enter some basic information into Calc.

![](img/34e72348d53ca54c2a1d9c871316691b_162_0.png)

Calc's layout makes it easy to organize information into rows and columns. As you can see in the example, we have salespeople listed in the left column, customers in the second column, invoice date in the third column, and finally revenue in the fourth column. At the moment, no formulas are entered to help you interpret the data. Clicking the E43 cell selects it and enables you to enter in a formula in the top formula bar. If you enter in the equal sign, Calc knows that you are entering a formula and works accordingly.

In this example, we want to know the total revenue brought in up to now, so the formula to enter is **=sum(E4:E42)**, followed by Return. Calc automatically enters the result into cell E43 for you to see. Now you want to see what the average order value was. To do this, you have to obtain the number orders made. For this, you can use the **counta** function to count the number of entries in a given list. This is usually used when you need to find out how many entries there are in a text list. So, in cell B43, enter **=counta(B4:B42)** and press Enter. Calc now counts the number of entries in the range and returns the total in B43. All that remains for you to do is divide the total revenue by the number of orders to find the average order value. So, in cell E44, enter the formula **=E43/B43** to get the average order value.

> **TIP**
> Calc offers some nifty little features that you can use quickly if you need to. The handiest one in our opinion is the capability to select multiple cells and see immediately the total and average of the range. You will find these figures in the bottom-right status bar. This has saved us numerous times when we have needed to get this information quickly!

## Formatting Your Spreadsheets

Getting back to our example, it looks a little basic at the moment as there is no formatting involved. For instance, what's the billing currency? You can also see that some of the cells have text that does not fit, which is highlighted by a small right arrow in the cell. We should also add some labels and titles to our spreadsheet to make it a bit more visually appealing.

To start off, all the revenue figures can be changed into currency figures. To do this, select all the cells containing revenue information and click the small icon shown in Figure 6.8. This immediately formats the cells so that they display the dollar sign and also puts in a thousands separator to make the numbers easier to read.

Now you need to space all the cells so that you can read all the information. A quick and easy way to do this is to click the area immediately to the left of column A and immediately above row 1 to select the entire spreadsheet. Now all you have to do is double-click the dividing lines and each column resizes according to its longest entry.

Next you can add a little color to the worksheet by using the Paint Can icon in the toolbar. Select the range B3 to E3 with the mouse cursor and click the background fill icon to bring up the color window shown in Figure 6.9. Now select the color you want to use and Calc fills the cells with that color. You can also change the font color by using the icon immediately to the right in the same way.
