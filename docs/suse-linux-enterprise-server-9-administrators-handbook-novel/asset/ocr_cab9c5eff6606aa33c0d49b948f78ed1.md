server during software selection earlier, its setup will not be performed during this step.

# **FIGURE 1.12**  
**Configuring CA management and LDAP.**

![](bbox=[0.152, 0.221, 0.915, 0.573])

If you choose not to set up these services at this time, you can easily do so later using YaST. Any other services you have selected (such as MySQL) will need to be set up later using YaST or their specific configuration tools.

# Configuring User Information

The next step allows you to configure some user-related settings. First, you need to select how a user to your server will be authenticated: via an NIS server, an LDAP server, or using locally stored /etc/passwd information (see Figure 1.13). The default selection is LDAP. If you don't have an NIS or LDAP server on your network or if the users for this server are to be locally managed, select Local as the authentication method; this setting can be easily changed later using YaST.

If you choose NIS or LDAP as the user authentication method, a screen to set up the client is displayed next. Figure 1.14 shows the LDAP client configuration screen.