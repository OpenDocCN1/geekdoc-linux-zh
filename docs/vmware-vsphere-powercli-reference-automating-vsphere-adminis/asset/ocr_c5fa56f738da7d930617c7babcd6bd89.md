# GATHER STATISTICAL DATA

```
AvgKbps = [Math]::Round($_.Group | \
Measure-Object -Property Value -Average).Average, 1
TotalKbps = [Math]::Round($_.Group | \
Measure-Object -Property Value -Sum).Sum, 1
```

The script in Listing 16.14 produces a simple table (similar to the following) that lists the average and total transmit rate per pNIC for the previous day on each server. This table allows you to see how your load balancing is performing across servers.

| TotalKbps ESXname pNIC AvgKbps |
|---|---|---||
| 282 | esx8.test.local vmnic0 | | 5,9 |
| 35338 | esx8.test.local vmnic1 | | 736,2 |
| 5 | esx8.test.local vmnic6 | | 0,1 |
| 0 | esx8.test.local vmnic7 | | 0 |
| 210 | esx9.test.local vmnic0 | | 4,4 |
| 13368 | esx9.test.local vmnic1 | | 278,5 |
| 0 | esx9.test.local vmnic6 | | 0 |
| 1 | esx9.test.local vmnic7 | | 0 |
| 175 | esx10.test.local vmnic0 | | 3,6 |
| 26463 | esx10.test.local vmnic1 | | 551,3 |
| 0 | esx10.test.local vmnic6 | | 0 |
| 0 | esx10.test.local vmnic7 | | 0 |
| 186 | esx11.test.local vmnic0 | | 3,9 |
| 12857 | esx11.test.local vmnic1 | | 267,9 |
| 0 | esx11.test.local vmnic6 | | 0 |
| 4460 | esx11.test.local vmnic7 | | 92,9 |
| 287 | esx12.test.local vmnic0 | | 6 |
| 17960 | esx12.test.local vmnic1 | | 374,2 |
| 0 | esx12.test.local vmnic6 | | 0 |
| 1 | esx12.test.local vmnic7 | | 0 |

If you investigate the Values closely, you will notice that the first element is the complete VHostImpl object, not just the name property. In this script, that didn't make a difference, but if you want to use only the ESXi host's name, just replace the line containing the Group-Object cmdlet with this:

```
-Finish $Finish | Group-Object -Property {$_.Entity.
Name), Instance | \
```