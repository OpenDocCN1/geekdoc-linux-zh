On the In tab of the Invoke-ExternalScriptReturnCode workflow, create the following (Figure 21.19):

powershellHost Type: PowerShell:PowerShellHost, as workflow attribute. Set the value to be the PowerShell created as part of the PowerShell plug-in setup.

scriptPath Type: String, as workflow attribute. Set the value to C:\Scripts\Set-VMTag.psl

and select the following existing attribute (Figure 21.19):

arguments Type: String

# Figure 21.19 Invoke-ExternalScriptReturnCode (In tab)

![](bbox=[0.268, 0.357, 0.823, 0.532])

On the Out tab of the workflow create the following (Figure 21.20):

returnCode Type: string, as workflow attribute

Close the Invoke-ExternalScriptReturnCode workflow and then Save And Close the workflow.