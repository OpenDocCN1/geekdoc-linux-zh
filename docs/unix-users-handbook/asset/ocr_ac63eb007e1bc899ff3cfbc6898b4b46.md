| bwr t/s | Number of physical writes per second from the buffer cache to the disk (or other block device); |

| lread/s | Number of reads per second from buffer cache; |

| lwr it/s | Number of writes per second to buffer cache; |

| %r cache | Buffer cache hit ratio for read requests e.g., 1 - bread/lread; |

| %w cache | Buffer cache hit ratio for write requests e.g., 1 - bwr it/lwr it; |

| pread/s | Number of reads per second from character device using the physio() (raw I/O) mechanism; |

| pwr it/s | Number of writes per second to character device using the physio() (i.e., raw I/O) mechanism; |

-d Report activity for each block device, e.g., disk or tape drive. One line is printed for each device that had activity during the last interval. If no devices were active, a blank line is printed. Each line contains the following data:

device Logical name of the device and its corresponding instance. Devices are categorized into the following four device types:
diskl - HP-IB disks (CS/80)
disk2 - CIO HP-FL disks (CS/80)
disk3 - SCSI and NIO FL disks
sdisk - SCSI disks;

| %busy | Portion of time device was busy servicing a request; |

| avque | Average number of requests outstanding for the device; |

| r+w/s | Number of data transfers per second (read and writes) from and to the device; |

| blks/s | Number of bytes transferred (in 512-byte units) from and to the device; |

| await | Average time (in milliseconds) that transfer requests waited idly on queue for the device; |

| aserv | Average time (in milliseconds) to service each transfer request (includes seek, rotational latency, and data transfer times) for the device. |

-y Report tty device activity: