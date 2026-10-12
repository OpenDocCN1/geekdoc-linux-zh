addresses, and other details. I also recommend an excellent iptables Tutorial by Oskar Andreasson (http://iptables-tutorial.frozentux.net).

Here are a few tips for using iptables features:

+   - Reduce rules — Try to improve performance by reducing the number of rules. Using subchains can keep a packet from seeing rules that don’t apply to it.

+   - Deal with fragments — Use the -f option to refer to the second and subsequent packets of a packet that was split into fragments. In general, it is safe to not drop second and third fragments for which you don’t have a first batch fragment because they won’t be reassembled. If you use NAT the fragments are assembled before filtering, so you shouldn’t have problems with unfiltered fragments being sent through.

+   - Opposite — To make a rule its opposite, use an exclamation mark (!).

+   - All interfaces — To match all interfaces of a type, use a plus sign (+), as in eth+.

+   - Blocking connections — Use the -syn option to block SYN packets (that is, those packets requesting connections). This option only applies to TCP packets.

+   - Limiting — Use the -limit option to restrict the rate of matches that result in log messages. This option allows matches to only produce messages a limited number of times per second (the default is three per hour with burst of five).

+   - DOS Attacks — You can use the -limit option to reduce the impact of DOS attacks, but it still won’t stop them altogether. As long as the traffic is directed at your server, your network bandwidth is being leeched away, and the machine still utilizes resources to ignore the data.

+   - Table types — The default table type is filter. The other types of tables are nat (for IP Masquerading) and mangle (for altering packets). To use a table other than filter you must add a -t table_type option, where table_type is either nat or mangle.

# ## Detecting Intrusions from Log Files

Preparing your system for a cracker attack is only part of the battle. You must also recognize a cracker attack when it is occurring. Understanding the various log files in which Fedora records important events is critical to this goal. The log files for your Fedora system can be found in the /var/log directory.

Fedora comes with a System Logs window (system-logviewer command) that you can use to view and search critical system log files from the GUI. To open the System Logs window, from the main desktop menu, select System Tools → System Logs. Figure 14-2 shows an example of the System Logs window.

To view a particular log file, click the log name in the left column. If you are looking for a particular message or problem, type a keyword into the Filter for: box, and click Filter: Only