Under Path to Export enter the full path to the directory you want to export. There is a place to enter a comment; this is optional. You are asked for the Client name(s) to export to. There are four types of entries that you can use here. These were explained earlier, in the section “Setting Up the /etc/exports File.”

You are presented with options for the share. If you select May Write, the user on the client will be able to write to files in the exported directory providing that the file’s permissions allow them to do so. Root Privileges gives root on the client root privileges in the exported directory. This puts a lot of trust in root on the client machine. You can leave Request Access from Secure Port selected.

You may of course want to have different permissions for different clients. That is why there is more than one place to enter a client name and its permissions. By default there are two places for entering a client and its permissions. You can have as many as you wish—just click Add and another entry will be created.

Now save your changes and exit \texttt{linuxconf}. Make sure to accept changes whenever presented with the option.

# # Complete Sample Configuration Files

Listing 16.1 contains a complete /etc/exports file for a server.

```
LISTING 16.1  A Complete /etc/exports File

```
#
# /etc/exports for demon
#
# Share the home dirs:
/export/home
technics(rw) pioneor(rw) vestax(rw)
	tatus(rw) rane(rw)

#
# Share local software
#
/export/usr/local
technics(rw,no_root_squash)
	vestax(rw,no_root_squash)
	pionooer(rw,no_root_squash)
	atus(rw,no_root_squash)
	-rane(rw,no_root_squash)
```
```

Listing 16.2 contains a complete /etc/fstab file for a client.