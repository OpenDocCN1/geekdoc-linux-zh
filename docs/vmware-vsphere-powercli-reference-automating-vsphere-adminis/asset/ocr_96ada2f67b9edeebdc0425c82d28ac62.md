throw "Unable to retrieve Alarm Event IDs";

A sample run of the function results in a listing of the EventType and EventTypeId values you'll need in order to define your trigger. Here's a sample output that all types show regular, EventEx, and ExtendedEvent:

```
Get-AlarmEventId | Select-Object -First 3
```

EventType : AccountRemovedEvent
EventType : vim.event.AccountRemovedEvent
Group : regular
Description : Account removed
Attributes : account(string),group(bool)

EventType : EventEx|ExtendedEvent
EventType : com.vmware.license.AddLicenseEvent
Group : EventEx
Description : Added License
Attributes : eventTypeId(string),message(string),objectId(st...objectName(string),severity(string),licenseKey(string)

EventType : ExtendedEvent|EventEx
EventType : com.vmware.vc.HA.ClusterFailoverActionCompleted...
Group : ExtendedEvent
Description : vSphere HA completed a failover action
Attributes : message(string),eventTypeId(string),managedObje...

Now you have seen illustrations of the three event types—regular(the standard set of events that come with vSphere), EventEx, and ExtendedEvent—and you know what information needs to be supplied to define the event, let's create an example.

First, let's create an Event type alarm expression that will fire when the network redundancy for the dvPorts is restored. Both properties in the EventAlarmExpression object would be populated like this:

```
$expression = New-Object VMware.Vim.EventAlarmExpression
$expression.eventType = "EventEx"
$expression.eventTypeId = "esx.clear.net.dvport.redundancy.restored"
```