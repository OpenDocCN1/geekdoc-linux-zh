```
```ini
; /etc/samba/smb.conf
;
; Copyright (c) 1999 SuSE GmbH Nuernberg, Germany.
;
[global]
    workgroup = workgroup
    guest account = nobody
    keep alive = 30
    os level = 2
    kernel oplocks = false
    security = user

; Uncomment the following if you want to use an existing
; NT Server to authenticate users, but remember
; to create them locally.
; security = server
; password server = 192.168.1.10
; encrypt passwords = yes

    printing = bsd
    printcap name = /etc/printcap
    load printers = yes

    socket options = TCP_NODELAY

    map to guest = Bad User

; Uncomment this if you want to integrate your server
; into an existing net, e.g., with NT-WS to pre-
; vent net traffic
; local master = no

; Uncomment the following entry and replace the
; IP number and netmask with the correct numbers for
; your ethernet interface.
; interfaces = 192.168.1.1/255.255.255.0

; If you want Samba to act as a wins server, set
; wins support = yes
    wins support = no
```
```