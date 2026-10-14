
+   - evmget (1)

Using the EVM_SHOW_TEMPLATE, you can define the information that is returned from the evmget, evmwatch(1), evmsort(1), and evmshow(1) commands.

```
# export EVM_SHOW_TEMPLATE=
> "@timestamp {@event_id}\n[@priority] @name\n@\n\n"
```

There are two cluster-related filter template files in the /usr/share/evm/filters directory as shown by the evf script that we wrote.

```
$ ./evf -vd /usr/share/evm/filters clu caa

/usr/share/evm/filters

clu.evf

@clu:clu          -> [name sys.unix.clu]
@clu:cfs          -> [name sys.unix.clu.cfs]
@clu:cnx          -> [name sys.unix.clu.cnx]
@clu:drd          -> [name sys.unix.clu.drd]
@clu:member       -> [name sys.unix.clu.member]
@clu:shutdown     -> [name sys.unix.clu.shutdown]
@clu:wall         -> [name sys.unix.clu.wall]
@clu:caa          -> [name sys.unix.clu.caa]
@clu:clua         -> [name sys.unix.clu.clua]

caa.evf

@caa:caa          -> [name sys.unix.clu.caa]
@caa:app          -> [name sys.unix.clu.caa.app]
@caa:cli          -> [name sys.unix.clu.caa.cli]
@caa:err          -> [name sys.unix.clu.caa.err]
@caa:res          -> [name sys.unix.clu.caa.res]
```

By setting the EVM_SHOW_TEMPLATE and using the "@clu" filter, you can retrieve all cluster-related events that have occurred using the following evmget command.

```
$ evmget -A -f @clu
29-Aug-2002 01:55:24 (13)
[200] sys.unix.clu.cnx.quorum.gain
CNX MGR: Node has (re)gained quorum (current votes 2, quorum votes 2)
--
```

When troubleshooting, it is often useful to cast a wide net and then draw it tight as appropriate (perhaps limiting the events to a specific time period); for example, to return all events that have occurred in the last two hours:

```
# evmget -A -f "[age < 2h]*"
29-Aug-2002 03:36:14 (968)
[200] sys.unix.clu.drd.new_accessnode__hwid.105
DRD: Server molari selected for device 105
...
```

Once you find an event of interest, you can get more information by using the evmshow command with the "-d" option.

## A.1.4 Parsing Events

Taking the event ID from the previous example, we can get more information as follows:

```
# evmget -f "[event_id = 968]" | evmshow -d
EVM Log event ================================
EVM event name: sys.unix.clu.drd.new_accessnode__hwid.105

This event is posted by a DRD client to indicate that it has
selected a server as a new access node for the specified device.

===============================================
Formatted Message:
DRD: Server molari selected for device 105

Event Data Items:
Event Name      : sys.unix.clu.drd.new_accessnode__hwid.105
Cluster Event   : True
Priority        : 200
PID             : 1061550
PPID            : 1061518
Event Id        : 968
Member Id       : 2
Timestamp       : 29-Aug-2002 03:36:14
Host IP address : 192.168.0.69
Cluster IP address: 192.168.0.70
Host Name       : sheridan.dec.com
Cluster Name    : babylon5
Format          : DRD: Server $server_name selected for device $_hwid
Reference       : cat:evmexp_clu.cat

Variable Items:
disk_type (STRING) = "SERVED"
server_name (STRING) = "molari"
_hwid (INT64) = 105
reason_code (INT32) = 0
```

![](img/a0df85c2e542a8d6c913113908553aa4_797_0.png)

![](img/a0df85c2e542a8d6c913113908553aa4_797_1.png)

![](img/a0df85c2e542a8d6c913113908553aa4_797_2.png)

![](img/a0df85c2e542a8d6c913113908553aa4_797_3.png)

## A.1.5.2 Memory Channel Address Space Window Size

In order for redundant Memory Channel rails to function with 512MB address space window size, each Memory Channel must be located in separate PCI buses. You can use the “show config” command to determine the location of the Memory Channel cards.

```
P00>>>show config

    Bus 00  Slot 08: DEC PCI MC                         mca0.0.0.8.0        Rev: 22, mca0

    Bus 01  Slot 03: DEC PCI MC                         mca1.1.0.3.0        Rev: 22, mca1
```

```
>>> mc_diag -d
LCERR  MC PORT  PEBAR  CFG304  CFG10  MODCFG  POS
mca0 - 00204800 00000000 42400000 80000000 04000006 40000008 0000000b 00000004
mca1 - 00204800 00000000 42400000 80000000 04000006 48000008 0000000b 00000004
```

### Figure A-5: Memory Channel 2 Memory Window Size of 512MB

How can you determine the address space window size without looking at the card? Bit 2 of the MODCFG field indicates memory window size. If bit 2 is not set, the address space window size is 512MB. See Figure A-5.

## A.1.5.3 The MCERR Field

The MCERR field should always be zeroes. However, a non-zero MCERR field is not necessarily fatal. We have seen an instance where the Memory Channel on a DS10 system does not complete its power-up self-test before the SRM console is ready. If this happens, run the init command, which should clear the problem. If it does not clear the error, you can cycle power on the system. As a last resort to clear the error before logging a call with HP, power off the system and reseat the card.

For more information on the "mc_diag -d" bit fields, see Chapter 3 (Troubleshooting) of the Memory Channel Service Information Guide, which shipped with your Memory Channel hardware. The guide also contains additional tips for troubleshooting the Memory Channel hardware as well.

## A.1.6 CNX Problems (quorum, CNX boot hangs, etc.)

If you experience quorum problems or the cluster seems to hang and CNX messages are displayed on the console, try setting the sysconfig debug values in cnx:msg_level (default 1) and cnx:debug_msg_level (default 0) each to 5 either at boot time (by modifying /etc/sysconfigtab) or in real time using "sysconfig -r cnx <attribute>=5". These settings cause more verbose CNX messages to be logged to the console, /var/adm/messages and /var/adm/syslog.dated/current/kern.log, and can help you or HP Support with additional clues about the CNX behavior in your cluster.

## A.1.7 Unable to See Your Shared Storage from Your Cluster Members

This is usually a persistent reservation problem and should only happen in isolated situations. Refer back to sections 15.13 and 22.5 for details about I/O Barriers and when they might get in your way. You can check for persistent reservations from the perspective of the cluster with "cleanPR show":
