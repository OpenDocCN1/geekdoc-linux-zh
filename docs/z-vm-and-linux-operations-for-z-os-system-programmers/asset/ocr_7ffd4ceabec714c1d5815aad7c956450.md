Finally, the QUERY ALLOC TDISK displays all defined and assigned temporary disk space, as shown in Example 5-9.

# Example 5-9 Checking the amount of TDISK allocated

```
q alloc tdisk
VOLID RDEV EXTENT START EXTENT END TOTAL IN USE HIGH % USED
---------------- ----------------
LX6TDK 8225 1 3338 3338 20 20 1%
---------------- ----------------
SUMMARY 3338 20 1% CKD
USABLE 3338 20 1% CKD
Ready; T=0.01/0.01 11:06:01
```

# Checking system dump space configuration: query dump

The QUERY DUMP command (abbreviated Q DUMP), in Example 5-10, shows:

+   - The device type and unit or units assigned to receive CP abnormal termination dumps
+   - The current settings of the DUMP options

# Example 5-10 Querying the DUMP configuration

```
q dump
DASD 1A21 dump unit CP IPL pages 31437
Ready; T=0.01/0.01 11:57:09
```

# Checking the recording status: query recording

The QUERY RECORDING command (abbreviated as Q REC) checks the status of the following items:

+   - CP data collection for these records:
+     - Accounting
+     - EREP (errors recording)
+   - CP data collection for symptom records
+   - Active retrieval of these records

In Example 5-11 on page 242, all recordings are active, using the defaults user IDs defined in z/VM: EREP userid for error recording, ACCOUNT for accounting information, and OPERSYMP for symptoms records gathering. The count field shows any unprocessed records.