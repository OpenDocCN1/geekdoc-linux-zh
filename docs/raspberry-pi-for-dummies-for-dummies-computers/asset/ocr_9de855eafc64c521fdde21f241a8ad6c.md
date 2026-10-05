You can make a column wider so that you can easily enter the descriptions of your budget items. Click and drag the line between the letter at the top of the column and the letter at the top of the column to its right.

To show a currency sign in a cell, click the Format menu, choose Cells, and then change the category to Currency and the format to the layout and currency symbol you would like to use. You can select a group of cells and format them at the same time by clicking and dragging the cells before you go into Format menu.

You can enter formulae (or calculations) into cells, and the answers will appear in the spreadsheet. If you want to enter a formula into a cell, you type the equal sign (=), you use an asterisk (*) for multiplication and a slash (/) for division. For example, click any cell and enter

```
=7*5
```

The result (35) appears in the cell where you entered the formula. You can view or edit the formula itself by clicking the cell and then clicking the formula bar above the spreadsheet, or double-clicking the cell.

The magic happens when you start using the numbers in one cell to work out what should go in another one. You do that by using the grid reference of a cell in your formula. For the holiday budget, you multiply the cost of an item (such as a night in a hotel) by how many of them you need (six nights). The first of those values is stored in column B, and the second is beside it in column C, both on the same row. After the titles and spacing at the top of the spreadsheet, the first expense is on row 5. In column D5, you enter

This multiplies the values in cell B5 (the price) and C5 (the quantity) and puts the result (the total amount spent on that particular item) into cell D5. You can click cell D5 and then copy its contents and paste them into the cells below. There are options for copying and pasting from the Edit menu, but LibreOffice also supports Windows shortcuts, including Ctrl-C to copy and Ctrl-V to paste.

You might think the same number goes into those cells, but it actually copies the formula and not the result, and updates it for the correct row number as it goes. If you copy the formula from cell D5 into cell D6 and then click D6 and look on the Formula bar, you'll see that says

```
=B6+C6
```

CHAPTER 6 Being Productive with the Raspberry Pi 133