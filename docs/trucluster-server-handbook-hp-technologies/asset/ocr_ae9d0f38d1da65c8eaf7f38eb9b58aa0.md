The CPU time column in the above output shows no measurable CPU time, so there is no need to alter the ics_hl subsystem attributes.

# 18.1.4 ICS Statistics

The “ics” option in the cfsstat command provides statistics on ICS activities. Despite the command’s name, it provides a wealth of ICS statistics. It can be issued with an interval option providing excellent insights into ongoing ICS activities.

Note that there are many options within cfsstat that focus on various ICS statistics as shown in Table 18-2.

| ICS Options to cfsstat(8) |
|---|---|---|
| Option | V5.1B V5.1A | V5.1 V5.0A | Description |
| ics | ✓ | ✓ | Displays all ICS statistics |
| icsstat | ✓ | ✓ | Displays ICS client/server statistics |
| icschan | ✓ | ✓ | Displays ICS channel statistics (same as icschanbytes) |
| icsvc | ✓ | ✓ | Displays ICS service statistics (same as icsvccbytes) |
| icschanbps | ✓ | x | Displays ICS channel statistics (byte per second mode) |
| icschanops | ✓ | x | Displays ICS channel statistics (ops per second mode) |
| icschanbytes | ✓ | x | Displays ICS channel statistics (byte mode) |
| icschancounts | ✓ | x | Displays ICS channel statistics (count mode) |
| icsvccbytes | ✓ | x | Displays ICS service statistics (byte mode) |
| icsvcccounts | ✓ | x | Displays ICS service statistics (count mode) |
| icschanhistot | ✓ | x | ICS channel transfer size histograms (total table) |
| icschanhistcli | ✓ | x | ICS channel transfer size histograms (client table) |
| icschanhistsvr | ✓ | x | ICS channel transfer size histograms (server table) |
| icschanhistclisend | ✓ | x | ICS channel transfer size histograms (cli send table) |
| icschanhistclirecv | ✓ | x | ICS channel transfer size histograms (cli recv table) |
| icschanhistsvrrecv | ✓ | x | ICS channel transfer size histograms (svr recv table) |
| icschanhistsvrsend | ✓ | x | ICS channel transfer size histograms (svr send table) |
| icschanhistall | ✓ | x | ICS channel transfer size histograms (all tables) |
| icslog | ✓ | ✓ | Displays last 200 message sent/received by ICS -- Available only in DEBUG kernels |

Table 18-2: ICS options to the cfsstat(8) command