# Moving Alarms

Moving alarms within the same vCenter Server is quite easy, and numerous scripts are available in the blogosphere; Google or Bing around a bit. You'll find one example of such a script here:

```
www.lucd.info/2020/02/20/alarms-moving-them-around/
```

When you want to move alarm definitions between vCenter Servers that don’t “see” each other, you can’t use a script that reads the alarm definitions from one vCenter Server and re-create these alarms on another vCenter Server. The script in this case will need to store the alarm somewhere where they can be picked up when the script is running on the target vCenter Server. Unfortunately, serializing and deserializing PowerShell objects is not too straightforward. This is why we use the following alternative. The Get-AlarmScript function takes an object, produced by the Get-Alarm function, and will generate PowerShell code that contains all the necessary statements to create the alarm. This PowerShell code can be saved in a PSI file and can be transferred to your destination vCenter Server. When you execute the code on the destination vCenter Server, the alarm will be created. The Get-AlarmScript and Get-Alarm functions are included as part of the vCenterAlarms module produced by the authors and referenced earlier in the chapter.

Listing 17.15 shows a sample run using both functions.

# LISTING 17.15 Generating PowerShell code to move alarms between vCenters

```
Get-Alarm -Name "Book: test alarm" | Get-AlarmScript |\nSet-Content "C:\myAlarm.ps1"
```

The file myAlarm.ps1 will contain a PSI script that you can execute on another vCenter Server, and provided the entity on which the original alarm was defined is there, the script will create a new alarm identical to the one you started from. The generated script looks something like Listing 17.16.

# LISTING 17.16 myAlarm.ps1

```
#Requires -Version 4.0\n#Requires -Modules @{ModuleNameName="VMware.VimAutomation.Core"};`\nModuleVersion="6.0.0.0"\n\n$spec = New-Object VMware.Vim.AlarmSpec
```

![](bbox=[0.903, 0.427, 0.933, 0.555])