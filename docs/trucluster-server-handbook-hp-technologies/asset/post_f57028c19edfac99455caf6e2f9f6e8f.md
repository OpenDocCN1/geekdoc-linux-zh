
defined, 28, 555
relationships, 28
for resource synchronization, 489
use of, 556
dn_setup command, 193–94
defined, 193
-init option, 193
-install_tape option, 194
LSM and, 402
-sanity_check option, 194
Domain Name Service (DNS) server
specification, 135, 139
DRD clients, 405
drdmgr (8) command, 276–77
-a switch, 413, 414
for checking paths to devices, 421
-h switch, 415, 416
output, 421
DRD server, 405
ds.fmgr command, 173, 188–93, 318–20
database files, 188–89
defined, 188
-e option, 191, 192
-K option, 181, 189
-m option, 189, 190
-O option, 320
-o option, 320
options, 319
reference, 193
-R option, 191
-s option, 189, 319, 587
using, 318–20
-vF option, 192
-V option, 192
-Z option, 190
dumpsys (8) command, 799
dupatch program, 254, 255
in Non-Rolling Patch Upgrade, 783–84
rolling cluster members after, 777
dxkernel_tuner (8) command, 354
Dynamic Device Recognition (DDR)
database, 174
Dynamic Host Configuration Protocol (DHCP), 602–3
clients, 602, 603
database, 603
defined, 602
server, 602, 603
Dynamic routing
of cluster aliases, 449
daemons, 449–50
EISA Configuration Utility (ECU), 87
defined, 759
firmware, updating, 87–88
Electronic resources, 813–19
mailing lists, 814
USENET newsgroups, 814
WWW (HP), 815–18
WWW (non-HP), 818–19
See also Resources (Tru64 UNIX/TruCluster Server)
E-mail server specification, 136, 141
Emergency Repair (ER) disk, 58, 645, 808
Encapsulation, 381–82
AdvFS domain, 392–94
decision, 383
defined, 381
disk, 394
disk partition, 394
LSM migration vs., 381–82
swap partition, 394–96
uncapsulation and, 396–401
verification, 393
with volencap (8) command, 391–96
Environment Variables (action scripts), 713–18
__CAA_CLIENT_LOCALE, 717
__CAA_REASON, 714
__SCRIPT_TIMEOUT, 713
categories, 713
locale information, 717–18
profile attribute, 713–14
reason code, 714
user-defined attribute, 714–17
Errors
AdvFS I/O, 811
boot, 810
"device record not found in status database," 191–92
device special file databases, repairing, 192–93
"second device status is active," 190–91
Essential Service Monitor daemon (esmd), 628–29
Event Manager (EVM), 26, 195–229, 320–24
additions in cluster, 322
API, 216
API shared library, 196
applications, 196
channel manager, 199
channels, 202–3
channel services, 201
cluster-wide event support, 592
commands, 204
components, 196–206
configuration files, 200–201
curses-style interface, 205
daemon, 198–99
defined, 195
device special files, 196
event loggers, 195–96
event path, 195
Event Viewer, 205–6
filter files, 203
filters, 323–24
graphical user interface (GUI), 205
logger, 199
messages, 27
priorities, 206–7
publishing company analogy, 196
remote access, 216
residential components, 198–99
root directory hierarchy, 197
security, 214–16
template files, 205
using, 217–29
/usr directory hierarchy, 197
/var directory hierarchy, 198
Events, 322–23
authorization rights, 215
on cluster, 322–23

Cluster Application Availability (CAA) subsystem, 725–26
cluster_event attribute, 320
Cluster File System (CFS), 357
Cluster Logical Storage Manager (CLSM), 402
clusterwide, 320–21
default attribute values for, 210
Device Request Dispatcher (DRD), 432
examples of, 196
filter files, 212–14
filters, 210, 321, 322–24
getting, from specific channels, 220
information, finding, 227–29
information, formatting, 222–23
keywords, 211–12
NetRAIN, 240
NIFF, 233
parsing, 803–4
priorities, 206
registration determination, 217–18
retrieving, 219
retrieving, from members, 321
sending, 221–22
sending, from scripts, 222
sorting, 226–27
on standalone system, 322
templates, 207–10
"timestamp" formatting, 220
waiting for, 218–19
evf command, 323–24, 726
-d switch, 224, 225
-v switch, 224, 225
evm.auth file, 200, 214–16
event_rights, 214–15
service_rights, 215–16
evmchannel.conf file, 200
evmchmgr, 199
evmd, 198–99
evmd daemon.conf file, 200
evmget command, 802–3
-A switch, 220, 227
-C switch, 220
-E switch, 212, 227–28, 321
-t switch, 222
evmlogger, 199
evmlogger.conf file, 200
evmpost command, 222
    -a switch, 221
    -u switch, 221
evmreload command
    -c switch, 201
    -d switch, 201
    -l switch, 201
    -n switch, 201, 225
evmshow command
    -D switch, 227, 228
    -d switch, 227, 228, 803
    -f switch, 225, 321
    -T switch, 220, 222
    -x switch, 227
evmsort command, 217
    -A switch, 226, 321
    -s switch, 226, 321
    -t switch, 321
evmwatch command
    -a switch, 219
    -f switch, 321
    -i switch, 217, 321
    for monitoring failover activity, 720
    -t switch, 222, 721
exports.aliases file, 484, 607–8
    defined, 608
    excerpt, 608
    reference page, 608

Failed quorum disk
    cluster information and, 541
    HWID, 659
    removing, 659
    replacing, 529, 658–63
    See also Quorum disk
Failover cluster
    defined, 2
    interconnect, 2
    SSI application cluster vs., 3
    See also Clusters
Failover mode, 66–68
    defined, 66

multi-bus, 66–67
transparent, 66, 68
Fiber Distributed Data Interface (FDDI), 98
Fibre Channel
    RAID controllers, 182
    storage, 36
    switches, 88, 182
File systems
    CFS supported, 331–32
    checking, 270–71
    creating, 127–28
    hierarchy, 154–55, 307–10
    hierarchy illustration, 309
    layout determination, 122–27
    mounting, 333–35, 580
    quick view, 246
    in standalone system, 307
    in two-member cluster, 308
    type selection, 121–27
    unmounting, 333, 396
    unmounting, troubleshooting, 810
    See also specific file systems
"File Value" information, 515
Filter files, 212–14
    directories, 212
    information on, 214
    syntax, 213

Filters, 210, 323–24
    available, finding, 223–25
    CAA, 726
    cluster, 323–24
    format, viewing, 225
    See also Event Manager (EVM); events
find(1) command, 155, 677
Firmware, 85–88
    Alpha, 85–87
    ECU, 87–88
    Fibre Channel Switch, 88
    HBA, 88
    HSZ/HSG RAID array controller, 88
    platform dependence, 85
    update, causes HOST_ID changes, 808–9
