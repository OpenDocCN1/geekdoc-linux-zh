# FIGURE 17.1 Alarm schematic

![](bbox=[0.376, 0.143, 0.801, 0.477])

# TABLE 17.1 Alarm managed object properties

| Property | Description |
|---|---|
| Name | The name of the alarm. Be descriptive when you name your alarms. |
| Description | A description of the alarm. |
| Enabled | A Boolean value that indicates whether an alarm is enabled. |
| Setting | Defines how long to wait before an alarm is triggered again and the alarm should use a range around the threshold value. |
| Expression | Defines the conditions that must be met before an alarm is triggered. |
| Action | Defines what must be done when an alarm is triggered. |
| ActionFrequency | Defines how often the actions connected to the alarm should be repeated. |

# Alarm Actions

The action part of an alarm is where you can define what needs to be done when an alarm is fired. vCenter offers the actions described in Table 17.2. Note that you can define multiple actions on a single alarm.