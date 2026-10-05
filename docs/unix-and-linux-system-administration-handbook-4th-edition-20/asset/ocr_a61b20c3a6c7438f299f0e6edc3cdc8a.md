# BIND dynamic updates

server crash. **named** recovers the in-memory state of the server by reading the original zone files and then replaying the changes from the journal.

You cannot hand-edit a dynamically updated zone without stopping the dynamic update stream. **rndc freeze** zone or **rndc freeze** class view will do the trick. These commands sync the journal file to the master zone file on disk and delete the journal. You can edit the zone file by hand. Unfortunately, the original formatting of the zone file will have been destroyed by **named's** monkey—the file will look like those maintained by **named** for servers.

Dynamic update attempts are refused if the zone is frozen. We use **rndc thaw** with the same arguments you froze to reload the zone file and reenable dynamic updates.

The **nsupdate** program supplied with BIND 9 comes a command-line interface for making dynamic updates. It runs in batch mode, taking commands from the keyboard or a file. A blank line or the **send** command signals the end of an update and sends the changes to the server. Two blank lines signify the end of an input. The command language includes a primitive if statement to express constructs such as "if hostname does not exist in DNS, add it." As predicates for an **nsupdate** action, you can require a name to exist or not exist, or require a resource record to exist or not exist.

For example, a simple nsupdate script adds a new host and also adds a nickname for an existing host if the nickname is not already in the zone. The angle bracket is produced by **nsupdate** and is not part of the command script.

```
$ nsupdate
> update add newest.cs.colorado.edu 86400 A 128.238.243.16
>
> prereq nxdomain. gypsy.cs.colorado.edu
> update add gypsy.cs.colorado.edu CNAME evi-laptop.cs.colorado.edu
```

Dynamic updates to DNS are scary. They potentially provide uncontrolled access to your important system data. Do not use IP addresses for access—they are too easily forged. TSIG authentication with a shared-secret key is better; it's available and easy to configure. BIND 9 supports:

```
$ nsupdate -y keyname:secretkeyfile
```

or

```
$ nsupdate -y keyname:secretkey
```

Since the password goes on the command line in the **-y** form, running with or **ps** at rest moment can see it. For this reason, the **-k** form is preferred. For more details on TSIG, see the section starting on page 645.

Dynamic updates to a zone are enabled in **named.conf** with an allow-update or update-policy clause. allow-update grants permission to update any records in accordance with IP- or key-based authentication. update-policy is a BIND 9