# Report Formats

Once you have collected the data for your report, you will need to present it in one form or another. With PowerShell, many formats for presenting your data are available.

# On the Screen

This is the simplest way to visualize results from a script. As you have seen in examples of this chapter, when the Select-Object cmdlet is and you do not redirect the output to another destination, the results will be displayed in the console of the PowerShell session.

# Out-GridView

If you want to quickly view your report in a nice interactive table, you can use the Out-GridView cmdlet. Remember that this feature requires Microsoft .NET Framework 3.5 with Service Pack 1 to work. Using the interactive table, you can sort your data on any column by clicking the header. To hide, or reorder columns, right-click a column. You can also apply a search filter or filter criteria by using the Query window and adding criteria using the Add button. Figure 15.2 shows a typical Out-GridView report.

FIGURE 15.2 Sample Out-GridView report

![](bbox=[0.142, 0.587, 0.881, 0.805])