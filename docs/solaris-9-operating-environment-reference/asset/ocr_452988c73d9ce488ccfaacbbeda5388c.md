# 1192

example% runat file.1 man runat
getcwd: Not a directory
example%

The following example spawns a tcsh shell in an attribute directory.

example% runat file.3 /usr/bin/tcsh
tcsh: Not a directory
tcsh: Trying to start from "home/user"
example%

A tcsh shell has been spawned with the current working directory set to the user's homie directory.

The following example spawns a zsh shell in an attribute directory.

example% runat file.3 /usr/bin/zsh
example%

While the command seems to have worked, zsh has actually just changed the working directory to / . You can see this with the /bin/pwd command.

example% /bin/pwd
/
example%

# Environment Variables

+   - SHELL Specify the command shell to be invoked by runat.

# Exit Status

+   - 125 The attribute directory of the file referenced by the file argument cannot be accessed.

+   - 126 The exec of the provided command argument failed.

Otherwise, the exit status returned is the exit status of the shell invoked to execute the provided command.

# Attributes

See attributes(5) for descriptions of the following attributes.

| Attribute Type | Attribute Value |
| Availability SUNWcs |
| CSI Enabled |
| Interface Stability Evolving |

# See Also

open(2), attributes(5), fsattr(5)