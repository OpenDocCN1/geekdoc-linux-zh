# nisgrpdadm 959

-M Master server. Send the lookup to the master server of the named data. This option guarantees that the most up-to-date information is seen, at the possible expense that the master server may be busy. Note that the -Moption is only applicable with the -l option.

-r Remove the list of principals specified from group. The principal name should be fully qualified.

-s Work silently. Return results, using the exit status of the command. This status can be translated into a text string by the niserror(1) command.

-t Display the principals specified are members in group.

# Examples

# Administering Groups

The following example creates a group in the foo.com. domain. castle@nisgrpdadm -c my_buds.foo.com.

The following example removes the group from the current domain. castle@nisgrpdadm -d freds_group

# Administering Members

The following example shows how you would add two principals, bob and betty, to the groupmy_buds.foo.com... castle@nisgrpdadm -a my_buds.foo.com bob.bar.com. betty.foo.com.

The following example removes betty from freds_group. castle@nisgrpdadm -r freds_group betty.foo.com.

# Environment Variables

NIS_DEFAULTS Specify a default string that overrides the NIS+ standard defaults.

NIS_PATH If variable is set and the NIS+ name is not fully qualified, search each specified directory until the object is found (see nisdefaults(1)).

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNmisu |

# See Also

nis+(1), nischgrp(1), nismod(1), nisttl(1), nisdefaults(1), niserror(1), nis_groups(3NSL), attributes(5)