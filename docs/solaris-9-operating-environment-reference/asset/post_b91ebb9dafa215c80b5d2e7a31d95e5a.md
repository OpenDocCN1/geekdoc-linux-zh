
## nisrm

# Exit Status

```
0 Success.
1 Permission denied.
2 Invalid combination of options.
3 Unexpected failure. NIS+ passwd table unchanged.
4 NIS+ passwd table missing.
5 NIS+ was busy. Try again later.
6 Invalid argument to option.
7 Aging was disabled.
```

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUN+nisisu |

# See Also

keylogin(1), login(1), nis+(1), nistbladm(1), passwd(1), login(1), domainname(1M), getspnam(3C), getspnam(3C), nis_local_directory(3NSL), nswitch.conf(4), passwd(4), shadow(4), attributes(5)

# nisrm — Remove NIS+ Objects from the Namespace

# Synopsis

```
/usr/bin/nisrm [-if] name...
```

# Description

Use the nisrm command to remove NIS+ objects named name from the NIS+ namespace. This command fails if the NIS+ master server is not running.

> Note — This command does not remove directories (see nismirdir(1)), nor does it remove tables that are not empty (see nistbladm(1)).

# Options

- -f Attempt a forced removal, and if it fails for permission reasons, try an nischmod(1) operation and retry the removal. If the command fails, it fails silently.
- -i Like the system rm(1) command, interactively ask for confirmation before removing an object. If the name specified by name is not a fully qualified name, force this option on. This option prevents the removal of unexpected objects.

## nisrmdir

# Examples

The following example removes the objects foo, bar, and baz from the namespace.
castle% nismrm foo bar baz

# Environment Variables

# Exit Status

- 0 Success.
- 1 Failure.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNnis |

# See Also

nis+(1), nischmod(1), nisdefaults(1), nisrmdir(1), nistbladm(1), rm(1), attributes(5)

# nisrmdir — Remove NIS+ Directories

# Synopsis

```
/usr/bin/nisrmdir -if -s hostname dirname
```

# Description

Use the nisrmdir command to delete existing NIS+ subdirectories. You can remove a directory outright or simply remove replicas from serving a directory.
This command modifies the object that describes the directory dirname and then notifies each replica to remove the directory name dirname. If the notification of any of the affected replicas fails, the directory object is returned to its original state unless you specify the -f option.
This command fails if the NIS+ master server is not running.

> Note — Special per-server and per-directory access restrictions may be when this command updates the serving lists of the affected NIS+ servers.
For more information, see nisopaccess(1).

# Options

- -f
Force the command to succeed even though it may not be able to contact the affected replicas. Use this option when a replica is known to be down and is not able to respond to the removal notification. When the replica is finally rebooted, it reads the updated directory object, notes that it is no longer a replica for that directory, and stops responding to lookups on that directory. You can manually clean up the files that held the now removed directory by removing the appropriate files in the /var/nis directory (see nfiles(4) for more information).

- -i
Like the rm command, interactively ask for confirmation before removing a directory. If the name specified by dirname is not a fully qualified name, force this option on it. This option prevents the removal of unexpected directories.

- -s hostname
Remove the hostname as a replica for the directory named dirname. If this option is not present, remove all replicas and the master server for a directory and remove the directory from the namespace.

# Operands

- dirname
an existing NIS+ directory.

# Examples

The following example removes a directory bar under the foo.com. domain. castle@ nisrmdir bar.foo.com.

The following example removes a replica that is serving the bar.foo.com. directory. castle@ nisrmdir - replica.foo.com. bar.foo.com.

The following example forces the removal of the bar.foo.com. directory from the namespace. castle@ nisrmdir -f bar.foo.com.

# Environment Variables

- NIS_PATH
This variable is set and the NIS+ name is not fully qualified, search each specified directory until the object is found (see nisdefaults(1)).

# Exit Status

- 0
Success.
- 1
Failure.

## nistbladm

# Attributes

See attributes(s) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUMwnisu |

# See Also

nis+(1), nisdefaults(1), nisopaccess(1), nisrm(1), nisfiles(4), attributes(5)

# nistbladm — Administer NIS+ Tables

# Synopsis

```
/usr/bin/nistbladm -a|-A [-D defaults] colname=value... tablename
/usr/bin/nistbladm -a -A [-D defaults] indexname
/usr/bin/nistbladm -c [-D defaults] [-p path] [-s sep] type
classname=[flags] [access...] tablename
/usr/bin/nistbladm -d tablename
/usr/bin/nistbladm -e|E colname=value... indexname
/usr/bin/nistbladm -m colname=value... indexname
/usr/bin/nistbladm -r -R [colname=value...] tablename
/usr/bin/nistbladm -r -R indexname
/usr/bin/nistbladm -u [-p path] [-s sep] [-t type] [colname=access...]
tablename
```

# Description

Use the nistbladm command to administer NIS+ tables. It performs five operations:

- Creating tables.
- Deleting tables.
- Adding entries to tables.
- Modifying entries within tables.
- Removing entries from tables.

Although NIS+ does not place restrictions on the size of tables or entries, the size of data has an impact on the performance and the requirements of NIS+ server. NIS design is optimized to support 10,000 objects with a total size of 10 megabytes. If the requirements exceed the above, it is suggested that you create the domain hierarchy or store pointers to the data instead of storing the data itself.

When creating tables, you must specify a table type, and a list of column definitions.

## nistblad

typeis a string that is stored in the table and later used by the service to verify that entries being added are of the correct type. Column definitions use the following syntax.

```
colname=[flags] {access}
```

flags is a combination of:

- S Searches can be done on the column's values (see nismatch(1)).
- I Searches ignore case (makes sense only in combination with S).
- C Encrypt column values.
- B Binary data (does not make sense in combination with S). If not set, the column values are expected to be null-terminated ASCII strings.
- X XDR encode data (makes sense only in combination with B).

access is specified in the format defined by the nismod(1) command. When manipulating entries, this command takes two forms of entry name. The first uses a series of space-separated colname=value pairs that specify column values in the entry. The second is an NIS+ indexed name, indexname, of the following form.
[colname=value, ...], tablename

# Options

- -a Add entries to an NIS+ table. The difference between the lowercase and the uppercase A is in the treatment of preexisting entries. The entry's contents are specified by the column=value pairs on the command line. Note that you must specify values for all columns when adding entries to a table.

Normally, NIS+ reports an error if you try to add an entry to a table that would overwrite an entry that already exists. This feature prevents multiple parties from adding duplicate entries and having one of them get overwritten. The uppercase A specifies that the entry is to be added if it already exists. This option is analogous to a modify operation on the entry.

- -c Create a table named tableName in the namespace. The table that is created must have at least one column, and at least one column must be searchable.

- -d Destroy the table tableName. The table that is being destroyed must be empty. First delete the table's contents with the -R option.

- -D defaults When creating objects, specify a different set of defaults to be used during this operation. The defaults string is a series of tokens separated by colons. These tokens represent the default values to be used for the generic object properties. All of the legal tokens are described below.
