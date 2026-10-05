optimal path. When you are working with lots of statistical data, the execution time of your script can become a critical factor. The following list shows some ways to improve execution time.

+   - Limit the number of calls to the Get-Stat cmdlet.
- Combine entities.
- Combine metrics.
- Combine groups in one call to Group-Object.
- Use only metrics that are meaningful for your report.

# # Offload Statistical Data

As you learned in the "Understand Some Basic Concepts" section, the data for HI4 is kept for one year by default. You can change the retention time to five years, that will increase the size of your vCenter Server database with a possible performance impact.

If you want to be a statistics report on older data, there is another solution. At regular points in time, collect the oldest statistical data you want to use later and store it in an external file. PowerShell provides the Export-Clixml cmdlet to store PowerShell objects in an external file. Later, you can use the Import-Clixml cmdlet to retrieve the objects and bring them back into your PowerShell session.

The script in Listing 16.19 shows some metrics to an external file.

# ## LISTING 16.19 Exporting statistical data

```
$entityNames = 'esx[01] [01289]*' 
$metrics = 'cpu.usage.average','mem.usage.average',
$disk.usage.average','net.usage.average'
$archiveLocation = 'C:\Archive'

# Time range - 12 months ago
$monthsBack = 12
$todayMidnight = (Get-Date -Hour 0 -Minute 0 -Second 0)
$xMonthsAgoMidnight = $todayMidnight.AddMonths(-monthsBack + 1)
$endOfMonth = $xMonthsAgoMidnight.
```