405GP User’s Manual, we determine that this will produce a refresh request every 15.2 microseconds. As with the other timing parameters, this value is dictated by the SDRAM chip specifications.

A typical SDRAM chip requires one refresh cycle for each row. Each row must be refreshed in the minimum time specified by the manufacturer. In the chip referenced in Section D.4.1, “Suggestions for Additional Reading,” the manufacturer specifies that 8,192 rows must be refreshed every 64 milliseconds. This requires generating a refresh cycle every 7.8 microseconds to meet the specifications for this particular device.

# ### D.4 Summary

SDRAM devices are quite complex. This appendix presented a very simple example to help you navigate the complexities of SDRAM controller setup. The SDRAM controllers perform a critical function and must be properly set up. There is no substitute to diving into a specification and digesting the information presented. The two example documents referenced in this appendix are excellent starting points.

# #### D.4.1 Suggestions for Additional Reading

+   AMCC 405GP Embedded Processor User’s Manual
+   AMCC Corporation
+   www.amcc.com/Embedded/

+   Micron Technology, Inc.
+   Synchronous DRAM MT48LC64M4A2 Data Sheet
+   http://download.micron.com/pdf/datasheets/dram/sdram/256MSDRAM. pdf