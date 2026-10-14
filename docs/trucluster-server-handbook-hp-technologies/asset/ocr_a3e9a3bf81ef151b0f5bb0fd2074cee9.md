The error will look like this:

```
```text
# dsmgr -e dsk7 dsk9

dsmgr: ERROR: find device node dsk9  : Device record not found in status database
dsmgr: ERROR: exchange failed: Device record not found in status database
```
```

Follow the “How Do I Fix a “second device status is active” Error?” procedure (section 7.5.1.4) to resolve the problem.

# 7.5.1.7  How Can I Verify that My Device Special File Databases are Error Free?

```
```text
# dsmgr -v

dsmgr: verify all datum for system at /

Default File Tree:
    OK.

Device Class Directory Default Database:
    OK.

Device Category to Class Directory Database:
    OK.

Dev directory structure:
    OK.

Device Status Files:
    OK.

Dev Nodes:
    OK.
```
```

# 7.5.1.8  How Can I Repair Errors in My Device Special File Databases?

Fix database errors or inconsistencies (output not shown). Note this may need to be run a few times to correct errors.

```
```text
# dsmgr -vF
```
```