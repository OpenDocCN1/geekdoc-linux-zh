# # Answers to Review Questions

+   1. D. The main system logging process is syslogd; the klogd process kernel messages, generally by passing them to syslogd.

+   2. C. The /etc/syslog.conf file is the configuration file for the syslogd process.

+   3. B. The dmescmd displays the contents of the kernel ring buffer.

+   4. A, B, C, D. During rotation, the oldest log file is deleted.

+   5. C, D. The swatch and logwatch tools are distributed as part of the Red Hat PowerTools collection. Neither logman nor logrotate analyze log files.

+   6. C. The logrotate program rotates log files weekly, keeping four generations of log files in addition to the current log file.