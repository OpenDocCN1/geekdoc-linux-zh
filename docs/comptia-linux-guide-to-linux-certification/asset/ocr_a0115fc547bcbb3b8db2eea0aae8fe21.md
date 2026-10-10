![](bbox=[0.18, 0.08, 0.41, 0.16])

Any system **documentation** should be printed and kept in a log book because this information might be lost during a system failure if kept on the Linux system itself.

Reactive maintenance is further composed of many procedures known as **troubleshooting procedures**, which can be used to efficiently solve a problem in a systematic manner.

When a problem occurs, you need to gather as much information about the problem as possible. This might include examining system log files and viewing the contents of the /proc file system, as well as running information utilities, such as ps or mount. In addition, you might research the symptoms of the problem on the Internet; Web sites and newsgroups often list log files and commands that can be used to check for certain problems.

![](bbox=[0.18, 0.39, 0.41, 0.48])

The `tail -f /path/to/logfile` command opens a specific log file for continuous viewing; this allows you to see entries as they are added, which is useful when gathering information about system problems. If your system uses Systemd, you can use the `--follow` option to the `journalctl` command to do the same. For example, to view chryond events as they are added, you can use the `journalctl _COMM=chryond --follow` command.

Following this, you need to try to isolate the problem by examining the information gathered. Determine whether the problem is persistent or intermittent and whether it affects all users or just one.

Given this information, you might then generate a list of possible causes and solutions organized by placing the most probable solution at the top of the list and the least probable solution at the bottom of the list. Using the Internet at this stage is beneficial because solutions for many Linux problems are posted on Web sites or newsgroups. In addition, posing the problem at a local Linux Users Group will likely generate many possible solutions.

Next, you need to implement and test each possible solution for results until the problem is resolved. When implementing possible solutions, it is very important that you only apply one change at a time. If you make multiple modifications, it will be unclear as to what worked and why.

After the problem has been solved, document the solution for future reference and proceed to take proactive maintenance measures to reduce the chance of the same problem recurring in the future. These troubleshooting procedures are outlined in Figure 14-2.

The troubleshooting procedures listed in Figure 14-2 serve as a guideline only. You might need to alter your approach for certain problems. Remember, troubleshooting is an art that you will begin to master only with practice. There are, however, two golden rules that should guide you during any troubleshooting process:

+   * Prioritize problems—If you need to solve multiple problems, prioritize the problems according to severity and spend the most time on the most severe problems. Becoming fixated on a small problem and ignoring larger issues results in much lower productivity. If a problem is too difficult to solve in a given time period of time, it is good practice to ask for help.