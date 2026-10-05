# 11 Syslog and Log Files

System daemons, the kernel, and various utilities and services all emit data that is logged and eventually ends up on your finite-sized disks. Most of data that has a limited useful life and needs to be summarized, compressed, archived, and eventually-thrown away. Access and audit data may may need to be managed closely according to regulatory retention rules or site security policies.

Experienced administrators review logs sooner rather than later. Log files often contain important hints that point toward the resolution of vexing configuration problems. When a daemon refuses to start or a chronic error continues to plague a booting system, check the logs first.

UNIX has historically tried to use an integrated system known as syslog for one-stop log shopping, but this effort has met with mixed success at best. Although the syslog daemon still reigns as the designated king of logging, plenty of applications, network daemons, startup scripts, and other vigilantes still write to their ad hoc log files. This lawlessness has resulted in a complement of logs that varies significantly among flavors of UNIX and even among Linux distributions.

In most cases, a log event is captured as a single line of text that includes the time and date, the type and severity of the event, and any other relevant details. The