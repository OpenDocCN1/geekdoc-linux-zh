# 8.4.3 DASD errors

The characteristics of DASD errors are:

+   State: DASD error messages in /var/log/messages (see Example 8-12).

```
Example 8-12 /var/log/messages
Apr 19 15:14:09 xx kernel: dasd: 0.0.0104: Interrupt fastpath failed!
Apr 19 15:14:09 xx kernel: dasd: 0.0.0106: Interrupt fastpath failed!
Apr 19 15:14:09 xx kernel: dasd_erp: 0.0.0104: default ERP called (254 retries left)
Apr 19 15:14:09 xx kernel: dasd_erp: 0.0.0106: default ERP called (254 retries left)
Apr 19 15:14:09 xx kernel: dasd_erp: 0.0.0100: default ERP called (255 retries left)
Apr 19 15:14:09 xx kernel: dasd_erp: 0.0.0103: default ERP called (255 retries left)
Apr 19 15:14:10 xx kernel: dasd: 0.0.010c: Interrupt fastpath failed!
```

+   Environment: SLES9 SP3 on System z (not related on LPAR or on z/VM).
+   Information gathered: dbginfo.sh (especially /var/log/messages).
+   Analysis step
+   Search the error messages. Messages report an error when I/O requests are performed.
+   Error messages are displayed in some device address on the same path. Confirm that this is a hardware error or a hardware change with hardware support person.
+   Result and solution: hardware temporary error. ESS detected the temporary error of the FC adapter at the same time. ESS does a warm start (about 2 seconds). If there is no longer a problem, ESS has recovered normally.
+   Tips: It appears to be a path error if the error occurs in some address on the same path.