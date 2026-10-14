```
[sheridan]
# drdmgr -a server tape0

View of Data from member sheridan as of 2001-07-24:14:39:48
    Device Name: tape0
    Device Type: Served Tape
    Device Status: OK
    Number of Servers: 2
    Server Name: sheridan
    Server State: Server
    Server Name: molari
    Server State: Not Server
```

Now that sheridan is acting as the server, let’s reset the statistics and do some I/O from molari and sheridan this time.

```
[molari]
# drdmgr -a statistics=0 tape0
```

```
[molari]
# drdmgr -h sheridan -a statistics=0 tape0
```

```
[molari]
# tar -cvf /dev/tape/tape0 ./someCool.txtFile
a ./someCool.txtFile 50 Blocks
```

```
[molari]
# tar -tvf /dev/tape/tape0

blocksize = 20
-rw------- 0/0 25157 Jul 24 14:13:41 2001 ./someCool.txtFile
```

```
[sheridan]
# tar -cvf /dev/tape/tape0 ./someCool.txtFile
a ./someCool.txtFile 50 Blocks
```

```
[sheridan]
# tar -tvf /dev/tape/tape0

blocksize = 20
-rw------- 0/0 25157 Jul 24 14:13:41 2001 ./someCool.txtFile
```

The I/O should now be tallied on sheridan this time.