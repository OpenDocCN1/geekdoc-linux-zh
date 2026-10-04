# Attacking and Defending Microsoft Terminal Services • Chapter 9

I have read articles about using Stunnel (www.stunnel.org) and IPSec tunnels to perform similar extraordinary measures, but I feel it is overkill for most situations. You should calculate your risk for a particular network, host, or data, decide what fits your needs.

# Remote Administration Mode Specific Defenses

If you are using the Terminal Server for remote administration, the biggest thing to worry about is limiting who has access to connect; do not give permissions to administrators that do not require access and be the ones that have strong passwords. The easiest way to do this is by creating a Global Terminal Server group and making them local administrators on the Terminal Server.

# Rename the Administrator (RID=500)

Rename the Administrator (RID=500) and create a new administrator with a strong password and no privileges. Watch your logs to see if this user attempts to log on. If you see failed logins, investigate further. Don't forget to remove the description, otherwise an attacker can easily figure out that you renamed the account.

# Remote Administration Specific Group Policy Settings

The settings shown in Table 9.1 are what I consider the most relevant for securing your Terminal Server.

**Table 9.1** Remote Administration–Specific Group Policy Settings

| Setting | Recommended Value | Justification |
|---|---|---|
| Do not allow administrators to customize permissions | Enabled | If you have problems with Administrators changing your security settings, applying this to your TS organizational unit. If you apply it locally, another administrator may just change the value |
| Sets rules for remote control of Terminal user sessions | Enabled | If enabled, this will override the user settings as well as the Terminal Services Configuration (TSC) tool settings. This is useful if you have Continued |