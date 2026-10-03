During the process of building the /devices directory, the devfsadmd daemon assigns each device a major device number by using the name-to-number mappings held in the /etc/name_to_major file. This file is maintained by the system and is undocumented. The following is a sample of the /etc/name_to_major file:

```
more /etc/name_to_major
cn 0
rootnex 1
pseudo 2
ip 3
logindmux 4
icmp 5
fas 6
hme 7
p9000 8
p9100 9
sp 10
clone 11
sad 12
mm 13
iwscn 14
wc 15
conskbd 16
consms 17
ipdcm 18
dump 19
se 20
log 21
sy 22
ptm 23
pts 24
ptc 25
pts1 26
bwtwo 27
audio 28
zs 29
cgthree 30
cgtwo 31
sd 32
st 33
...
...
envctrl 131
cvc 132
cvcredir 133
eide 134
hd 135
tadbat 136
ts102 137
simba 138
uata 139
dad 140
atapicd 141
```