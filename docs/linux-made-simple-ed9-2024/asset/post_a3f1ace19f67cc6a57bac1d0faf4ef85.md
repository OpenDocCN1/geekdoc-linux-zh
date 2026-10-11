
## Calc: Super spreadsheets

We've worked with words, now it's time to keep your numbers in check using Linux's premier spreadsheet, LibreOffice Calc.

![](img/420a7272a6efa239082a35eeadd9bc1d_49_0.png)

- If something goes wrong, you may be presented with an unintelligible error code. Highlight it and look at the bottom right of the Calc window to see what it means.

Here would we be without spreadsheets? Either considerably poorer or considerably richer, most likely. Whichever is true, there comes a time when we all need to put numbers in a grid. You're probably familiar with Microsoft’s Excel, which rules the spreadsheet root over on Windows. On Linux there are, as ever, plenty of options, but we lean towards the well-honed spreadsheeting machine that is *LibreOffice Calc*. It should come preinstalled with your Linux distribution, but if it's nowhere to be found you'll need to install it – as part of the main *LibreOffice* package – from your distribution's package manager. In the case of Ubuntu 15.10, you'd use *Ubuntu Software Centre*. We're looking at *LibreOffice 5* for this tutorial, but if you have an earlier version you'll be fine to follow along.

As with *LibreOffice Writer*, running *Calc* for the first time should bring up a reasonably familiar environment. There's a standard grid of cells, menu bars at the top of the screen, below them the input line, and an area below the sheet where different pages can, once they're created, be accessed.

Realistically the way you use it is no different than you might have previously used *Excel*. Even the syntax is the same. But if you're unfamiliar, or if you need a refresher, let's create a sample spreadsheet to see what we can do with *Calc*.

### Numerous numbers

Let's start with a little housekeeping. Usually the leftmost and topmost cells – row 1 and column A – are used as labels to signify the contents of the cells they're next to. Fill in a bunch of sample labels – it doesn't matter what you type, we're merely playing with some of the features – by clicking in each of these edge cells and typing. You can use the arrow keys to navigate between them, which makes the process a bit quicker. You can also hover your mouse cursor over the bold dot in the corner of a cell and drag it to automatically copy the contents of that cell to those that you highlight. Fill in labels from A2 to A20 and from B1 to L1, leaving cell A1 empty – it's useless when we're laying out a spreadsheet like this.

Larger spreadsheets than ours may have content which goes further than your screen can easily display, so it's good practice to isolate the label columns in their own pane. On the right of the screen, just above the scrollbar, you'll see a small horizontal line – drag it downwards until the top pane shows just the labels, and do the same for the small vertical line to the right of the bottom scrollbar. Hover your mouse over the icons on the right hand side of the top row of toolbars until you find the one labelled 'Freeze panes'. Click it, and your labels will be neatly locked in place.

Now it's time to fill in some data! But let's use one of *Calc*'s features to generate our own random data to play with, rather than using anything useful. Click and drag over cells B2 to L20 to select them, then head to Edit > Fill > Random Number. You'll see your chosen cell range has been automatically inserted in the topmost box. We now need to choose what kind of random number to generate, and its range. By default it'll be a floating point number, although you can change the distribution to *Uniform Normal* if you want to make a whole number. We'll stick with *Standard Uniform* for now, as it will allow us to demonstrate a further function later on. Leave the *minimum* at 0.000 and change the *maximum* to 9.0000. Click 'Apply' and you'll have a nicely filled in spreadsheet.

### Function room

Time to crunch those numbers a bit. The most basic spreadsheet function is a sum, which performs basic arithmetic on a group of cells. Let's start by adding the first column of numbers together. Click below it in cell B2, type =SUM( then click and drag your mouse over the numbers in the column above. Pointers to the first and last cells will be added, with a colon between to indicate a cell range. Close the brackets with a ) then hit [Enter] to see the total of all the numbers in that column.

![](img/420a7272a6efa239082a35eeadd9bc1d_49_1.png)

You can format the numbers in your cells any way you like without affecting the original values. Try representing floating point numbers as fractions!

Let’s try some different functions. In the next cell to the right, we’ll use SUMIF to add together all the numbers over 5. Type =SUMIF(C2:C80,“>5”) – the semicolon divides the cell range with the criteria for the sum, and remember to include quote marks around your criteria. In the next cell along, let’s take an extra course. Typing =SUMIF(D2:D20,“>6”,C2:C20) adds an extra clause: it’ll add together only the numbers in column D which lie next to numbers in column C which are greater than 5.

You can duplicate formulas (and automatically move their range of cells) in the same way that we earlier duplicated labels, by selecting their cell and dragging its bottom right corner. But for now, try replacing SUM and SUMIF with the following in subsequent columns: AVERAGE, MAX, PRODUCT, STDEV. And why not try creating functions using the totals we’ve already generated? The output of a function is just a value after all.

### Simple science

Presentation is everything if you’re handing off a spreadsheet to someone and you actually want them to understand it, so let’s do a little sprucing up. We’ve filled our spreadsheet with a lot of long numbers, but there’s a way of rounding them without losing the original granularity of the data. To prove it, select your original range of data (B2 to L20) and go to Format > Cells. Select ‘Number’ in the category box, and change the Number of decimal places to ‘0’ and hit OK. You’ll see everything reduced to whole numbers visually, but the formula line below won’t change to match because it’s still working on the actual values stored within the cells. Clicking each cell will display its actual contents (rather than its formatted contents) in the input line at the top of the Calc window. You can also use cell formatting to turn numbers into currency values, force them to be text values (which can’t be worked on with formulas) and apply fonts and borders.

A quick thing you should know before we sign off: you can create a new sheet within the same document by clicking the plus sign at the bottom left of the Calc window, and within it you can refer to cells from the first sheet by using the syntax ‘<sheet name>.<cell>’. So to sum the first column of the first sheet in a cell on the second, you’d use =SUM(Sheet1.B2:Sheet1.B20) – and you can, of course, use this technique to work with, and apply formulas to, numbers stored on multiple sheets.

- **Quick tip**: Calc can, like Writer, save documents in a format compatible with Microsoft products. We’d recommend you choose .xls for maximum compatibility.

### Cracking the Calc code

![](img/420a7272a6efa239082a35eeadd9bc1d_50_0.png)

#### Colour up
Calc features standard the standard formatting tools you’d expect, so you can change fonts, sizes, colours and more.

#### Cell mate
The currently selected cell is always shown here – bear in mind that you can use the arrow keys to navigate between cells rather than clicking.

#### What a pane
Locking your panes like this gives a clean look and means your labels will always stay in place no matter where you are in the document.

#### Line up
You can type directly into cells, but it’s often useful to use the input line, which always reflects the content of the cell.

#### Extended play
If all of the icons on your toolbar don’t fit on the screen, click the small arrow double icon on the right to display an expanded menu like this one.

![](img/420a7272a6efa239082a35eeadd9bc1d_50_1.png)

Random numbers can be inserted into cells, but you’ll need to understand how, for example, Bernoulli numbers work to get them to work.
