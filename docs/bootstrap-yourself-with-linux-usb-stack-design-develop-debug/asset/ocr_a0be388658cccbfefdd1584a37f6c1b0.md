# Chapter 18 = Debugging Using Linux USB

The devnum member variable indicates the device for which URB event took place. The Linux kernel assigns a unique number to each USB device, starting from 1.

```
char devnum;
```

The epnum member variable indicates the endpoint to which the URB is processed. The endpoint value starts from 0.

```
char epnum;
```

The next variable, is_in, represents the direction of the URB event, with true indicating an IN USB transfer and false indicating an OUT USB transfer.

```
char is_in;
```

The next variable, xtype, represents different transfer types available on USB. The variable can hold B, I, Z, or C, representing bulk, interrupt, isochronous, and control transfers, respectively.

```
char xtype;
```

The next member, length, maps the length of data transferred in the URB. The could be the actual buffer length or the transferred length.

```
int length;
```

The next member, status, indicates the status of URB transfer. This field is valid for nonisochronous URB transfers. The return status is based on the values defined in include/linux/errno.h.

```
int status;
```

The interval member variable indicates the transfer period for time-bounded transfers as interrupt and isochronous transfers. The interval is based on the device configuration.

```
int interval;
```

The next member, start_frame, is specific to isochronous transfers and indicates the initial frame of the isochronous transfer.

```
int start_frame;
```

The member variable, error_count, is also specific to isochronous transfers and indicates the number of errors in the isochronous transfer.

```
int error_count;
```