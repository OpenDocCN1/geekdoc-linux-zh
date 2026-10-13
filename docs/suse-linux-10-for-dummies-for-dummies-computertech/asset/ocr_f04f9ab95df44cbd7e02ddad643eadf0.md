![](bbox=[0.131, 0.136, 0.205, 0.208])

To learn more about the functions available in OpenOffice.org Calc, choose Help➪OpenOffice.org Help. This opens the OpenOffice.org Help window, from which you can browse the functions by category and click a function to read more about it.

One interesting feature of Calc is the support for scenarios. A scenario is simply a collection of values for one or more cells. Scenarios are useful when you compare the effect of some cells on other calculations in the spreadsheet. For example, the monthly payment on a loan would depend on the principal, the interest rate, and the duration of the loan. You can use Calc’s scenario feature to compare the monthly payments for a number of different scenarios where each scenario has a certain combination of interest rate and loan duration in months. To use scenario for this comparison, follow these steps:

+   1. **Set up the spreadsheet cells with labels and values for the principal, annual interest rate in percentage, and loan duration in months (refer to Figure 12-12). Calculate the monthly payment using this formula:**
+   
+   ```text
+   =PMT (MONTHLY_RATE; MONTHS; PRINCIPAL)
+   ```
+   
+   Figure 12-12 illustrates this example. The cells in the range B5:C7 specify the principal, annual rate, and the number of months. Cell C6, with the annual interest rate, is formatted to show a percentage. Cell C11 computes the payment using the formula that you see in the formula bar. Notice that the annual rate in cell C6 has to be divided by 12 to get the monthly rate.

+   2. **Select the cells that you want to include in the scenario and choose Tools➪Scenarios.** For example, in Figure 12-12, select the cells in the range B5:C7.
+   
+   The Create Scenario dialog box appears.

+   3. **Fill in the scenario name, and then click OK.**
+   
+   For example, the scenario shown in Figure 12-12 is named `Rate 6.5 PCT` (that’s my name for the 6.5% rate scenario).

+   4. **Enter values into the cells — principal, interest rate, and months to repay loan.**
+   
+   The scenario name appears in a drop-down list above the cells that constitute the scenario (as shown in Figure 12-12). The cell values define what that scenario means.