certificate using a local overlay for writes, a readahead of 64k and a tiout of 10 seconds.

```
```
qe-img create -f qcow2 -o backing_file='{"file.driver":"https", "file.url":"&fdSna-datastore1", "file.sslverify":"off", "file.readahead":"64k", "file.tiout":10}' /tmp/test.qcow2 qe-system-x86_64 -drive file=/tmp/test.qcow2
```
```

Bluetooth(R) options:

**-bt hci[...]**
Defines the function of the corresponding Bluetooth HCI. -bt options are matched with the HCIs present in the chosen machine type. For example when elating a machine with only one HCI built into it, only the first `-bt hci[...]` option is valid and defines the HCI's logic. The Transport Layer is decided by the machine type. Currently the machines n800 and n810 have one HCI and all other machines have none.

The following three types are recognized:

**-bt hci,null**
(default) The corresponding Bluetooth HCI assus no internal logic and will not respond to any HCI commands or emit events.

**-bt hci,host[;id]**
(bluez only) The corresponding HCI passes commands / events to / from the physical HCI identified by the na id (default: hc i0) on the computer running QEMU. Only available on bluez capable systems like Linux.

**-bt hci,vlan=n**
Add a virtual, standard HCI that will participate in the Bluetooth scatternet n (default 0). Similarly to -net VLANs, devices inside a bluetooth network n can only commicate with other devices in the sa network (scatternet).

**-bt vchi[,vlan=n]** (Linux-host only) Create a HCI in scatternet n (default 0) attached to the host bluetooth stack instead of to the elated target. This allows the host and target machines to participate in a common scatternet and cormuniate. Requires the Linux vchi driver installed. Can be used as following:

```
```
qe-system-i386 [...OPTIONS...] -bt hci,vlan=5 -bt vchi,vlan=5
```
```

**-bt device:dev[,vlan=n]** Elate a bluetooth device dev and place it in network n (default 0). QEMU can only elate one type of bluetooth devices currently:

**keyboard**
Virtual wireless keyboard implenting the HDP bluetooth profile.

TPM device options:
The general form of a TPM device option is:

**-tpmdev backend ,id=id [options]**
Backend type st be: passthrough.

The specific backend type will determine the applicable options. The -tpmdev option