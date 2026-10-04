# Using Windows 2000 Terminal Server Commands

There are many command line tools available from Microsoft that are useful in a Terminal Server session. The following lists are some of the security-focused command-line tools from Microsoft. Each tool has a variety of uses; you should try all of them to find out which work best for you. Many of these tools exist on Windows XP and Windows Server 2003:

+   - Qinsta.exe (query session) This is useful to figure out how their sessions are connected and in case you need to "look over your shoulders" for any reason using Shadow. This can also be used to monitor other Terminal Servers using the /server:server_ip directive. Query Session is shown in Figure 9.11.

# Figure 9.11 Example of the Query Session Command

![](bbox=[0.293, 0.388, 0.806, 0.598])

+   - Shadow This allows you to monitor and control other user sessions from your TS session. The ability to perform this action is determined by the setting with the highest precedence. The same applies regarding Require Users Permission setting that determines if they will or not be asked for permission to allow the shadowing. An interesting fact is that the Console cannot be shadowed on Windows 2000, but it can be shadowed and controlled on Windows XP and Windows Server 2003.

+   - Query termserver This command can only be used in a TS session. It is useful for attackers and administrators to find other Terminal Servers in the current domain.