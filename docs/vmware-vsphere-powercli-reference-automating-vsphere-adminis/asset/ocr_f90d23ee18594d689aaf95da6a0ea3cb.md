# INTERACT WITH THE GUEST

3. Creating a listener to accept requests on any IP address
4. Enabling- firewall exception for WS-Management traffic
(for http only).

Do you want to continue?

[Y] Yes [A] Yes to All [N] No [L] No All [S] Suspend
[?] Help (default is "Y"): y

WinRM already is set up to receive requests on this machine.
WinRM has been updated for remote management.
Created a WinRM listener on HTTP:// to accept WS-Man requests
to any IP on this machine.
WinRM firewall exception enabled.

# POWERSHELL REMOTING IN A DOMAIN ENVIRONMENT

When you use Windows 7, Windows 2008 R2, or a newer OS, PowerShell remoting is preinstalled. When dealing with these systems in a domain environment, you will find it much easier to control PowerShell Remoting through Group Policies. Learn more about enabling Group Policies here:

> www.jonathanmed.net/2010/03/enabling-powershell-2-0-0-remoting-in-an-enterprise.html

When the environment configured to receive PowerShell sessions, it's time
to put this fantastic technology to use. Remember that the user performing remote
script execution must be a member of the Administrators group on the remote
computer to be able to run commands.

There are two varieties of PowerShell Remoting: temporary sessions and persistent
sessions. Temporary sessions are sessions that are opened to run a command and
immediately closed when command is finished. This kind of session is useful
created when the -ComputerName parameter is specified in a cmdlet. For example, the
Invoke-Command cmdlet will create a temporary session and retrieve WMI information-from the remote guest:

```
Invoke-Command -ComputerName VM001 -ScriptBlock {
    Get-WmiObject Win32_CDROMDrive} | Format-List
```

Caption : NECMWar VMware SATA CD000