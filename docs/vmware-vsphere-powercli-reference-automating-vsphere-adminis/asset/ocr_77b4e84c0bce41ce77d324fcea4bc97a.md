# CHAPTER 17 * ALARMS

```
$expression += New-AlarmExpressionMetric -Metric "cpu.usage.
average" \
-Object "HostSystem" -Operator "isAbove" -YellowValue 7000 \
-YellowInterval 25 -RedValue 8500 -RedValue 10
```

```
# Create the alarm in the vCenter root
New-Alarm-Entity(Get-Inventory)-Name "Datacenters"-Name \
"Book: host busy" -Description "Host too busy" -Action \
groupactions \
-Expression $expression -Enabled
```

The next alarm, in Listing 17.10, sends an email and an SNMP trap when a guest loses its connectivity. The alarm is enabled for all guests in datacenter DC1.

# LISTING 17.10 Guest network connectivity alarm

```
# The transition state
$trans = @()
$trans += New-AlarmTransition-Start "green" -Final "yellow" \
-Repeat:$true

groupactions = @()
```

```
# Send an SNMP trap
$action = New-AlarmActionSnmp
groupactions += New-AlarmTriggerAction -Action $action \
-Transition $trans
```

```
# Send an Email
$action = New-AlarmActionEmail -To "lucd@lucd.info" \
-Subject "Mail subject" -Body "Body text"\ \
groupactions += New-AlarmTriggerAction -Action $action \
-Transition $trans
```

```
# Fire the alarm on the vmNetworkFailed event
$expression = @()
$expression += New-AlarmExpressionOr
$expression += New-AlarmExpressionEvent -Event \
"VmNetworkFailedEvent"
```