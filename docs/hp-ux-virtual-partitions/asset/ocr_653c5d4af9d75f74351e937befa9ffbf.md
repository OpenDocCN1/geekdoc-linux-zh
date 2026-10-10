corresponding non-machine-readable display (-v or -A).

+   -w Displays the name of the current virtual partition (the one in which the command is executed). The monitor must be running.
+   
+   -e Displays the monitor's event log, a circular file roughly 4K bytes long. Once the file is full, new entries overlay old ones to the nearest character. As a result, the first entry displayed may be missing some leading characters. The monitor must be running.
+   
+   -P Displays Processor Information Module (PIM) data from the most recent reset of the specified virtual partition. If a virtual partition is not specified, PIM data from the current virtual partition, that is, the one in which the command is executed, is displayed.
+   
+   If the virtual partition has not been reset, or if PIM data has been cleared since then, no PIM data is available so a message to that effect is displayed. The monitor must be running.

RETURN VALUE

The vpartatus command exits with one of the following values:

0 Successful completion.

1 Syntax error or invalid option.

# EXAMPLES

These examples assume the existence of an N-class hardware system, Europe, on which the virtual partition database Norway is currently loaded in the virtual partition monitor.Norway has two configured virtual partitions: Oslo, and Bergen. The vpartatus command is run from Gslo.

Europe has eight CPUs, two System Bus Adapters (SBAs), each with six Local Bus Adapters (LBAs), and 2 Gbytes of main memory. These resources are allocated among Oslo and Bergen as follows:

+   Gslo:
+   
+   + Two bound CPUs at hardware paths 33 and 37. The CPU at 33 was specified by the user with the -a cpupath resource specification. The CPU at 37 was assigned by the monitor from the pool of CPUs available when Oslo was booted.
+   
+   + One Floating (unbound) CPU at hardware path 41.
+   
+   + One SCSI boot disk at SBA/LBA/path 0/0/2/0.6.0.
+   
+   + One terminal at 0/0/4/0.
+   
+   + One LBA (0/4) to which are attached several LAN adapters.
+   
+   + Specific memory addresses 0x0000000 to 0xC000000 (Range = 64 MB) and 0x2000000 to 0x60000000 (Range = 128 MB). These specific ranges are part of a total memory allocation of 768 MB.
+   
+   Bergen:
+   
+   + Two bound CPUs at hardware path 97 and 101, both assigned by the monitor.
+   
+   + Two unbound CPUs at hardware paths 93 and 99.
+   
+   + One SCSI boot disk at 1/4/0/0.5.0.
+   
+   + One LBA (1/10) to which are attached several LAN adapters
+   
+   + Specific memory 0x64000000 to 0x50000000 (Range = 192 MB) and 0x60000000 to 0x80000000 (Range = 512 MB). These specific ranges are part of a total memory allocation of 768 MB.