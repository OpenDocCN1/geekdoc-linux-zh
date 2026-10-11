![](bbox=[0.22, 0.05, 0.41, 0.29])

Figure 17-17: Your new spreadsheet thus far, with income and expenses listed

# 17A-2: Doing Some Math

Okay, so now it's time to make your numbers look more like money and to do some math. Here's what you need to do:

+   1. Click the **B heading** at the very top of the B column (*not* the B button that selects bold text). Once you do this, all of the cells in that column will be highlighted in black.
+   2. Next, go to the **Currency Number Format** button (the one to the left of the percent sign on the toolbar) and click it once, after which the numbers in your B column will be in a more familiar dollars-and-cents format (**$725.00** rather than **725**. Note that this is not strictly necessary, but at least now you know how to do it.)
+   3. Now get on to the math by clicking cell **B7**, typing `=sum`, and then pressing ENTER.
+       The equal sign, in case you are wondering, is a signal to your spreadsheet that you are entering a formula, such as `=2+2`, or `=3*4` (three times four), or `=3/4` (three divided by four), and so on. Typing `=sum` after the equal sign tells the spreadsheet that you will be entering a string of numbers, or cells, that you would like to add.
+       As you most likely noticed after pressing ENTER, a pair of dark parentheses appeared next to `=sum` with a flashing cursor between them. It is between these parentheses that you will list the items you want to add together.
+   4. Now click, but do not release, your mouse button in cell B2, drag the cursor to cell B6, and then release your mouse button. Those cells will now be surrounded by a red line, indicating the same *range* of cells now listed between the parentheses in your formula.
+   5. The formula in cell B7 should now read `=SUM(B2:B6)`. If so, press ENTER, and you will know your total monthly income without so much as a single gear turning in your head.