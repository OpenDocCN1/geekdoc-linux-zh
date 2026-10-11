| Table 10.5 Signals That Can Be Sent to syslogd |  |  | |---|---|---| | *Signal* | *Action* |  | | SIGHUP | Reinitializes syslogd by stopping the daemon, reading the /etc/syslog.conf file, and starting syslogd |  | | SIGTERM, SIGQUIT, SIGINT | Stops syslogd |  | | SIGUSR1 | Toggles debugging if started with the -d switch |  | | SIGALRM | Logs the mark line |  |

After you kill syslogd, you can restart it using the options listed in Table 10.4. The best way is for you to specify a configuration file containing the instructions to be sent to syslogd.

# Key Concept

You can manage the syslogd daemon through the use of signals. This enables you to make changes to the configuration file and then have them take effect.

# Configuring syslogd

The /etc/syslog.conf file controls where information is written. Any line that begins with a # contains comments and is ignored by syslogd. Also, any blank lines are ignored. A typical /etc/syslog.conf file might look like the following:

```
# Log all kernel messages to the console.
kern.* /dev/console

# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none /var/log/messages

# The authpriv file has restricted access.
authpriv.* /var/log/secure

# Log all the mail messages in one place.
mail.* /var/log/maillog
```