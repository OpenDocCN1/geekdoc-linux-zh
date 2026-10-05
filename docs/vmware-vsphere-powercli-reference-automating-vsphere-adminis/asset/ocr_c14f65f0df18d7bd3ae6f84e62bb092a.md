# EXECUTING A SCRIPT

| Name | NumCpu | MemoryGB |
|---|---|--|
| VM1 | 4 | 16 |
| VM4 | 2 | 6 |
| VM5 | 4 | 6 |
| VM7 | 1 | 1 |
| VM8 | 1 | 1 |

# # Scheduling a Script

Sometimes you need for an action to happen at a specific time, or after a certain event that you may, or may not, be present. Maybe you want to run a report every morning before you arrive, or you may want to schedule a check each time the server reboots. Regardless, these tasks are accomplished using the Windows Task Scheduler to execute PowerShell scripts at a configured interval.

To schedule a PowerShell script to be run by Windows, you can create the task like any other task. From the Computer Management console expand the Task Scheduler and browse to the Task Scheduler Library. Create a new basic task, give it a name, and set it when it is executed. For example, you'll select Start A Program.

The program you want to execute is the PowerShell executable: powershell.exe. To specify which script you want to execute, in the Add Arguments field enter -file C:\path\script.ps1, where the latter part the actual path to your script (see Figure 25.2).

**FIGURE 25.2** Creating a scheduled task

![](bbox=[0.287, 0.607, 0.843, 0.927])

PowerCLI and DevOps

PART VI