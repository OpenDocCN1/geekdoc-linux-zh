![](bbox=[0.19, 0.05, 0.95, 0.44])

*Figure 17.1: Ancillary data structures are composed of various substructures, data zones, and pad bytes.*

The control message header itself is defined as the following C structure:

```
struct cmsghdr {
 socklen_t cm_sg_len;
 int cm_sg_level;
 int cm_sg_type;
 /* u_char cm_sg_data[]; */
};
```

Table 17.3 describes the members of this structure in detail.

Table 17.3: The struct cm_sghdr Members

| Member | Description |
|---|---|
| cm_sg_len | This is the byte count of the ancillary data, which includes the size of this structural header. This value is computed by the CM SG_LEN() macro. |
| cm_sg_level | This value indicates the originating protocol level (for example, SOL_SOCKET). |
| cm_sg_type | This value indicates the control message type (for example, SCM_RIGHTS). |
| cm_sg_data | This member does not actually exist. It is shown in comments to illustrate where additional ancillary data is located physically. |