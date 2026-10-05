
# USE THE VSPHERE API REFERENCE

writing, there are more than 120 managed objects. Some of the entries in the ToC could in fact have been listed together. The enumerated types are just a special type of data object. An enumerated type is a data object with a specific set of predefined values. A good example is the DayOfWeek, which you might have guessed, can only contain the names of the weekdays (Monday, Tuesday, and so on). There are more than 1,800 data objects and 290 enumeration types. You will also find a Fault Type entry in the ToC. Fault types are used to pass error information from the server to your application. There are more than 680 fault types.

## 18.2 vSphere API Reference

| Area | Description |
| :--- | :--- |
| Table of Contents | Located on the left-hand pane, the Table of Contents shows the topics that are available in the reference. |
| Index | The Index provides an alphabetical list of all the elements selected in the Table of Contents. |
| Search | The Search field allows you to specify the full or partial name of the element you are looking for. The results of the search are displayed in a pop-up list below the Search field. When there is more than one hit, you will be able to select a specific element with the help of the cursor keys and the Enter. |
| Content | The Content for a specific element is shown in the right-side frame of the browser. |

Following entries in the ToC are there to make your life as an API user easier. Instead of wading through vSphere objects, these entries (listed in Table 18.3) provide indexes to commonly used concepts in vSphere objects.

## 18.3 vSphere object concepts

| Object concept | Description |
| :--- | :--- |
| All Types | Lists all known object types (managed objects, data objects, enumeration types, and fault objects). There are more than 2,990 entries here. |
| All Methods | Lists all methods available in the API. There are currently more than 720 available methods for you to call. |
| All Properties | Lists all the properties and the object(s) where you can find the property. This is the longest list of them all, with more than 6,150 entries. |
| All Enumerations | Lists all the possible values you can find in the enumerated types. There are more than 1,390 entries in this list. |

There are several ways to use the SDK Reference, and which you choose depends on what you are trying to find. To be proficient, you'll need to acquire a lot of hands-on experience. The next sections provide some cases to get you started.

## Setting a Host in Maintenance Mode

A common task is to set a host into Maintenance mode. Let's look to see if there is a method that does this. Enter maintenance in the Quick Index field for the All Methods entry. Bingo, you have a winner (Figure 18.2);

FIGURE 18.2 EnterMaintenanceMode_Task

![](img/62596f5acc979040608a4e5111beb7d6_657_0.png)

Just like PowerShell scripts, there is no single correction for a problem. You can arrive at the same result via the All Properties entry. Enter maintenance in the Quick Index field (Figure 18.3).

FIGURE 18.3 inMaintenanceMode_property

![](img/62596f5acc979040608a4e5111beb7d6_657_1.png)

There is a property called inMaintenanceMode that looks promising. Let's investigate the data object that contains the property (Figure 18.4).

In the description of the property, you can see a link to EnterMaintenanceMode_Task.

## FIGURE 18.4 Host Object Description

| Property | Description |
| :--- | :--- |
| hostTime | dateTime | The time when the host was booted. |
| connectionState | connectionState | The host connection state. See the description in the connectionState enumeration for details. |
| maintainedState | ClusterDefinedMaintenanceState | The availability state of a host in a cluster (maintenance or standby mode, if it has one). See ClusterDefinedMaintenanceState. The property is set to if the host is disabled, or if the host is in maintenance mode. |
| healthSystemStatus | healthEnum | Available system health status |
| hostMaxVirtualDiskCapacity | long | The maximum spherical virtual disk capacity supported. |

## Did the Alarm Fire the SNMP Trap?

As you learned in Chapter 17, "Alarms," you can set alarms in the vCenter Server that will fire when a specific event occurs in your vSphere environment. The alarm will execute one or more actions. One type of action that is used for monitoring is to fire an SNMP trap. This SNMP trap will be transmitted to a monitoring server where you can take appropriate action for the event occurred.

But if you're pretty sure the event occurred and you never see the SNMP trap arriving at your monitoring server?

Now this is, perhaps, a question you would not expect to find an answer in a section on the vSphere API Reference. We include it here to show you that even when you do not intend to use the API. All the events that can be created in a vSphere environment are documented under

## CHAPTER 18 • THE SDK

The Data Object Types entry. Let's take a look. Type **snmp** in the Quick Index field (Figure 18.5).

FIGURE 18.5 SNMP events

![](img/62596f5acc979040608a4e5111beb7d6_659_0.png)

Two of the entries that appear are obviously related to SNMP traps that are fired by an alarm. Since we want to find out what went wrong, we will have to look for the AlarmSnmpFailedEvent. With the techniques learned in Chapter 15, "Reporting and Auditing," it is quite easy to use AlarmSnmpFailedEvent as a filter after Get-VIEvent cmdlet. Doing lets you investigate whether the problem is due to a failure of the vCenter Server to send out the SNMP trap.

## Metrics for Thin Provisioning

When you want to collect statistical data on your thin provisioning, you should know of many available metrics to use. The vSphere select the PerformanceManagers object in the Managed Objects entry, and under the Performance Counters heading you will find the available performance counters (Figure 18.6).

FIGURE 18.6 Performance counters

![](img/62596f5acc979040608a4e5111beb7d6_659_1.png)

Under the Storage category, select the Datastore entry. You can now see the available metrics (Figure 18.7).

## USE THE VSPHERE API REFERENCE

## 629

## FIGURE 18.7 Storage capacity

![](img/62596f5acc979040608a4e5111beb7d6_660_0.png)

A virtual machine contains numerous metrics, including usage, snapshots, compression, etc. Available from system.

Values are updated every 30 minutes.

| Metric | Unit | FOR DEVICE | FOR DATASETS | INSTANCE |
| :--- | :--- | :--- | :--- | :--- |
| capacity | bytes | 1 | 1 | 0.0 |
| usage | bytes | 1 | 1 | 0.0 |
| free | bytes | 1 | 1 | 0.0 |
| instance | bytes | 0 | 1 | 0.0 |
| space | bytes | 0 | 1 | 0.0 |
| free | bytes | 0 | 1 | 0.0 |

Configured size of the disks. Available from dataset unit.

Amount of disk space used by a dataset or virtual machine. Since the dataset or virtual machine can expand, this may not be exceeded. Available from dataset and virtual machine metric.

To configure aggregate pool settings for the entire dataset, set the property of the HostSystem to the dataset.

To get a metric for a specific virtual machine on the dataset, set the property of the virtual machine.

To get aggregate settings specified for the virtual machine target, set the property of the virtual machine.

Amount of space associated exclusively with a virtual machine. Available from dataset and virtual machine target.

You can compile your report of provisioning based on the provided and used metrics. See Chapter 16, "Using Statistical Data," for further details on working with metrics and statistical data.

## Can You Migrate this Guest?

In vSphere client, you get a message when a operation is not possible. The Move-Vm cmdlet does not have this functionality, how does the vSphere client do this? Type migrate in the Quick Index for all Methods text, as shown in Figure 18.8.

## FIGURE 18.8 Can vMotion migrate this?

## All Methods

+   * vSphere API Reference
* All Types
* Data Objects
* All Enumerations
* All Methods
* All Types
* All methods

+   * All Methods Overview

+   * A

Check Migrate_Task. That looks promising; let's look at the method Figure (18.9).

![](img/62596f5acc979040608a4e5111beb7d6_660_1.png)
