# Example 2.3 resolv.conf

```
; /etc/resolv.conf
;
domain		foo.bar.org		; default domain
nameserver	123.145.100.1	; name server1
nameserver	123.145.100.2	; name server2
```

# Inetd

Instead of running some of the TCP/IP service daemons continuously, they can be started when a request is made for the service and stopped when the service has been completed. This capability is supported by the inetd daemon. Configuration information for inetd is located in the /etc/inetd.conf and /etc/services files (Examples 2.4 and 2.5). Entries in the /etc/inetd.conf file indicate each service name and any required startup information. The /etc/service file lists the service name, whether it uses TCP or UDP protocols, and the well-known port number associated with the service. Each time updates are made to either of these tables the inetd daemon must be refreshed. This can be done by sending a hangup signal to the inetd PID.

```
# kill -HUP <inetd-PID>
```

# Example 2.4 /etc/inetd.conf

```
# inted.conf
#
# service socket protocol wait/ user server server program
# name type nowait program arguments
#
echo stream tcp nowait root internal
echo dgram udp wait root internal
discard stream tcp nowait root internal
discard dgram udp wait root internal
daytime stream tcp nowait root internal
daytime dgram udp wait root internal
chargen stream tcp nowait root internal
chargen dgram udp wait root internal
ftp stream tcp nowait root /etc/ftpd ftpd
telnet stream tcp nowait root /etc/telnetd telnetd
time stream tcp nowait root internal
time dgram udp wait root internal
bootps dgram udp wait root /etc/bootpd bootpd
tftp dgram udp wait nobody /etc/tftpd tftpd -n
finger stream tcp nowait nobody /etc/fingerd fingerd
exec stream tcp nowait root /etc/rexeced rexecd
login stream tcp nowait root /etc/rlogind rlogind
shell stream tcp nowait root /etc/rshd rshd
talk dgram udp wait root /etc/talkd talkd
```