
# CHAPTER 17 ALARMS

```powershell
[CmdletBinding()]
[OutputType('System.Management.Automation.PSCustomObject')]

Param (
    [parameter(Mandatory = $true, ValueFromPipeline = $true)]
    [ValidateNotNullOrEmpty()]
    [PSObject]$Entity
)

begin {
}
process {
    try {
        foreach ($EntityObject in $Entity){
            foreach ($ActiveAlarm in $EntityObject.ExtensionData.TriggeredAlarmState){
                # -- Get Object Views

                $AlarmView = Get-View $ActiveAlarm.Alarm -Property Info.Name
                $EntityView = Get-View $ActiveAlarm.Entity -Property Name

                # -- Create Output Object

                $Object = [pscustomobject]@(
                    Name = $AlarmView.Info.Name
                    Entity = $EntityView
                    EntityType = $EntityView.GetType().Name
                    Status = $ActiveAlarm.OverallStatus
                    Time = $ActiveAlarm.Time
                    Acknowledged = $ActiveAlarm.Acknowledged
                    AcknowledgedByUser = $ActiveAlarm.AcknowledgedByUser
                    AcknowledgedTime = $ActiveAlarm.AcknowledgedTime
                )
                Write-Output $Object
            }
        }
    }
    catch [Exception] {
        throw "Unable to get active alarm"
    }
}
end {
}
```

Typical output would be as follows:

```powershell
Get-Folder "Datacenters" | Get-ActiveAlarm
```

| Property | Value |
| :--- | :--- |
| Name | Host memory usage |
| Entity | vesxi20.sunnydale.local |
| EntityType | HostSystem |
| Status | yellow |
| Time | 11/06/2015 21:57 |
| Acknowledged | True |
| AcknowledgedByUser | sunnydale |
| AcknowledgedTime | 15/06/2015 22:19 |

# Integration

- CHAPTER 19: vDIRECTOR
- CHAPTER 20: vCenterAIR
- CHAPTER 21: vRealIZE ORCHESTRATOR
- CHAPTER 22: SITE RECOVERY MANAGER
- CHAPTER 23: POWERCLI

# CHAPTER 18: The SDK

IN THIS CHAPTER, YOU WILL LEARN TO:

- WORK WITH THE vSphere SDK ........................... 622
- USE THE vSphere API REFERENCE ........................ 624
- Setting a Host in Maintenance Mode. ............................ 626
- Did the Alarm Fire for SNMP? ............................ 627
- Finding Metrics for Thin Provisioning. ........................ 628
- Can You Migrate This Guest? ....................... 629
- USE MANAGED OBJECTS ..................................... 633
- Managed Object Types ................................... 634
- Data Objects and Their Methods. ............................... 639
- Using vSphere Managers ......................................... 642
- Managed Object References. ....................... 644
- PARAMETER OBJECTS ............................... 649
- FIND THE METHOD YOU NEED ................................ 650
- Changing the Boot of a Virtual Machine ............ 651
- Finding the Patches on ESXi Host ................... 652
- Finding the Host Uptime. ........................ 653
- Changing the vCenter Logging ............................ 653
- UNDERSTAND RETURN VALUES AND FAULTS ............... 656
- PUT SOME TIPS AND TRICKS TO USE ................... 658
- Waiting for Asynchronous Task ................................ 658
- Better Handling after Asynchronous Tasks ................... 659
- Finding Service Managers with Get-View ........... 659
- Advanced Filters with Get-View ....................... 660

Though PowerCLI has grown over various releases, there will still come a time when you won't find a cmdlet to do the task you have in mind. That is when you start looking at vSphere APIs. These APIs give you full access to all vSphere management components. Working with vSphere APIs might appear to be obscure, but rest assured, once you find your way around, you will find them easy to use.

Now, would you write a book on PowerCLI with vSphere API? The answer is simple. With the help of the vSphere API, your scripts can get part of the functionality that PowerCLI cmdlets cover, but not everything. There are, for example, properties that you cannot retrieve through PowerCLI cmdlets. That is where the vSphere API comes in. It provides access to vSphere through specialized cmdlets Get-View and Get-Object.

# Work with the vSphere SDK

The full name of this is vSphere Services SDK, but most of the time we will refer to it as the vSphere SDK or just the SDK. While the SDK is a collection of documents, Service Definition Language (WSDL) files, and Java libraries, most of the time we refer to one specific document, the vSphere API Reference. This reference provides all the information concerning the data structures available through the vSphere API. This section provides a short summary of how the vSphere Services are implemented and how you can use them from PowerCLI scripts.

# WANT TO KNOW MORE?

This chapter only scratches the surface of what is available and what you can do with the vSphere Services. The summary should be enough to give you a rough idea of how the web services work. If you want to delve deeper, consult Steve Jordan's excellent book VMware vSphere SDK (Prentice Hall, 2009).

The vSphere API is exposed as a web service that runs on vSphere servers. The servers can be the vCenter Server or a VMware vSphere Hypervisor server (formerly known as an ESXi server). In other words, you use the same API for the vCenter Server as for the ESXi server. So far so good—as you might have guessed, this rule doesn't hold true in some cases. For example, to download a screenshot of a guest's console you need to connect directly to the vSphere Hypervisor server. And to retrieve tasks and events information, you will have to connect to the vCenter Server.

Because the API is exposed as a web service, it is language independent from a client perspective. The requests and responses that your application sends and receives from the vSphere servers use the XML format. The protocol that is used to send and receive these requests and responses is the Simple Object Access Protocol (SOAP). The underlying network protocol used is HTTPS. The object model that is used contains the three major types of objects listed in Table 18.1.

# TABLE 18.1 vSphere API object model

| Object type | Description |
| :--- | :--- |
| Managed objects | These are server-side objects and represent a vSphere entity (host, guest, datastore, etc.) or a vSphere service (LicenseManager, PerformanceManager, etc.). |
| Data objects | These contain information about the managed objects. They can contain: Managed object properties (number of vCPUs in a guest, mount information about an NFS datastore.), Method parameters (for example, the HostVirtualNicSpec, which is a parameter object to the AddVirtualNic method). Return values (for example, the GetAlarm method returns an array of Alarm object references). |
| Fault objects | These are objects that are returned when a method could not be executed correctly. They contain information about the error that has occurred. |

An important concept you should understand is that you do not access these vSphere objects directly. The client, the PowerCLI session in our context, has a copy of these vSphere objects. These copies are called .NET VObjects, .NET objects for short. These .NET objects are asynchronous copies of the vSphere objects. This means that when a property in one of the vSphere objects changes, that change will not appear automatically in the .NET object. It is up to the client to refresh its copy, the .NET object!

# Use the vSphere API Reference

The vSphere API Reference can be quite intimidating at first view. But rest assured, it all clicks nicely once you get the hang of it.

> TIP The complete vSphere API Reference is available online, but you can also download and install a local copy. That is handy when you are writing a script and you do not have Internet access.

You access the vSphere API Reference with a web browser (Figure 18.1).

# FIGURE 18.1 The vSphere API layout

![](img/62596f5acc979040608a4e5111beb7d6_655_0.png)

The layout of the vSphere API Reference has four distinct areas, as described in Table 18.2.

The Table of Contents (ToC) is logical if you understand the different object types that live in vSphere SDK. (We described them in the section "Work with the vSphere SDK.") ToC lists all of the managed objects. As of this
