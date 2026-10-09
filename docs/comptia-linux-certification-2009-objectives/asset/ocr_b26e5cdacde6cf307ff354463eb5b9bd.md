| Condition | Description |
|---|---|
| -atime | Matches by access time in days. |
| -mtime | Matches by modification time in days. |
| -ctime | Matches by time of latest changes in a file. Arguments are counted in days. |

# Logical Operators for Conditions

You can combine conditions using logical operators. When more than one criterion is specified, by default, only those files that satisfy all conditions are returned. However, the logical operator OR can be applied to these conditions by using -o between conditions. Also, the NOT operator could be applied to conditions by using -not to negate a condition.

# Numeric Arguments

Numeric arguments are used to specify a numeric value. The following table lists the numeric arguments for size and their description.

| Use This Argument | If You Need To |
|---|---|
| n | List files that are equal to n units (default option). |
| +n | List files that are greater than n units. |
| -n | List files that are less than n units. |

The following table lists the numeric arguments for time and their description.

| Use This Argument | If You Need To |
|---|---|
| n | List files that were accessed n days ago (default option). |
| +n | List files that were accessed more than n days ago. |
| -n | List files that were accessed less than n days ago. |