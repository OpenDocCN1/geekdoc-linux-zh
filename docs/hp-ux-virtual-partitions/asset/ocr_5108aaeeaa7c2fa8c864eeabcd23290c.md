| | |
| --- | --- |
| <i>Monitor</i> | Provides alarm monitoring capability by accepting alarms from VantagePoint Performance and displays alarms. |
| <i>Planner</i> | Provides forecasting capability by extrapolating VantagePoint Performance data for forecasts. |
| <i>Analyzer</i> | Analyzes VantagePoint Performance data from multiple systems and displays data. You can view the data from multiple systems simultaneously. |

In our example, we will be working with a single system. We'll take the VantagePoint Performance data, collected over roughly a one-week period, and display some of it. In this example, we won't take data from several distributed systems and we'll use only one server in the example.

HP VantagePoint Performance Agent produces log files that contain information about the system resource consumption. The longer HP VantagePoint Performance Agent runs, the longer it records data in the log files. I am often called to review systems that are running poorly to propose system upgrades. I usually run HP VantagePoint Performance Agent for a minimum of a week so that I obtain log information over a long enough period of time to obtain useful data. For some systems, this time period is months. For other systems with a regular load, a week may be enough time.

After having run VantagePoint Performance for a week, I invoked VantagePoint Performance Analyzer/UX to see the level of system resource utilization that took place over the week. The graphs we'll review are CPU, Memory, and Disk. Figure 12-11 shows Global CPU Summary for the week: