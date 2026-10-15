+   - Destinations
+   - Log Paths

# Facilities

The facility refers to the subsystem that provides the corresponding message. Each program that uses syslog for logging is assigned such a facility, usually by its developer.

The following describes these facilities:

Table 7-1

| Facility | Description |
|---|---|
| authpriv | Used by all services that have anything to do with system security or authorization. All PAM messages use this facility. The ssh daemon uses the auth facility. |
| cron | Accepts messages from the cron and at daemons. |
| daemon | Used by various daemons that do not have their own facility, such as the ppp daemon. |
| kern | All kernel messages. |
| lpr | Messages from the printer system. |
| mail | Messages from the mail system. This is important because many messages can arrive very quickly. |
| news | Messages from the news system. As with the mail system, many messages might need to be logged in a short time. |
| syslog | Internal messages of the syslog daemon. |