+   - Now we create a Striped set from the two Mirror sets that we had just created.

```
HSG> add stripeset clu_sys m1 m2
```

+   - Finally, we initialize and save the RAID configuration to the newly created Striped Mirror set.

```
HSG> initialize clu_sys save_configuration
```

Partition the RAID 0+1 set.

You may notice that partitioning the RAID 0+1 set and creating and configuring the partitioned storage units pretty much duplicates the RAID 5 example. There is nothing new to this.

```
HSG> create_partition clu_sys size=14
HSG> create_partition clu_sys size=14
HSG> create_partition clu_sys size=14
HSG> create_partition clu_sys size=14
HSG> create_partition clu_sys size=1
HSG> create_partition clu_sys size=largest
```

Create the partitioned storage units.

```
HSG> add unit d21 clu_sys partition=1 disable_access_path=all
HSG> add unit d22 clu_sys partition=2 disable_access_path=all
HSG> add unit d23 clu_sys partition=3 disable_access_path=all
HSG> add unit d24 clu_sys partition=4 disable_access_path=all
HSG> add unit d25 clu_sys partition=5 disable_access_path=all
HSG> add unit d26 clu_sys partition=6 disable_access_path=all
```

Configure the partitioned storage units.

```
HSG> set d21 identifier=21 enable_access_path=(MORLRA1,MORLRA2,SHER1A1,SHER1B2)
HSG> set d22 identifier=22 enable_access_path=(MORLRA1,MORLRA2,SHER1A1,SHER1B2)
HSG> set d23 identifier=23 enable_access_path=(MORLRA1,MORLRA2,SHER1A1,SHER1B2)
HSG> set d24 identifier=24 enable_access_path=(MORLRA1,MORLRA2,SHER1A1,SHER1B2)
HSG> set d25 identifier=25 enable_access_path=(MORLRA1,MORLRA2,SHER1A1,SHER1B2)
HSG> set d26 identifier=26 enable_access_path=(MORLRA1,MORLRA2,SHER1A1,SHER1B2)
```

# 4.2.4.6  Building RAID Sets for Other “Important” File Systems

As we indicated earlier, all RAID storage sets and storage units should be configured ahead of time and before you install Tru64 UNIX. We further recommend that other important file systems would certainly benefit from using RAID sets, including the users’ home directory area, the file systems