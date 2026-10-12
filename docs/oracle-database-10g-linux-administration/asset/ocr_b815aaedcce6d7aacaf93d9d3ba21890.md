The EVMD is the event manager daemon that starts the RACGEVT process. This daemon will generate events when things happen to the cluster. It spawns a permanent child, emvlogger. EVMD scans the callout directory and invokes callouts. Like CRSd, this daemon is restarted automatically upon failure, but it runs as the oracle user.

There is a fourth daemon, OPRCD, which will only appear on platforms that do not use vendor clusterware with the CRS. OPRCD is the process monitor for the cluster. There is only one set of these daemons running on each node no matter how many Oracle instances are running.

Each daemon has a set of logfiles, which are found in the following locations:

| Daemon | Logfile location |
|---|---|
| CRSd | $CRS_HOME/crs/log |
| EVMD | $CRS_HOME/evm/log |
| OCRD | $CRS_HOME/ocr/log |

CRS is started automatically whenever the system is rebooted. The DBA or Systems Administrator can also stop and start the CRS manually by executing the following commands:

```
```
/etc/init.d/init.crs start
/etc/init.d/init.crs stop
```
```

The CRS requires both the voting disk and the OCR, and if either of these files is not available, CRS will not start. CRS must be up and running before the Oracle RAC instances can be mounted. Three network addresses are required for the CRS: a public IP address, a private interconnect IP address, and a virtual IP address (VIP). The VIP and public addresses must be set up in DNS prior to the CRS installation.

The command to see the status of the CRS is crs_stat. The format of the output of this command is difficult to read, so I recommend running a script to better format the output. Here is a sample script that will return the output from the crs_stat binary in a more readable form.

```
```
crs_stat.sh
#!/usr/bin/ksh

# Sample 10g CRS resource status query script
#
# Description:
# - Returns formatted version of crs_stat -t, in tabular
#   format, with the complete rsc name and filtering keywords
# - The argument, $RSC_KEY, is optional and if passed to the script, will
#   limit the output to HA resources whose names match $RSC_KEY.
```
```