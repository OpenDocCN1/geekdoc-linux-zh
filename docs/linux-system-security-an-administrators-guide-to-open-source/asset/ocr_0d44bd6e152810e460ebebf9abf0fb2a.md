# Table 10.3 Extending Capabilities in Allow and Deny Files (Continued)

| Optional Keyword | Description |
| :--- | :--- |
| `severity facility.level` | Allows for the relocation of log messages through `syslogd`. Normally, Red Hat 5.2/6.0 implementation will log to `auth-priv.info`. By using this option, you may change both the facility and level, such as with `severity local0.warn`. If you change the facility, then you may also need to make an appropriate entry in `/etc/syslog.conf` for this change to have an effect. Use of this option does not require the facility, but it does require the level. |
| `allow deny` | These options permit maintaining both allow and deny rules in the same file. If used, one of these two mutually exclusive options must appear last in the rule. See *Condensing TCP_Wrappers Rules into One File* on page 213 for examples. |
| `spawn`<br>`shell_command` | Executes the specified `shell_command` as a child process. See *Using spawn* on page 210 for examples. |
| `twist`<br>`shell_command` | Executes the specified `shell_command` as a replacement process to the process specified as the last field in an `/etc/inetd.conf` file. See *Using twist* on page 211, for examples. |
| `rfc931 seconds` | Causes the server to execute a call to the client in order to obtain the username invoking the request. The client must be running `identd` or similar RFC931 or RFC1413 command daemon. A time-out for the call may be specified in `seconds`; the default is 10 seconds. This option does not apply to UDP services. |
| `banners dir` | Specifies the fully qualified directory, `dir`, in which `tcpd` will search for a file of the same name as the wrapped daemon, the contents of which will be displayed prior to the `login` prompt. See *Using banners* on page 206, for example. This option is available only for certain TCP services. Services such as `in.rshd` in remote execution mode will not work with banners. |
| `setenv`<br>`var value` | Allows for the establishment or modification of a shell environment variable (`var`); usually this option is followed by a `spawn` or `twist` option. |
| `umask value` | Sets the umask for any operations in a rule; `value` must be in octal. |
| `user`<br>`username.group` | Causes the privileges within the rule to be set to the specified `username` and optionally the specified `group`. |

It turns out that many of the options described in Table 10.3 may utilize information collected by `tcpd`. This is accomplished through a defined set of variables, listed in Table 10.4. The information is carried in letters and may be expanded with a preceding $, such as $a for client IP address and $d for the daemon name.