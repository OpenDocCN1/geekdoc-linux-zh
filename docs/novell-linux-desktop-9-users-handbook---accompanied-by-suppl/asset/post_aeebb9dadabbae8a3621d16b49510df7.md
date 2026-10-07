
# TIP

You can also drag to copy a formula or function. For example, if you have several like ranges of numerical values in rows, you can use Sum to compute the first total and then drag the Sum function to the other cells to compute their totals. The Sum function is actually copied using the autofill handle, and it adjusts to the new row values, giving you the correct total for each range of numbers.

# 115 Enter Dates

Although dates appear as dates (August 11, 2005, for example) in your Calc sheets, these dates actually have numerical significance. For example, you might need to calculate the number of days between two different dates. You can actually subtract the earlier date from the later date and be provided the number of days that they differ.

The date is actually seen by Calc as a numerical value; so when you enter 11/22/2005, you see it as a date, but Calc sees it as a number—the number of days that have elapsed since January 1, 1900. So, Calc sees 11/22/2005 as 38,678.

- 1 Enter Date

In Calc, click on a cell that will hold a date. Type the date; you can enter the date as November 22, 2005 or as 11/22/2005. Press Enter.

- 2 Open Format Cells Dialog

You can change the format (appearance of the date). Select a cell or cells containing dates and then select Format, Cells. The Format Cells dialog box opens.

- 3 Format Date

The Numbers tab of the dialog box will be selected. Select a format for the date in the Format list. After you have completed your selection, click OK.

# CHAPTER 12: Creating Spreadsheets with OpenOffice.org Calc

![](img/6e85ebc4ce06a64c82109523b60183ba_295_0.png)

115 Enter Dates

# 116 About Creating Formulas

Calc is designed to do calculations. Although many built-in formulas and functions are provided by Calc, in some situations you will need to build your own formulas. These formulas typically involve simple math operations such as subtraction, multiplication, and division.

All formulas that you create must begin with the equal sign (=). This tells Calc that the information that follows the equal sign is a formula. To designate the type of calculation you want Calc to perform you use a mathematical operator (see Table 12.1).

TABLE 12.1. Mathematical Operators

| OPERATOR | PERFORMS | EXAMPLE |
|---|---|---|
| + | Addition | =A1+B1 |
| - | Subtraction | =A1-B1 |
| * | Multiplication | =A1*B1 |
| / | Division | =A1/B1 |
| ^ | Exponentiation | =A1^2 |

You enter the cell addresses for the cells that will be acted on by the formula. For example, B5*C5 multiplies the contents of B5 times the contents of C5.

When you design your own formulas, keep the natural order of math operator precedence in mind: Exponents are computed first, then multiplication and division, followed by addition and subtraction. To force the precedence you can place portions of your formula in parentheses. This part of the formula is computed first.

# Create a Formula

Calc makes it easy to add simple formulas in your spreadsheet.

- BEFORE YOU BEGIN
- About Creating Formulas

# Start Formula

Select the cell that will contain the formula. Type an equal sign (=) or select the Function button (the big equal sign on the Formula bar).

# Select Cell

Select the first cell that will be included in the formula (selecting the cell is better than typing the cell address because it avoids typos). The cell address appears in the cell where you are creating the formula.

# Enter Operator and Select Second Cell

Type the operator for the formula. For example, type an asterisk (*) for multiplication. Then select the second cell that will be acted on by the formula. Press Enter to complete the formula. The results of the formula appear in the cell where you built the formula. Select the cell and view the formula on the Formula bar's Input line.

# TIP

After you create the formula, you can use the autofill feature to copy the formula to other cells or use Copy and Paste to copy the formula to other cells.

# CHAPTER 12: Creating Spreadsheets with OpenOffice.org Calc

![](img/6e85ebc4ce06a64c82109523b60183ba_297_0.png)

# 118 About Calc Functions

Functions are built-in formulas that can do everything from add a range of values to provide an average for a range of cells to figure out the payment amount for a loan at a particular interest rate. Functions consist of two parts: the function name (such as =Average) and the range of cells that the function should act on. Calc provides many functions broken down into different categories (see Table 12.2). A statistical category includes functions such as average, maximum, and minimum. A financial category provides functions that allow you to calculate returns on investment and loan payment amounts among other finance-related calculations.

# TABLE 12.2 Some of the Calc Function Categories

| CATEGORY | EXAMPLE | PURPOSE |
|---|---|---|
| Date and Time | TODAY | Enters the current date |
| Financial | PMT | Calculates loan payments |
| Logical | IF | Returns a true or false |
| Mathematical | COS | Calculates the cosine of an angle |
| Statistical | AVERAGE | Calculates the average for range |

The easiest way to specify the function is the AutoPilot. The AutoPilot dialog box allows you to select the function. The AutoPilot provides information about the function. You can use the various formatting options on the Object bar. The AutoPilot also helps you specify the function for the range.

# Use Format Cells

- Use AutoPilot
- Use Format Cells

- BEFORE YOU BEGIN
- About Calc Functions

# Select Cell Range

- Select the cell that will contain the function.
- Select the function from the AutoPilot on the right.

# Select Function

- Select the function from the dropdown list.
- Select the range of cells you want to format.
- The AutoPilot dialog box opens.

# Shrink AutoPilot

- Select the range of cells to highlight the function.
- Select the range of cells.
- After you have selected your options, click OK.

# Enter Function

- Select the cell range and then click OK. The function is placed in the cell.

# CHAPTER 12: Creating Spreadsheets with OpenOffice.org Calc

![](img/6e85ebc4ce06a64c82109523b60183ba_299_0.png)

# TIP

When you use some functions such as the AVERAGE function, you may want to decrease the number of decimal places shown in the results so that only whole numbers are represented. Use the Decimal Place button on the Object bar to reduce the number of decimal places.

# TIP

If the results of your function show ####, this means that the column width can't accommodate the results. Widen the column as needed to view the function.

# Select and Format Spreadsheet Cells

It makes sense to build your sheets by entering text, numerical values, and your formulas and functions before formatting the data on the sheet. You can then select ranges of cells and format them with different font attributes and numerical formats, and add borders or backgrounds to highlight certain cells or ranges of cells on the sheet.

You can use the various formatting options on the Object bar (Bold, Italics, Currency, Percentage, and so on). More options are available in the Format Cells dialog box. You can also format the entire spreadsheet using the AutoFormat feature.

# Select Cell Range

Select the cell range that you want to format.

# Open Format Cells Dialog

Select Format, Cells from the menu. The Format Cells dialog box opens.

# Select Format Options

Use the tabs on the Format Cells dialog box to select formatting options for the selected cell range. The Numbers tab allows you to select a number format for a cell containing numerical values. The Font tab provides access to font attributes. The Alignment tab allows you to change the alignment of the data in the selected cells. The Borders tab allows you to select a border for the selected cells or create a custom border. Use the Background tab to select a background color for the selected cells. After you have selected your options, click OK.

# Open AutoFormat

You can also select a range of cells that includes the entire spreadsheet. You can then apply an AutoFormat to the cell range.

Select the range of cells and then select Format, AutoFormat. The AutoFormat dialog box opens.
