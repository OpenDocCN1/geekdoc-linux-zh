# DESCRIPTION

pkcheck

is used to check whether a process, specified by either **—process** (see below) or **—system-bus-na**, is authorized for *action*. The **—detail** option can be used zero or more tis to pass details about *action*. If **—allow-user-interaction** is passed, **pkcheck** blocks while waiting for authentication.

The invocation **pkcheck —list-temp** will list all temporary authorizations for the current session and **pkcheck —revoke-temp** will revoke all temporary authorizations for the current session.

This command is a simple wrapper around the polkit D-Bus interface; see the D-Bus interface documentation for details.