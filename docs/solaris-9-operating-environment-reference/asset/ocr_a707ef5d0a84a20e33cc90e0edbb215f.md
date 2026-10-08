# nischmod

# Environment Variables

NIS_PATH If this variable is set and the NIS+ name is not fully qualified, search each specified directory until the object is found (see nisdefaults(1)).

# Exit Status

+   0 Success.
1 Failure.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | sunmisu |

# See Also

nis+(1), nischmod(1), nischown(1), nisdefaults(1), nisgrpadm(1), nis_objects(3NSL), attributes(5)

# nischmod — Change Access Rights on an NIS+ Object

# Synopsis

/usr/bin/nischmod [-AfLP] mode name...

# Description

Use the nischmod command to change the access rights (mode) of the NIS+ objects or entries specified by name to mode. Specify entries, using indexed names (see nismatch(1)). Only principals with modify access to an object can change its mode. mode has the following form.

rights [, rights]...

rights has the form:

[who] op permission [op permission]...

+   who is a combination of the following identities.
n Nobody's permissions.
o Owner's permissions.
g Group's permissions.
w World's permissions.
a All or owg.

If you omit who, the default is a.