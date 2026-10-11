![](bbox=[0.18, 0.11, 0.29, 0.2])

When using the Shared Server option, each user’s sort area is taken from the UGA, not the server’s main memory.

# **Oracle Objective**

Set old and new sort parameters

# **SORT_AREA_RETAINED_SIZE**

By default, the value for SORT_AREA_RETAINED_SIZE is equal to the size of SORT_AREA_SIZE. The minimum size for this parameter is the equivalent of two Oracle blocks. The maximum size is limited to the value of SORT_AREA_SIZE. Once a sort operation is complete, if the sort area still contains sorted rows that need to be returned to the user, the user’s Server Process reduces the memory set aside for the final fetch to the value specified by SORT_AREA_RETAINED_SIZE.

The SORT_AREA_RETAINED_SIZE parameter can be set in init.ora, by using the ALTER SYSTEM SET SORT_AREA_RETAINED_SIZE=n DEFERRED command, or by using the ALTER SESSION SET SORT_AREA_RETAINED_SIZE=n command.

![](bbox=[0.18, 0.59, 0.29, 0.68])

Depending on the degree of parallelism specified, sorts performed using the Oracle Parallel Query option can require several times the amount of memory specified by SORT_AREA_SIZE.

# **PGA_AGGREGATE_TARGET**

After SORT_AREA_SIZE has been used to specify how much memory will be assigned for sorting to each user on a per-session basis, the parameter PGA_AGGREGATE_TARGET can be used to establish an upper boundary on the maximum amount of memory that all user processes can consume while performing database activities—including sorting. The default value for this init.ora parameter is zero. Valid values for PGA_AGGREGATE_TARGET are 10MB to 4000GB.