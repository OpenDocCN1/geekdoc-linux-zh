This line must not be set in the **smb.conf** file of the Samba server acting as the WINS server itself. If you set both the *wins support = yes* option and the *wins server = <name> option* then **nmbd** will fail to start.

There are two possible scenarios for setting up cross-subnet browsing. The first details setting up cross-subnet browsing on a network containing Windows 9x/Me, Samba, and Windows NT/2000 machines that are not configured as part of a Windows NT domain. The second details setting up cross-subnet browsing on networks that contain NT domains.

# ### 9.5.2 WINS Replication

Samba-3 permits WINS replication through the use of the **wrepld** utility. This tool is not currently in use because it is still in development and has not been worked on for a long time. As soon as this tool becomes moderately functional, we will prepare man pages and enhance this section of the documentation to provide usage and technical details.

# ### 9.5.3 Static WINS Entries

Adding static entries to your Samba WINS server is actually fairly easy. All you have to do is add a line to *wins.dat*, typically located in */usr/local/samba/var/locks* or */var/run/samba*.

Entries in *wins.dat* take the form of:

"NAME#TYPE" TTL ADDRESS+ FLAGS

where NAME is the NetBIOS name, TYPE is the NetBIOS type, TTL is the time-to-live as an absolute time in seconds, ADDRESS+ is one or more addresses corresponding to the registration, and FLAGS are the NetBIOS flags for the registration.

A typical dynamic entry looks like this:

"MADMAN#03" 1155298378 192.168.1.2 66R

To make a NetBIOS name static (permanent), simply set the *TTL* to 0, like this:

"MADMAN#03" 0 192.168.1.2 66R

The NetBIOS flags may be interpreted as additive hexadecimal values: 00 - Broadcast node registration, 20 - Peer node registration, 40 - Meta node registration, 60 - Hybrid node registration, 02 - Permanent name, 04 - Active name, 80 - Group name. The 'R' indicates this is a registration record. Thus 66R means: Hybrid node active and permanent NetBIOS name. These values may be found in the **nameserv.h** header file from the Samba source code repository. These are the values for the NB flags.