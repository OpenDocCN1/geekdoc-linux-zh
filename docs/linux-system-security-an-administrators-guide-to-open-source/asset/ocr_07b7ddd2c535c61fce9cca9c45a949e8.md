# Table 10.14 Description of xinetd Log Entries

| Log Keyword | Format and Description |
| :------- | :------- |
| START | START: service_id [pid=PID] [from=IPaddress] |
|       | This entry is recorded whenever a service has started. The service_id is the name of the service as specified by the 1d attribute (recall that if this attribute is not explicitly set, it assumes the value of the service argument; see Table 10.10 on page 232); the PID is the process identifier of the invoked daemon, or if no daemon is invoked (only record if PID is specified to log_on_success); and the IPaddress is the client’s IP address (only recorded if HOST is log_on_success). |
| EXIT | EXIT: service_id [type=sl [pid=PID] [duration=ss(sec)] | 
|      | This entry is recorded when a daemon terminates; only if EXIT is specified to log_on_success. The service_id and PID entries are as before. The type entry will record the exit status or signal that caused termination. The duration captures the duration of the session in seconds and requires the DURATION option to log_on_success. |
| FAIL | FAIL: service_id reason [from=IPaddress] |
|      | This entry is generated whenever a failed attempt occurs and at least one value is specified to the log_on_failure attribute. The service_id is as before. The reason is a simple word or phrase explaining the cause of failure. The IPaddress is the client’s and the HOST value to log_on_failure must be set for this to appear. |
| DATA | DATA: service_id data |
|      | Recorded only when the RECORD value to log_on_failure occurs. The service_id is as before. The data recorded depends upon the service, but normally includes the remote username if available and status information. |
| USERID | USERID: service_id text |
|       | This information is recorded only when the USERID value is specified to log_on_success or log_on_failure or both. The service_id is as before. The text includes the client’s response to the RFC1413 call and, in particular, the remote username. |
| NOID | NOID: service_id IPaddress reason |
|     | This entry will appear only if the IDONLY value is set to the flaga attribute and the USERID value is set to at least one of log_on_success or log_on_failure. The service_id is as before. The IPaddress given is the client’s. The reason is a failure status. |

# Example 10-50 Failed rlogin Attempts from Unauthorized Host

```
sly.no.good.org$ rlogin tocpat
			topcat: Connection reset by peer
sly.no.good.org$ rlogin -l paul tocpat
			topcat: Connection reset by peer
sly.no.good.org$ rlogin -l mary tocpat
			topcat: Connection reset by peer
sly.no.good.org$
```