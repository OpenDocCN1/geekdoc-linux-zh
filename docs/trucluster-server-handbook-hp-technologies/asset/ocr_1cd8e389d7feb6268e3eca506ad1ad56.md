As of V5.1A, newline (\n) and tab (\t) characters can be used to increase the readability of your event output. For example, you can insert a newline into the event output by using a "\n".

```
# evmget -A -f "[age < 1d]" \
> -t "%n%t%timestamp - %event_id [%priority]%n%name\n%" | more
26-Sep-2002 03:43:59 - 344680 [200]
sys.unix.clu.drd.server_leave_hwid.52
DRD: Removed (unmapped) DRD server molari
```

Using the "s" character next to a filter keyword allows you set a minimum field width. For example, to set the minimum field width of a cluster_event field to five you can use the following command.

```
# evmget -A -f "[age < 1d]" \
> -t "@cluster_event%5 -@name" | more
True  - sys.unix.hw.net.niff.alert
False - sys.unix.evm.logger.log_closed
False - sys.unix.evm.logger.log_started
False - sys.unix.evm.mark
False - sys.unix.binlog.chan.binlog_size
False - sys.unix.binlog.hw.acsi
True  - sys.unix.clu.drd.server_leave_hwid.52
False - sys.unix.binlog.hw.acsi
True  - sys.unix.clu.drd.server_add_hwid.52
True  - sys.unix.clu.drd.new_accessnode_hwid.52
True  - sys.unix.clu.drd.new_accessnode_hwid.52
...
```

# 8.7.10 How Can I Find Out Which Filters are Available?

Filter keywords are defined in the EvmFilters(5) reference page. You can find filters defined in the filter files located in the /usr/share/evm/filters (system) and /var/evm/adm/filters (site defined) directories.

```
$ ls /var/evm/adm/filters /usr/share/evm/filters
/usr/share/evm/filters:
binlog.evf  evm.evf    sys.evf    syslog.evf
/var/evm/adm/filters:
<no output>
```

Also, the TruCluster Server Handbook web site (see Appendix B for the URL) contains a Korn Shell script called evf(1) that can be used to find out which filters are available in a filter file.