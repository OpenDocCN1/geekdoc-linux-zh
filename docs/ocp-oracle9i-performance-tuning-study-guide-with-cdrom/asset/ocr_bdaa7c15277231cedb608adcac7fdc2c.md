| NAME | BYTES |
| :--- | :--- |
| PX msg pool | 2347731 |
| free memory | 612030 |

The value for free memory shown in this view can be used to help tune the size of the Large Pool. If V$SGASTAT shows high or increasing values for free memory, you have probably overallocated space to the Large Pool. If you have low or decreasing values for free memory, you may need to consider increasing the Large Pool size.

# ## Improving the Performance of the Large Pool

When warranted by the query shown above, you can increase the size of the Large Pool by increasing the value for LARGE_POOL_SIZE in the init.ora. The size of the Large Pool can be specified in bytes, kilobytes (using the K suffix), or megabytes (using the M suffix). The range of values for LARGE_POOL_SIZE is 600K to 2GB or more depending on operating system. The value of LARGE_POOL_SIZE cannot be changed dynamically using the ALTER SYSTEM command.

# ### Real World Scenario
**Using the Large Pool to Resolve RMAN Error**

You are running nightly hot backups using the Oracle RMAN utility. You’ve noticed that you are occasionally finding ORA-04031 unable to allocate x bytes of shared memory errors in your Alert Log during the time the backup was running. Additionally, users are complaining of poor application performance during the hot backup period.

When using the Recovery Manager feature in Oracle, RMAN will buffer its I/O activity in the Shared Pool. If database activity is high during the time that the RMAN backup is running, ORA-04031 unable to allocate x bytes of shared memory errors can result. This error indicates that a large piece of contiguous memory was requested in the Shared Pool, but could not be obtained. If this request is coming from RMAN, errors in the backup and poor application performance can result.

When the Large Pool is present, RMAN will use the Large Pool to buffer this I/O instead of the Shared Pool. This will result in not only better RMAN performance but also in improved Shared Pool hit ratios.