
```
% disklabel -r rz6

# /dev/rdisk/dsk6a:
type: SCSI
disk: rzw7s
label:
flags:
bytes/sector: 512
sectors/track: 71
tracks/cylinder: 15
sectors/cylinder: 1065
cylinders: 1900
sectors/unit: 2023500
rpm: 3600
interleave: 1
trackskew: 0
cylinderskew: 0
headswitch: 0
# milliseconds
track-to-track seek: 0
# milliseconds
drivedata: 0

8 partitions:
# size
a: 131072
b: 262144
c: 202350
d: 163840
e: 32768
f: 122956
g: 131072

offset fype bsize (Cyl.)
a 0 unused 1024 8192 (0-123)
b 0 unused 1024 8192 (0-369)
c 0 unused 1024 8192 (0-553)
d 0 unused 1024 8192 (0-784)
e 0 unused 1024 8192 (0-999)
f 0 unused 1024 8192 (0-1599)
g 0 unused 1024 8192 (0-1784)
h 0 unused 1024 8192 (0-3916)
```
