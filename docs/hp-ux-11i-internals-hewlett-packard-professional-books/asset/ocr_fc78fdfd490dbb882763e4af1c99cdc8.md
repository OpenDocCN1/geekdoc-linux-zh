![](bbox=[0.15, 0.08, 0.92, 0.44])

# Figure 11-5 PVRA and VGRA Components

Let's switch our focus to the VGRA and its components. The first part of the VGRA is the VGDA, which includes four main structures: VG_header, lvol[], pvol[], and VG_trailer. The configurable maximum number of logical volumes and physical volumes per volume group are used to size the lvol[] and pvol[] arrays respectively. The volume group tunables max_lv and max_pv may be set during the vgcreate command. Let's take a look at Listings 11.3 and 11.4:

# Listing 11.3 q4> fields struct VG_header

```
```
     First are the timestamps and identifier
     0 0 4 0 int      vg_timestamp.tv_sec
     4 0 4 0 int      vg_timestamp.tv_usec
    12 0 4 0 u_int    vg_id.id1
    16 0 4 0 u_int    vg_id.id2
     Next is the maximum number of logical volumes and physical
     volumes for the volume group
    16 0 2 0 u_short  maxlvs
    18 0 2 0 u_short  numpvs
     The maximum number of physical extents for the volume group
     and its status flag
    20 0 2 0 u_short  maxpexs
    22 0 2 0 u_short  flags
    24 0 4 0 u_int    reserved2
    28 0 4 0 u_int    reserved3
```
```