# Attacking and Defending Unix • Chapter 14

access may give unauthorized or untrusted users access to the system, which may ultimately result in compromise by a third party.

Provided that the user does not need access to a shell, the ability of the user to access one should be limited. If restricting user access to a shell is not possible, a user not requiring administrative access to the host, yet requiring command-line tools, should be granted a restrictive shell as possible. Exercise some caution, as many Unix utilities allow the user to escape the restricted environment by spawning a shell through the utility. Use multiple layers of access control where possible.

Users requiring elevated privileges on a host, but not full control of the system, should be limited in their abilities. Facilities such as Role-based Access Control (RBAC) as found in Sun’s Solaris Operating Environment can be used to provide this type of functionality. It is essentially a compromise, giving some security so the user can perform their tasks while maintaining some level of local security. The best policy is to implement the amount of security required to keep hosts secure while fulfilling business requirements.

# Logging

Because of the possibility of workstations being accessed by numerous users, it is necessary to monitor the system more closely than other hosts. Therefore, increase your logging to almost paranoid levels. A workstation should be configured to log and report any violation of security policy, and the user ID of the offender.

Different implementations vary in accounting systems, but it is a rule of thumb that all system auditing should be logged to a location that cannot be altered by any user other than the administrator. This precludes the use of logging commands executed in a shell by a user, and logging the commands to .bash_history. Syslog output should be more verbose than standard, and additional logging, such as the Basic Security Module (BSM) as included by Sun Microsystems in Solaris, should also be enabled. The log output should be secured to permit only appending to the log file at the file system level, if possible, or otherwise stored in a manner that prevents the alteration of logs in the event of system compromise.

The Basic Security Module implemented with Sun Solaris will be discussed in more detail later in this chapter. The important point is that logging should be significantly increased, and activity on the system should be logged at the lowest level possible.