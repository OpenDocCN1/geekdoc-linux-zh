different scenarios where each scenario has a certain combination of interest rate and loan duration in months. To use scenario for this comparison, follow these steps:

+   1. Set up the spreadsheet cells with labels and values for the principal, annual interest rate in percentage, and loan duration in months. Calculate the monthly payment using this formula:
+   2. Select the cells that you want to include in the scenario and choose Tools→Scenarios.
+   3. Fill in the scenario name, and then click OK.
+   4. Enter values into the cells — principal, interest rate, and months to repay loan.

```
-PMT(MONTHLY_RATE,MONTHS,PRINCIPAL)
```

The Create Scenario dialog box appears.

The scenario name appears in a drop-down menu above the cells that constitute the scenario (as shown in Figure 2-4). The cell values define what that scenario means.

Figure 2-4:
Use scenarios to compare the effect of different sets of values on a calculation.

![](bbox=[0.25, 0.58, 0.7, 0.85])

+   5. Repeat Steps 2, 3, and 4 for other scenarios where each scenario has a combination of principal amount, rate, and loan duration in months.
+   6. Select a scenario from the drop-down list (refer to Figure 2-4) to see the monthly payment for that scenario.