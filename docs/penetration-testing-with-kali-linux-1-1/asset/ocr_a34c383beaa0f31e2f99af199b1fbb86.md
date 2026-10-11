```
tcp   LISTEN    0  128  :::22           :::*
tcp   LISTEN    0    2  :::13355      :::*
tcp   LISTEN    0    2  :::3389       :::*
```

*Listing 529 - Listing all active network connections on Linux*

The output lists the various listening ports and active sessions, including our own active SSH connection.

# 18.1.1.6 Enumerating Firewall Status and Rules

Generally speaking, a firewall’s state, profile, and rules are only of interest during the remote exploitation phase of an assessment. However, this information can be useful during privilege escalation. For example, if a network service is not remotely accessible because it is blocked by the firewall, it is generally accessible locally via the loopback interface. If we can interact with these services locally, we may be able to exploit them to escalate our privileges on the local system.

In addition, we can gather information about inbound and outbound port filtering during this phase to facilitate port forwarding and tunneling when it’s time to pivot to an internal network.

On Windows, we can inspect the current firewall profile using the **netsh**$^{462}$ command.

```
C:\\Users\\student>netsh advfirewall show currentprofile

Public Profile Settings:

-------------------------------------------------

**State**    **ON**

Firewall Policy        BlockInbound,AllowOutbound
LocalFirewallRules     N/A (GPO-store only)
LocalConSecRules       N/A (GPO-store only)
InboundUserNotification    Enable
RemoteManagement       Disable
UnicastResponseToMulticast Enable

Logging:
LogAllowedConnections    Disable
LogDroppedConnections    Disable
FileName %systemroot%\system32\LogFiles\Firewall\pfwfirewall.log
MaxFileSize 4096

Ok.
```

*Listing 530 - Listing the current profile for the firewall on Windows*

In this case, the current firewall profile is active so let’s have a closer look at the firewall rules. We can list firewall rules with the **netsh** command using the following syntax:

```
C:\\Users\\student>netsh advfirewall firewall show rule name=all

Rule Name:        @{Microsoft.Windows.Photos_2018.18022.15810.1000_x86__8wekyb3d8bbwe}
-------------------------------------------------
**Enabled:**   **Yes**
**Direction:** **In**
```

$^{462}$(Microsoft, 2019), https://docs.microsoft.com/en-us/windows-server/networking/technologies/netsh/netsh-contexts