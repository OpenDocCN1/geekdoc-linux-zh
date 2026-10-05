# CHAPTER 11 * BACKING UP AND RESTORING YOUR VIRTUAL MACHINES

depending on your requirements: New-DailySchedule, New-IntervalSchedule, New-MonthlySchedule, New-WeeklySchedule, and New-YearSchedule. Listing 11.9 demonstrates how to create a schedule for Monday–Friday, inclusive, starting at 8 p.m.

> NOTE In Listing 11.9, notice that the days of the week be in a single string separated by commas. From a PowerShell usability perspective, you would typically expect to supply the days of the week as individual strings, so don't get tripped up by this.

# LISTING 11.9 Creating a Monday–Friday schedule

```
$Schedule = New-WeeklySchedule -ExecutionDays \
'Monday, Tuesday, Wednesday, Thursday, Friday' -StartTime 20:00
```

# Backup Job Template

You now have all the elements in place required to create a backup job template. Listing 11.10 creates a backup job for all VMs in the Cluster Cluster01, stores the data in the SynologyNFS repository, and uses the schedule created in Listing 11.9. There are a multitude of other options for creating a backup job; a few are used in Listing 11.10. However, it is well worth checking the help for Add-BackupJobTemplate to see what is available.

# LISTING 11.10 Creating a backup job template

```
$ClusterEntity = Get-InventoryEntity -Type ClusterComputerResource \
-WhereObject {$_.Name -eq 'Cluster01'} \
$TargetRepository = Get-Repository -Type NFS \
-WhereObject {$_.Name -eq 'SynologyNFS'} \
$Schedule = New-WeeklySchedule -ExecutionDays \
'Monday, Tuesday, Wednesday, Thursday, Friday' -StartTime 20:00 \
Add-BackupJobTemplate -JobName Cluster01 $ClusterEntity \
-TargetRepository $TargetRepository -JobSchedule $Schedule \
-NumberOfSavePoints 5 -SpaceSavingTechnologyTypeFlag Differential \
-Flags NoFlags
```