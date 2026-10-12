```
ifInDiscards.1 /1 sec: 0
ifInDiscards.1 /1 sec: 0
ifInDiscards.1 /1 sec: 0
ifInDiscards.1 /1 sec: 0
ifInDiscards.1 /1 sec: 0
ifInDiscards.1 /1 sec: 0
ifInDiscards.1 /1 sec: 0
ifInDiscards.1 /1 sec: 0
```

Without user interaction, the above command continually polls the agent until a control+c (c) is issued by the user. Note that in the command we have used, the `-R` option activates random access to the agent MIB. This makes it easy to obtain the desired MIB objects. A high discard rate may indicate trouble with the interface. This trouble could be caused by a hardware problem related to cabling or even a software configuration error. In the example above, the discard rate didn't change and is why the values are all zero. This command supports a number of additional command-line arguments over the common options previously discussed. Table 8.4 lists the available options.

Table 8.4 Additional snmpdelta command-line options

| Option | Description | | --- | --- | | `-f` | Reads a configuration file | | `-k` | Displays time information in output | | `-l` | Writes the configuration to a file | | `-m` | Displays the maximum value ever retrieved | | `-p` | Specifies the polling period | | `-P` | Specifies the reporting period as a number of polling requests | | `-s` | Displays timestamp information | | `-S` | Logs data to a log file | | `-t` | Determines time interval | | `-T` | Produces table output |