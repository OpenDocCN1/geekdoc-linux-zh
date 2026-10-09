# ## Error Logs

The most frequently used log for troubleshooting is the `/tmp/hacmp.out` log. It contains detailed output of all the event scripts run on the node. This information supplements and expands upon the information in the `/usr/es/ladm/cluster.log` file.

Reported resource group acquisition failures (failures indicated by a nonzero exit code returned by a command) are tracked in `/tmp/hacmp.out`, and a summary is written near the end of the listing for each top-level event.

Checking this log is important and helps to identify problems in the cluster. Use `tail -f /tmp/hacmp.out` for real time viewing) or `vi` to check the log file to quickly locate the ERROR location. You might want to scan the pages above the error condition to see if another condition caused the error. For example, if a filesystem didn't mount, further checking may indicate that the volume group did not varyon. This was probably caused by a difference between the VGDA on the volume group and the ODM copy on the system that was attempting to varyon the volume group. So instead of troubleshooting a filesystem problem, you need to troubleshoot the volume group problem.

The `/usr/adm/cluster.log` contains a good overview of the event scripts called by the cluster manager. Keep in mind the cluster manager does not start event scripts unless an event has occurred, that is, something has failed.

In HACMP/ES, Topology Services and Group Services have additional log files useful in troubleshooting network problems. See the HACMP/ES manual for details.

# ## Event Summaries

In HACMP/ES only, event summaries appear at the end of each event's detailed output in the `hacmp.out` log. A good way to get a quick overview of what has happened in the cluster lately is to use the Display Event Summaries option, which compiles and displays all of the event summaries from the `hacmp.out` log file. In addition, resource group location and state information is reported at the bottom of the display, reflecting output from the `clfndres` command. The summary display is updated once per day with the current day's event summaries.

To view a compiled list of event summaries on a node or to save the event summaries to a specified file, navigate to the Display Event Summaries options under Cluster System Management in SMIT, or use the FastPath smity cm_dsp evs.

Note that event summaries can be seen in the `hacmp.out` file in HACMP/ES 4.4.1. The Display Event Summaries feature was added in version 4.5.

# ## Deadman Switch

With HACMP Classic, a timer ensures that keepalives (heartbeats) are processed in a timely manner. If they are not, then you can have false failovers when no error condition exists. This timer is called the deadman switch. The deadman switch is a kernel extension loaded when HACMP starts. The duration of the timer is determined by the formula *time of the slowest IP network minus one second*. If the deadman switch fires,