
# LISTING 21.5 vRO JavaScript code for Invoke-ExternalPSSScriptReturnCode

```javascript
// Create variables
var session
var sessionOutput;
var XMLReturncode = "";
var returnCode = ""

// Use powershell Host session
try {
    session = powershellHost.openSession();
    var script = '& ' + scriptPath + ' ' + arguments;

    System.log("Script is: " + script);

    // Run the script
    sessionOutput = session.invokeScript(script);

    // Get the results
    results = sessionOutput.getResults();

    // Get the return code from the results
    if (results != null) {

        XMLReturncode = results.xml();
        returnCode = XMLReturncode.split("<I32>").pop().split("</I32>").shift();

        System.log("XMLReturnCode is: " + XMLReturncode);
        System.log("returnCode is: " + returnCode);
    }
    System.log("Script output is: " + sessionOutput.getHostOutput());
} catch (ex) {
    System.warn(ex);
} finally {
    if (session) {
        powershellHost.closeSession(session.getSessionId());
    }
}
```

# CHAPTER 21 VREALIZE ORCHESTRATOR

> TIP It is worth creating a Dev/Scratch folder within vRO workflow folders where you can create initial drafts of workflows that may require some testing. Later on, they can be moved to a more appropriate folder.

The Invoke-ExternalPSScriptReturn workflow is now available for test with the Test-ReturnCode.ps1 PowerShell script. Run the workflow and supply the following inputs (PowerShell 21:13):

- For PowerShellHost: The PowerShell Host created by the vRO PowerShell plug-in
- For scriptPath: C:\Scripts\Test-ReturnCode.ps1
- - a 3

# FIGURE 21.13 Invoke-ExternalPSScriptReturnCode parameters

![](img/62596f5acc979040608a4e5111beb7d6_757_0.png)

In the workflow log you should see something similar to the following output containing the script return code and the output of the script:

[2015-01-12 17:23:19.59.514] [I] Script is: & "C:\Scripts\Test-ReturnCode.ps1"
-a 3
[2015-01-12 17:23:20.420] [I] XMLReturnCode is:
<Objs Version="1.1.0.1" xmlns="http://schemas.microsoft.com/powershell/2004/0"><I32>0</I32></Objs>

[2015-01-12 17:23:20.420] [I] returnCode is: 0
[2015-01-12 17:23:20.420] [I] Script output is: Random number is 10

Result is 30
Result is less than 40

It would be possible to take return code in a subsequent step of a parent vRO workflow and doing something with it. For example, you could create a scriptable task with a JavaScript case statement to do different things based on the return code (Listing 21.6).

# LISTING 21.6 Example of JavaScript case statement to process return code

```javascript
switch(returnCode) {
  case "0" : System.log("tResult is less than 40"); break;
  case "1" : System.log("tResult is greater than 40");break
  case "2" : throw "There was an error";
  default : throw "Undefined error occurred";
}
```

# Use Cases

In this section, we will look at a number of use cases for PowerShell within vRO and explain how to go about implementing it.

# vSphere Tagging

In vSphere 5.1, VMware introduced new tagging functionality to the vSphere Web Client to releaseCenter attributes as a method of attaching metadata to objects such as virtual machines and datastores. As of this writing, there is no public API to manage these tags and consequently it is not possible to achieve this natively via vRO. However, vSphere tagging functionality was added to PowerCLI in version 5.5

# Requirements

R1 and has been enhanced in later versions. Consequently, we can use PowerCLI via the PowerShell plug-in to bring tagging functionality to vRO.

- Ensure the vRO plug-in has been configured with a PowerShell host, the Invoke-ExternalPScriptReturn workflow created earlier in this chapter is available, and PowerCLI has been installed and is functional on the PowerShell host.
- Ensure that credentials are available to connect to vCenter with update tags for virtual machines.
- Ensure a tag category for virtual machines has been created and populated with tags. For example, to create these requirements we could use PowerCLI rather than the Web Client to create a Customer Tag category and tags within that (Listing 21.7).

# LISTING 21.7 Creating a Tag category and tags

```powershell
New-TagCategory -Name "Customer" -Cardinality Multiple \
-EntityType VirtualMachine \
-"Customer01", "Customer02", "Customer03" \
ForEach-Object {New-Tag -Name $_ -Category "Customer" }
```

# PowerCLI Tagging Script

You need a PowerCLI script to carry out the tagging. For the purposes of this example, the script will only handle tagging virtual machines. Listing 21.8 contains the code that will be used in the C:\Scripts\Set-VMTagging.ps1 file on the PowerShell host that we will use to achieve this and to send back return codes based on the outcome.

# LISTING 21.8 Tagging virtual machines via PowerCLI

```powershell
#
.SYNOPSIS
Set VM Tagging for vRO with Return Codes
.DESCRIPTION
Set VM Tagging for vRO with Return Codes
.PARAMETER Name
Name of the VM to tag
.PARAMETER Tag
Name of the tag to assign

.PARAMETER vCenter
Name of the vCenter to connect to

.PARAMETER Username
Username to connect to vCenter with

.PARAMETER Password
Password to connect to vCenter with

.INPUTS
String

.OUTPUTS
None

.EXAMPLE
/Set-VMTagging.ps1 -Name VM01 -Tag Customer01 -vCenter
vcenter05.sundayle.local -Username sundayle\vcosvc
-Password Pssword1
#>
[CmdletBinding()]
Param
(
[parameter(Mandatory=$true)]
[ValidateNotNullOrEmpty()]
[String]$Name,

[parameter(Mandatory=$true)]
[ValidateNotNullOrEmpty()]
[String]$Tag,

[parameter(Mandatory=$true)]
[ValidateNotNullOrEmpty()]
[String]$vCenter,

[parameter(Mandatory=$true)]
[ValidateNotNullOrEmpty()]
[String]$Username,

[parameter(Mandatory=$true)]
[ValidateNotNullOrEmpty()]
[String]$Password
)

# --- Import the PowerCLI Module
try {
```powershell
if ( -not ( Get-Module VMware.VimAutomation.Core ) ) {
    Import-Module "C:\Program Files (x86)\VMware\Infrastructure\vSphere PowerCLI\Modules\VMware.VimAutomation.Core"
}
```
# --- Connect to vCenter
try {
```powershell
Connect-VIServer -Server $vCenter -User $Username -Password $Password -WarningAction SilentlyContinue -ErrorAction Stop
Write-Host "Successfully imported the PowerCLI Module"
}
catch [Exception] {
    Write-Host "Unable to import the PowerCLI Module"
    return 2
}
```
# --- Test the VM exists
try {
```powershell
  $VM = Get-VM $VMName -ErrorAction Stop
  Write-Host "VM $VMName exists"
} catch [Exception] {
  Write-Host "VM $VMName does not exist"
  return 4
}
```

# --- Test the Tag exists
try {
```powershell
  $TagObject = Get-Tag -Name $Tag -ErrorAction Stop
  Write-Host "Tag $Tag exists"
} catch [Exception] {
  Write-Host "Tag $Tag does not exist"
  return 5
}
```

# --- Set the Tag Assignment
try {
```powershell
  $TagAssignment = $VM | New-TagAssignment -Tag $Tag -ErrorAction Stop
  Write-Host "Successfully set Tag Assignment for $VM"
  return 0
} catch [Exception] {
  Write-Host "Unable to set the Tag Assignment for $VM"
  return 1
}
```

# vRO Tagging Workflow

To create a new vRO workflow, you use the Set-VMTagging workflow. Set the inputs as follows (Figure 21.14):

- VM Type: string
- tag Type: string
- vCenter Type: string
- username Type: string
- password Type: SecureString

FIGURE 21.14 Set-VMTagging (Inputs tab)

![](img/62596f5acc979040608a4e5111beb7d6_763_0.png)

Within the workflow presentation, set all of the inputs to Mandatory. Figure 21.15 shows an example of how to set one using the VM input. Select the input and on the Properties tab add the Mandatory Input property.

Within the workflow schema, add a scriptable task and name it Set arguments on the Info tab. In the In tab of task, add all of the parameters of the workflow (Figure 21.16).
