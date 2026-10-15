
# SUSE Linux Enterprise Server 10: 安全

日志文件 `/var/log/messages` 提供了关于连接建立的价值信息。如果连接成功建立，信息将类似于以下来自 `/var/log/messages` 的摘录（此列表中已删除时间戳）：

```
kernel: NET: Registered protocol family 15

kernel: Initializing IPsec netlink socket

ipsec_setup: KLIPS ipsec0 on eth0 10.0.0.10/255.255.255.0 broadcast 10.0.0.255

ipsec_pluto: Starting Pluto subsystem...

ipsec_setup: ..Openswan IPsec started

ipsec_setup: Starting Openswan IPsec 2.4.4...

ipsec_setup: insmod
/lib/modules/2.6.16.11-7-default/kernel/net/key/af_key.ko

ipsec_setup: ipsec: insmod
/lib/modules/2.6.16.11-7-default/kernel/net/ipv4/xfrm4_tunnel.ko

ipsec_setup: insmod
/lib/modules/2.6.16.11-7-default/net/xfrm/user.ko

pluto[4040]: Starting Pluto (Openswan Version 2.4.4.509-1.5.4)

pluto[4044]: PLUTO_VENDORS_PLUTO_KEYSR: Vendor ID OE:)PPFR_gr_

pluto[4040]: Changing Nat-Traversal port-4500 floating to off

pluto[4040]: including Nat-Traversal activation criteria nat_t0/port_load=1

pluto[4040]: ike_alg_register_enc(): Activating OAKLEY_AES_CBC: On (ret=0)

pluto[4040]: [disabled] starting up 1 cryptographic helpers

pluto[4040]: started helper pid=4054(6d)

pluto[4044]: Using Linux 2.6 IPsec interface code on 2.6.16.11-7-default

pluto[4044]: Changing to directory /etc/ipsec.d/certs

pluto[4044]: loaded cert file /dalo0-cert.pem (1956 bytes)

pluto[4044]: Could not change to directory /etc/ipsec.d/acerts

pluto[4044]: Could not change directory /etc/ipsec.d/ocspcerts

pluto[4044]: Changing to directory /etc/ipsec.d/crl

pluto[4044]: Warning: empty directory

pluto[4044]: loaded host cert /etc/ipsec.d/certs/dalo0_cert.pem (1960 bytes)

pluto[4044]: added connection description "dalo0-da20"

pluto[4044]: listening for IKE messages

pluto[4044]: adding interface eth0/eth0 10.0.0.10:500

pluto[4044]: adding interface lo/lo 127.0.0.1:500

pluto[4044]: adding interface lo//:::500

pluto[4044]: loading secrets from /etc/ipsec.secrets

pluto[4044]: loaded private key file /etc/ipsec.d/private/dalo0_key.pem (1751 bytes)
```

```
pluto[4044]: "da10-da20" #1: initiating Main Mode
pluto[4044]: "da10-da20" #1: received Vendor ID payload (Openswan (this version) 2.4.4 X.509-1.5.4 PLUTO_SENDS_VENDORID PLUTO_USES_KEYRR)
pluto[4044]: "da10-da20" #1: received Vendor ID payload [Dead Peer Detection]
pluto[4044]: "da10-da20" #1: transition from state STATE_MAIN_I1 to state STATE_MAIN_I2
pluto[4044]: "da10-da20" #1: STATE_MAIN_I2: sent MI2, expecting MR2
pluto[4044]: "da10-da20" #1: I am sending my cert
pluto[4044]: "da10-da20" #1: I am sending a certificate request
pluto[4044]: "da10-da20" #1: transition from state STATE_MAIN_I2 to state STATE_MAIN_I3
pluto[4044]: "da10-da20" #1: STATE_MAIN_I3: sent MI3, expecting MR3
pluto[4044]: "da10-da20" #1: Main mode peer is ID_ASN_DN: CDE, St_Bvaria, O=Digitalairlines, OU=Training, CN=da20.digitalairlines.com
pluto[4044]: "da10-da20" #1: no crl from issuer='C=DE, St_Bvaria, O=Digitalairlines, OU=Training, CN=da20.digitalairlines.com
```
