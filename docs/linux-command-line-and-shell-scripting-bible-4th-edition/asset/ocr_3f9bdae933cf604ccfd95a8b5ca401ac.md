| -F | Use extra full output. |
| -O *format* | Display specific columns in the list *format*, along with the default columns. |
| -M | Display security information about the process. |
| -c | Show additional scheduler information about the process. |
| -f | Display a full format listing. |
| -j | Show job information. |
| -l | Display a long listing. |
| -o *format* | Display only specific columns listed in *format*. |
| -y | Don't show process flags. |
| -Z | Display the security context information. |
| -H | Display processes in a hierarchical format (showing parent processes). |
| -n *namelist* | Define the values to display in the wCHAN output column. |
| -w | Use wide output format, for unlimited width displays. |
| -L | Show process threads. |
| -V | Display the version of ps . |

That's a lot of parameters, and remember, there are still more! The key to using the ps command is not to memorize all the available parameters but only those you find most useful. Most Linux system administrators have their own sets of commonly used parameters that they remember for extracting pertinent information. For example, if you need to see everything running on the system, use the -ef parameter combination (the ps command lets you combine parameters like this):

```
$ ps -ef
  UID          PID  PPID  C STIME TTY          TIME CMD
 root          1     0  0 12:14 ?        00:00:02
 /sbin/init splash
 root          2     0  0 12:14 ?        00:00:00
 [kthreadd]
 root          3     2  0 12:14 ?        00:00:00 [rcu_gp]
```