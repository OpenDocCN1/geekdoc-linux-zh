# 17.5 Multicasting in Today's Internet 361

daemon. The daemon passes data to the kernel as shown below. We use the example of a
query of the virtual network device and an MFC entry to explain the procedure:

Initially, the mouted daemon allocates memory space for a sioc_vif_struct-
ture and writes the index of the desired virtual network device to the wifi field. Calling
of the ioctl() SIOCGETVIFCNT command makes the appropriate part executed by the dae-
mpr_ioctl. The argument for the ioctl() command is the address by which the vif index points to
valid virtual network device. If this is the case, the referenced structure is filled with
the appropriate values and copied back to the user address space by copy_to_user().
Structure used to pass the data of a virtual network device is follows:

```
struct sioc_vif_req
include/linux/mroute.h
sioc_vif_req {
    vif_t           vifi;      /* Which iface *//
    unsigned long  icount;    /* In packets *//
    unsigned long  ocount;    /* Out packets *//
    unsigned long  ibytes;    /* In bytes *//
    unsigned long  obytes;    /* Out bytes *//
    unsigned long;
    unsigned long  obytes;      /* Out bytes *//
};
```

vif:This is the index of the virtual network device specified in the vif_table:
VIF used to request information.
icount, ocount: This is the number of packets received or sent, respectively,
over this VIF.
ibytes, obytes: This is the sum of bytes included in the packets received or sent.

The procedure in querying an entry in the multicast forwarding cache is
identical, except that the sioc_sg_req structure and the ioctl() command
SIOCGETSGCNT are used:

```
struct sioc_sg_req
include/linux/mroute.h
struct sioc_sg_req {
    struct          in_addr src;
    struct          in_addr grp;
    unsigned long   pktcnt;
    unsigned long   bytecnt;
    unsigned long   wrong_if;
    };
```

The elements of the sioc_sg_req structure handle the following tasks:

src:This is the sender address; it is part of the key for the MFC entry.
grp: This is the multicast group address; it is the second part of the key for the
MFC entry.