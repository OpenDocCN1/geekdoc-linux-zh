Long Driver Na:\ Driver File Na:\ Data File Na:\ Config File Na:\ Help File Na:\ Language Monitor Na:\ Default Data Type:\ Comma Separated list of Files

Any empty fields should be enter as the string “NULL”.

Saa does not need to support the concept of Print Monitors since these only apply to local printers whose driver can make use of a bi-directional link for comnocation. This field should be “NULL”. On a remote NT print server, the Print Monitor for a driver st already be installed prior to adding the driver or else the RPC will fail.

The version parater lets you specify the printer driver version nuer. If omitted, the default driver version for the specified architecture will be used. This option can be used to upload Windows 2000 (version 3) printer drivers.

```
addprinter <printer a> <share a> <driver n a> <port >
```

Add a printer on the remote server. This printer will be automatically shared. Be aware that the printer driver st already be installed on the server (see adddriver) and the *port st* be a valid port na (see enumports.

```
deldriver <driver >
```

Delete the specified printer driver for all architectures. This does not delete the actual driver files from the server, only the entry from the server’s list of drivers.

```
deldriverex <driver > [architecture] [version] [flags]
```

Delete the specified printer driver and optionally files associated with the driver. You can limit this action to a specific architecture and a specific version. If no architecture is given, all driver files of that driver will be deleted. *flags* correspond to nurlc DPD_* values, i.e. a value of 3 requests (DPD_DELETE_UNUSED_FILES | DPD_DELETE_SPECIFIC_VERSION).

```
enumdata
```

Enumerate all printer setting data stored on the server. On Windows NT clients, these values are stored in the registry, while Saa servers store them in the printers TDB. This command corresponds to the MS Platform SDK GetPrinterData() function (* This command is currently unimplemented).

```
enumdataex
```

Enumerate printer data for a key

```
enumjobs <printer >
```

List the jobs and status of a given printer. This command corresponds to the MS Platform SDK EnumJobs() function