On the Scripting tab of task, the JavaScript code shown in Listing 21.15.
Close the task.

# LISTING 21.15 vRO JavaScript code for New-ADUser Set arguments

```
var arguments = " -FirstName " + firstName + " -Surname " 
  + surname + " -OU " + ou + " -ADUsername " + adUsername + " " 
  + "-ADPassword " + adPassword;
```

Within the workflow schema, the previously created Invoke-LocalPSScriptReturnCode workflow (Figure 21.39).

Figure 21.39 Adding the Invoke-LocalPSScriptReturnCode workflow

![](bbox=[0.273, 0.342, 0.858, 0.555])

On the In tab of the Invoke-LocalPSScriptReturnCode workflow, create the following (Figure 21.40):

powersPath Type: String (as workflow attribute)
Set the value to C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
scriptPath Type: String (as workflow attribute)

Set the value to C:\Scripts\New-ActiveDirectoryUser.ps1

and selecting the following existing attribute (Figure 21.40):

arguments Type: String

On the Out tab of the workflow, create the following (Figure 21.41):

+   - returnCode Type: String (as workflow attribute)