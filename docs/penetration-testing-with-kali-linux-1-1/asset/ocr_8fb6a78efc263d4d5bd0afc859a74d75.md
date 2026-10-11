![](bbox=[0.12, 0.035, 0.27, 0.085])

```
High Integrity:	0
Process Name:	powershell
Process ID:	2976
Language:	 powershell
Language Version: 5
...
```

*Listing 831 - Executing the sysinfo command*

Note that the command does not return immediately. This delay is caused by the *DefaultDelay* parameter, which is currently set to the default value of five seconds.

The **help** command (Listing 832) shows all available commands, such as **upload**, **download**, and **screenshot**, which are self-explanatory. In addition, we can use **shell** to execute a command and **spawn** to create an additional agent on the same host.

```
(Empire: S2Y5XWIL) > help

Agent Commands
===============
agents          Jump to the agents menu.
back            Go back a menu.
bypassuac       Runs BypassUAC, spawning a new high-integrity agent for a listener.
clear           Clear out agent tasking.
creds           Display/return credentials from the database.
download        Task an agent to download a file.
exit            Task agent to exit.
help            Displays the help menu or syntax for particular commands.
info            Display information about this agent
injectshellcode Inject listener shellcode into a remote process. Ex. injectshellcode
jobs            Return jobs or kill a running job.
kill            Task an agent to kill a particular process name or ID.
killdate        Get or set an agent's killdate (01/01/2016).
list            Lists all active agents (or listeners).
listeners       Jump to the listeners menu.
lostlimit       Task an agent to change the limit on lost agent detection
main            Go back to the main menu.
mimikatz       Runs Invoke-Mimikatz on the client.
psinject        Inject a launcher into a remote process. Ex. psinject <listener> <pid>
pth             Executes PTH for a CredID through Mimikatz.
rename          Rename the agent.
resource        Read and execute a list of Empire commands from a file.
revertoself     Uses credentials/tokens to revert token privileges.
sc              Takes a screenshot, default is PNG. Giving a ratio means using JPEG.
scriptcmd       Execute a function in the currently imported PowerShell script.
scriptimport    Imports a PowerShell script and keeps it in memory in the agent.
searchmodule    Search Empire module names/descriptions.
shell           Task an agent to use a shell command.
sleep           Task an agent to 'sleep interval [jitter]'
spawn           Spawns a new Empire agent for the given listener name. Ex. spawn <listener>
stal_token      Uses credentials/tokens to impersonate a token for a given process ID
sysinfo         Task an agent to get system information.
updateprofile   Update an agent connection profile.
upload          Task an agent to upload a file.
usemodule       Use an Empire PowerShell module.
workinghours    Get or set an agent's working hours (9:00-17:00).
```