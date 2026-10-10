| Usage Restrictions | The vPar must not be running. <br> The I/O resource must be assigned to the target vPar. Only attributes may be modified. |

| Usage Guidelines | At most one device can be assigned the ALTBOOT and ROOT attributes. Assigning one of these attributes to a device silently deletes it from its former device, if any. <br> <br> Caution:You should assign attributes to appropriate devices, but this is not checked. For example, ALTBOOT and ROOT should be assigned to a disk or tape. Failure to do this may result in an unbootable partition. |

Task: -m mem=size

| Explanation | Specifies the total amount of memory, in megabytes rounded upward to a 64 megabyte boundary, to be allocated to the vPar. Any memory in excess of that specifically allocated by base and range is taken from unspecified ranges of memory available to the system when the partition boots. |

| Value | A positive 64-bit integer < 17592186044352 |

| Usage Restrictions | The vPar must not be running. <br> A decrease in total memory allocation must not result in a total less than that of all memory allocated in specific memory ranges. <br> <br> If the vPar is in the monitor database and the specification results in an increased memory allocation, the memory must physically exist and be available after the memory requirements of all other vPars have been satisfied. <br> <br> If the vPar is in an alternate database file and total memory is increased, the assignment always succeeds. The amount of memory actually allocated if the database is loaded into the monitor may be less if some or all of it is needed in other vPars. |

Task: -d cpu:path

| Explanation | De-assigns the bound CPU at the specified hardware path from the vPar and replaces it with a bound CPU of the monitor’s choice. Depending on availability, this may be the same CPU that was de-assigned. |

| Value | A text string of the form returned by the toscan(1M) command, such as “10/12/6” |

| Usage Restrictions | The vPar must not be running. The resource at the specified path must be a CPU resource. |