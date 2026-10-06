# rsh

Executes commands on a remote computer
rsh [option] host [command line]

The rsh utility runs command line on host by starting a shell on the remote system. Without a command line calls rsh login, which logs you in on the remote computer.

rsh Is Not Secure // security
The rsh utility uses host-trust, which is not secure, to authorize your login. Alternatively, it sends your password over the network as cleartext, which is not a secure practice. Refer to "Trusted Hosts" on page 373. Use ssh (page 374) when it is available.

# Arguments

The name of the remote computer must be given as host. Any arguments following are part of command line, which is run on the remote system. You must quote special characters in command line if you do not want them expanded by the local shell prior to passing them to rsh.

# Options

+   - login-name If your login name on the remote computer is different from your local login name, you can use this option to give the remote login name.

# Notes

Your local login name and the name of your local computer should appear in the file .rhosts in the home directory for the account used on the remote computer. See “Examples” for login (page 1302) for a sample .rhosts file.

# Examples

In the first example, Alex uses rsh to obtain a listing of the files in his home directory on bravo: