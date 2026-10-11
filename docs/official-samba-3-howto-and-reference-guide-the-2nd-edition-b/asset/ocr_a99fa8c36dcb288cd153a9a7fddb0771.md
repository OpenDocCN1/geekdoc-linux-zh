# RAP ADMIN *command*

Execute the specified *command* on the remote server. Only works with OS/2 servers.

> **NOTE**
> 
> ![note icon](image) Currently NOT implemented.

# RAP SERVICE

**RAP SERVICE START** *NAME* [*arguments*...] Start the specified service on the remote server. Not implemented yet.

> **NOTE**
> 
> ![note icon](image) Currently NOT implemented.

**RAP SERVICE STOP** Stop the specified service on the remote server.

> **NOTE**
> 
> ![note icon](image) Currently NOT implemented.

**RAP PASSWORD** *USER OLDPASS NEWPASS*

Change password of *USER* from *OLDPASS* to *NEWPASS*.

# LOOKUP

**LOOKUP HOST** *HOSTNAME [TYPE]* Lookup the IP address of the given host with the specified type (netbios suffix). The type defaults to 0x20 (workstation).