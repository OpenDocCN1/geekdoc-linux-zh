some of the most common runtime and configuration problems and proposed solutions.

# **Error Message/Problem:**

Rateup WARNING: /rateup could not read the primary log file for 10.0.2.50.1
Rateup WARNING: /rateup The backup log file for 10.0.2.50.1 was invalid as well
Rateup WARNING: /rateup Can’t remove 10.0.2.50.1.old updating log file.

# *Solution*

Don’t worry about these errors. They occur once in while but don’t pose any serious problem and can be ignored. Unfortunately, there’s no way to disable the generation of these messages.

# **Error Message/Problem:**

No answer from community@device. You may be using the wrong community

# *Solution*

MRTG is having trouble polling a device with the SNMP community string specified in the configuration file. Check to ensure that the correct community string is being used for the device(s) having the problem. Also, make sure the device(s) can be polled from the network using another SNMP tool like snmpget or snmpwalk.

# **Error Message/Problem:**

```
```bash
./mrtg rmcon
ERROR: I guess another mrtg is running. A lockfile (rmcon_l) aged 264 seconds is hanging around. If you are sure that no other mrtg is running you can remove the lockfile.
```
```

# *Solution*

MRTG detected a lock file, which indicates that another copy of MRTG is presently running or ran in the past and failed to remove the lock file. Use the pg command to ensure that no additional MRTG process is running. If no additional process is running, remove the lock file.

# **Error Message/Problem:**

```
```
ERROR: I can’t find a "target[10.0.2.50.1]" definition
```
```