# Getting Started with Calc

You can either click the shortcut icon that is located on the top GNOME panel, or select Spreadsheet from the Office menu under the Applications main menu. Whichever route you take, the result is the same and Calc starts to load.

By default, Calc loads with a blank spreadsheet just waiting for you to enter information into it. In Figure 6.7, you can see that we have already started to enter some basic information into Calc.

![](bbox=[0.12, 0.35, 0.78, 0.68])

FIGURE 6.7 Use Calc to store numerical and statistical information.

Calc's layout makes it easy to organize information into rows and columns. As you can see in the example, we have sales people listed in the left column, customers in the second column, Invoice Date in the third column, and finally Revenue in the fourth column. At the moment, there are no formulas entered to help you interpret the data. Clicking the E43 cell selects it and enables you to enter in a formula in the top formula bar. If you enter in the equal sign, Calc knows that you are entering a formula and works accordingly.

In this example, we want to know the total revenue brought in up to now, so the formula to enter is =sum(E3:E42), followed by Return. Calc automatically enters the result into cell E43 for you to see. Now you want to see what the average order value was. To do this, you have to obtain the number orders made. For this you can use the counta function to count the number of entries in a given list. This is usually used when you need to find out how many entries there are in a text list. So, in cell B43, enter =counta(B3:B42) and press Enter. Calc now counts the number of entries in the range and returns the total in