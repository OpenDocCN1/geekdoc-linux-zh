```
nproc 400 500
npty 60 60
netpty 60 60
netctl 60 60
nmapdev 10 10
nswapfs 10 10
nyswap 800 800
neymap64 800 800
num_tachyon_adapters 0 0
o_sync_is_o_dsync 0 0
page_razt_to_local - -
pfint_hash_locks 128 128
public_shilks 1 1
region_hash_locks 128 128
remote_nfs_swap 0 0
rtached_numpr 32 32
scroll_lines 100 100
srai_maxphys 1048576 1048576
seema - 1
semsem 16384 16384
semmap 66 66
semmsm 64 64
semmsa 128 128
semmni 30 30
semnum 10 10
semvmx 32767 32767
sendfile_max 0 0
shmes 1 1
shmmax 0x40000000 0x50000000
shmni 200 200
shmseg 120 120
st_atm_enabled 1 1
st_fail_overruns 0 0
st_large_recs 0 0
streampipes 0 0
swapmem_on 1 1
swchunk 2048 2048
sysv_hash_locks 128 128
tophasher 0 0
timeslice 10 10
timzone 420 420
unlockable_mem 0 0
vas_hash_locks 128 128
vnodc_od_hash_locks 128 128
vnodc_hash_locks 128 128
vpcs_ceiling 16 16
vpcs_char_ceiling 1048576 1048576
vpcs_pagesize 4 4
vx_fancyra_enable 0 -
vv_maxlink 32767 32767
vv_ncsize 1024 1024
vzfs_max_ra_kbytes 1024 1024
vzfs_ra_per_disk 1024 1024
#
```

Issuing **kmtune** with the *-*l* option produces a detailed listing of the kernel. The following shows just the output for one of the parameters:

```
# kmtune -l
Parameter: maxuprc
Current: 77
Planned: 77
Default: 75
Minimum: -
```