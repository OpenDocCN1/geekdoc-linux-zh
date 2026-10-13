
# Immediate Solutions

If you are replacing an original WINS installation, ensure that the current lease database is backed up before using the software.

# Creating A WINS Server

The creation of a WINS server on a Samba server is as simple as adding `wins support = yes` to the `smb.conf` file. If you already have a Microsoft NT Server performing this duty on your network, do not add a WINS server to your network, as a Windows NT Server would expect to adopt this function. In addition, the Microsoft WINS server is able to replicate its database with another WINS server, say, in a different building in a company. Samba does not support this ability and may be used only in a single configuration. The WINS database for a Samba server is contained in the `WINS.DAT` file, which is an ASCII text in `<samba_home>/var/locks/`. An example of this is shown in Listing 10.26.

### Listing 10.26 Entries in WINS.DAT

```
VERSION 1.0.418

"SAMABOOK#00" 930028 255.255.255.255

"SAMABOOK#01" 930028 255.255.255.255

"LINUXDS1#00" 930028 192.168.1.1

"LINUXDS1#03" 930028 192.168.1.1

"LINUXDS1#20" 930028 192.168.1.1
```
