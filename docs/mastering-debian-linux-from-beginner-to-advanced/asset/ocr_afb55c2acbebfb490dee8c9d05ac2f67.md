```
sudo nano /etc/rsyslog.d/custom.conf
```

+   2. Add your custom rules, for example:

```
:programname, iseqial, "myapp" /var/log/myapp.log
```

This rule sends all logs from a program named "myapp" to `/var/log/myapp.log`.

+   3. Restart the rsyslog service:

```
sudo systemctl restart rsyslog
```

# Syslog Security Considerations

+   1. **Log file permissions:** Ensure log files have appropriate permissions to prevent unauthorized access.

```
sudo chmod 640 /var/log/syslog
sudo chown syslog:adm /var/log/syslog
```

+   2. **Network security:** When using remote logging, consider using encryption (TLS) to protect log data in transit.