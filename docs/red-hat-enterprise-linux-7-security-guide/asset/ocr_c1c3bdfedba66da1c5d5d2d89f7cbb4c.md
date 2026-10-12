```
```bash
~]# aureport -u --failed --summary -i
```
```

To generate a summary report of all failed login attempts per each system user, use the following command:

```
```bash
~]# aureport --login --summary -i
```
```

To generate a report from an ausearch query that searches all file access events for user ID 1000, use the following command:

```
```bash
~]# ausearch --start today --loginuid 1000 --raw | aureport -f --summary
```
```

To generate a report of all Audit files that are queried and the time range of events they include, use the following command:

```
```bash
~]# aureport -t
```
```

For a full listing of all **aureport** options, see the aureport(8) man page.

# 6.9. ADDITIONAL RESOURCES

For more information about the Audit system, see the following sources.

# Online Sources

+   - The Linux Audit Documentation Project page: https://github.com/linux-audit/audit-documentation/wiki.

# Installed Documentation

Documentation provided by the audit package can be found in the `/usr/share/doc/audit/` directory.

# Manual Pages

+   - audispd.conf(5)

+   - auditd.conf(5)

+   - ausearch-expression(5)

+   - audit.rules(7)

+   - audispd(8)

+   - auditctl(8)

+   - auditd(8)

+   - aulast(8)

+   - aulastlog(8)

+   - aureport(8)