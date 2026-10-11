# **NOTE**

Just because a drive supports hardware data compression doesn't mean that you must use that feature. You can usually disable it through a jumper setting or a command issued through the Linux *mt* utility. Doing so can be convenient if you need to exchange tapes between two drives, one of which supports hardware compression and the other doesn't.

# # Read-After-Write Verification

Many of the more advanced drives support a feature known as *read-after-write verification*. In this configuration, a read head is placed so that it can read the data immediately after it is written by the write head, as depicted in Figure 8.4. The drive can then read the data immediately after it's been written, and if the drive detects an error, it can rewind the tape and write the data again. This feature can add substantially to the reliability of a tape drive.

![](bbox=[0.28, 0.45, 0.78, 0.77])

# **FIGURE 8.4**

*A given point on the tape passes under the write head, and then under the read head, enabling the drive to verify that the data were written correctly.*

If you don't have read-after-write verification, it's important that you perform a verify pass on the tape immediately after you create it. This operation reads the tape's data and compares