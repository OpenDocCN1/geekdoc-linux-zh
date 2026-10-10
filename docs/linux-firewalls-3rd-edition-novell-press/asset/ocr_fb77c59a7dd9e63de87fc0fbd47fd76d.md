However, it's important to look for underlying causes of such outages to ensure that an attack isn't underway or that an attack hasn't already occurred. It is in this area, event correlation, where a human is most necessary. For example, did the disk partition just run out of space because an attacker is using the space or because the log files filled up the partition?

# ## Symptoms Suggesting That the System Might Be Compromised

Often, a successful attacker will try to hide their tracks with greater success, and therefore simple service monitoring won't be of assistance. The attacker might be far more skillful at hiding his tracks than you are at tracking down anomalous system states.

Linux systems are too diverse, customizable, and complicated to define an iron-clad, fully comprehensive list of definitive symptoms proving that the system is compromised. As with any kind of detective or diagnostic work, you must look for clues where you can—as systematically as you can. RFC 2196, "Site Security Handbook," provides a list of signs to check for. The "Steps for Recovering from a UNIX or NT System Compromise," available from CERT at http://www.cert.org/tech_tips/root_compromise.html, provides another list of anomalies to check for.

The following sections incorporate both lists, including all or most of their points in one form or another. The anomalies have been roughly categorized into the following: indications related to the system logs; changes to the system configuration; changes related to the filesystem, file contents, file access permissions, and file size; changes to user accounts, passwords, and user access; problems indicated in the security audit reports; and unexpected performance degradation. The anomalous indications often cross category boundaries.

# ### System Log Indications

System log indications include unusual error and status messages in the logs, truncated log files, deleted log files, and emailed status reports:

+   * **System log files**—Unexplained entries in the system log files, shrinking log files, and missing log files all suggest that something is wrong. For example, `/var/log/messages` contains the majority of the system log information on most Linux systems. If that log file is zero-sized or is missing large portions, additional investigation is warranted.

+   * **System *daemon* status reports**—Instead of (or in addition to) writing to the log files, some daemons such as crond send status reports in email. Having unusual or missing reports suggests that something is not right.