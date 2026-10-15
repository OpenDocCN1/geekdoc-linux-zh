# TABLE 20-6
xinetd Attributes
(continued)

| Attribute | Description |
|---|---|
| wait | Specifies whether the service is single-threaded or multithreaded (yes or no). If yes, the service is single-threaded, which means that xinetd will start the server and then stop handling requests for the service until the server stops. If no, the service is multithreaded and xinetd will continue to handle new requests for it. |
| user | Specifies the user ID (UID) for the server process. The user name must exist in /etc/passwd. |
| group | Specifies the GID for the server process. The group name must exist in /etc/group. |
| instances | Specifies the number of server processes that can be simultaneously active for a service. |
| nice | Specifies the server priority. |
| server | Specifies the program to execute for this service. |
| server_args | Lists the arguments passed to the server. This does not include the server name. |
| only_from | Controls the remote hosts to which the particular service is available. Its value is a list of IP addresses. With no value, service is denied to all remote hosts. |
| no_access | Controls the remote hosts to which the particular service is unavailable. |
| access_times | Specifies the time intervals when the service is available. An interval has the form hour:min-hour:min. |
| log_type | Specifies where the output of the service log is sent, either syslog facility (SYSLOG) or a file (FILE). |
| log_on_success | Specifies the information that is logged when a server starts and stops. Information you can specify includes PID (server process ID), HOST (the remote host address), USERID (the remote user), EXIT (exit status and termination signal), and DURATION (duration of a service session). |
| log_on_failure | Specifies the information that is logged when a server cannot be started. Information you can specify includes HOST (the remote host address), USERID (user ID of the remote user), ATTEMPT (logs a failed attempt), RECORD (records information from the remote host to allow monitoring of attempts to access the server). |