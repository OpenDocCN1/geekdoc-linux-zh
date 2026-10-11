# Part IV: Networking



```
netbios-dgm 138/udp
netbios-ssn 139/tcp # NETBIOS session service
netbios-ssn 139/udp
imap2 143/tcp # Interim Mail Access Proto v2
imap2 143/udp
snmp 161/udp # Simple Net Mgmt Proto
snmp-trap 162/udp # Traps for SNMP
cmip-man 163/tcp # ISO mgmt over IP (CMOT)
cmip-man 163/udp
cmip-agent 164/tcp
cmip-agent 164/udp
xdmcp 177/tcp # X Display Mgr. Control Proto
xdmcp 177/udp
nextstep 178/tcp NeXTStep NeXTStep # NeXTStep window
nextstep 178/tcp NeXTStep NeXTStep # server
bgp 179/tcp # Border Gateway Proto.
bgp 179/udp
prospero 191/tcp # Cliff Neuman's Prospero
prospero 191/udp
irc 194/tcp # Internet Relay Chat
irc 194/udp
smux 199/tcp # SNMP Unix Multiplexer
smux 199/udp
at-rtmp 201/tcp # AppleTalk routing
at-rtmp 201/udp
at-nbp 202/tcp # AppleTalk name binding
at-nbp 202/udp
at-echo 204/tcp # AppleTalk echo
at-echo 204/udp
at-zis 206/tcp # AppleTalk zone information
at-zis 206/udp
z3950 210/tcp wais # NISO 239.50 database
z3950 210/udp wais
ipx 213/tcp # IPX
ipx 213/udp
imap3 220/tcp # Interactive Mail Access
imap3 220/udp # Protocol v3
ulist serv 372/tcp # UNIX Lister serv
ulist serv 372/udp
#
# UNIX specific services
#
exec 512/tcp
biff 512/udp comsat
```