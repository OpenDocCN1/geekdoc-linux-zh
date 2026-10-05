
- 4.3.3 Look and feel. ................................................................................ 79
- 4.3.4 User lockdown. ................................................................................... 83
- 4.3.5 Application choices ............................................................................... 83
- 4.3.6 File systems and partitions ................................................................ 83
- 4.4 Migrating applications ............................................................................ 84
- 4.4.1 Moving back to client/server computing ................................................. 84
- 4.4.2 Logical segmentation - Thin, slim, or fat ................................................. 85
- 4.5 Client administration planning ................................................................................ 86
- 4.5.1 Operating system and vendor distribution updates ................................. 87
- 4.5.2 Application updates ....................................................................... 88
- 4.5.3 Remote administration ................................................................... 88
- 4.5.4 Rollout of additional or replacement clients ...................................... 89
- 4.5.5 Backup of clients ........................................................................ 90
- 4.5.6 Virus mitigation ............................................................................................ 90
- 4.5.7 Examples of administration of enterprise distributions ................... 91
- 4.6 Desktop notebook considerations ................................................................ 94
- 4.6.1 Hardware considerations ................................................................. 95
- 4.6.2 Peripheral extensions ....................................................................... 96
- 4.6.3 Connectivity options ........................................................................ 97
- 4.6.4 Offline mode ............................................................................ 98
- 4.7 Unmigratable applications ........................................................................ 99
- 4.7.1 What makes an application unmigratable ...................................... 99
- 4.7.2 Terminal Server, Citrix Metaframe, or NoMachine NX solutions ............... 100
- 4.7.3 Ericrom Powertem Metaframe, WebConnect for Workplace solution .. 101
- 4.7.4 VMware solutions ......................................................................... 101
- 4.7.5 Dual boot solution ............................................................................ 102
- 4.7.6 What to do if all else fails ....................................................... 102
- 4.8 Deploying the new client ................................................................ 103
- 4.8.1 Deployment method ....................................................................... 103
- 4.8.2 Update deployed clients ................................................................ 104
- 4.8.3 Personalization of deployed clients ................................................... 105
- 4.9 Post-migration troubleshooting and technical support ................... 106
- 4.9.1 What to expect ............................................................................ 106
- 4.9.2 How to handle the unexpected ................................................ 107
- 4.9.3 When to contact vendor enterprise support ............................... 107

## Chapter 5. Linux architecture and technical differences. ............ 109
- 5.1 What is Linux. .......................................................................................... 110
- 5.1.1 Distributions ................................................................................... 110
- 5.1.2 Standards ....................................................................................... 111
- 5.2 Technical differences ....................................................................... 112
- 5.2.1 Kernel booting process ................................................................ 114
- 5.2.2 Communication, files, and services .......................................... 115
- 5.2.3 Multi-user ................................................................................. 117
- 5.2.4 Graphical and text-based environments ...................................... 118
- 5.2.5 System runlevels ....................................................................... 122
- 5.2.6 Drives, partitions, and file systems ........................................ 123
- 5.2.7 Virtual memory ....................................................................... 124
- 5.2.8 File links ............................................................................ 125
- 5.2.9 Replaceable kernel ................................................................... 125
- 5.2.10 Device drivers and hardware support ................................ 126
- 5.2.11 Font support ......................................................... 126
- 5.2.12 64 bit and multi-core support ....................................... 127

# Part 3. Performing the pilot migration ....................................... 129

## Chapter 6. Migration best practices ................................... 131
- 6.1 The transitional desktop ............................................ 132
- 6.2 Choose an installation methodology ................................. 132
- 6.2.1 Wipe and Reload ................................................ 132
- 6.2.2 Dual boot ........................................................ 132
- 6.2.3 Hardware refresh ........................................ 133
- 6.2.4 Hardware round-robin ................................ 133
- 6.3 Centralize data locations ................................ 133
- 6.3.1 Central file server ................................ 133
- 6.3.2 Central mail server ................................ 134
- 6.4 Break down migration into manageable groups .... 135
- 6.5 Minimize impact of down time .......................... 136
- 6.6 Get user feedback ....................................... 136
- 6.7 Automate the migration ................................ 136
- 6.8 Use a systems management tool ................ 136
- 6.9 Do not migrate until you are ready ........ 137
- 6.10 Do not migrate, upgrade. ................... 138

## Chapter 7. Client deployment models ................ 139
- 7.1 Restricting the desktop ................... 140
- 7.1.1 KDE Kiosk framework ................... 140
- 7.1.2 GNOME lockdown options ............... 151
- 7.2 Remoting tools ................................ 154
- 7.2.1 Remote access ........................ 154
- 7.2.2 Thin client ............................ 155
- 7.2.3 Application forwarding ............... 155
- 7.2.4 Multi-station lighting ............ 155
- 7.3 Rich client ................................... 156
- 7.3.1 Eclipse and the Eclipse Rich Client Platform .. 157
- 7.3.2 IBM Workplace Client Technology ... 158
- 7.3.3 IBM Workplace Managed Client .. 158
- 7.4 Stateless client ................................................................................ 160
- 7.4.1 Red Hat's Stateless Linux project ................................................. 161
- 7.4.2 Custom implementation of stateless client ....................................... 162
- 7.5 Multi-section client architecture ................................................. 162
- 7.5.1 Multi-section computing and Useful Desktop Multiplier ............... 163
- 7.5.2 What is multi-section computing .................................................... 164
- 7.5.3 Approaches to desktop consolidation and deployment .......................... 166
- 7.5.4 Where and when to deploy multi-section ................................. 168
- 7.5.5 Advantages of multi-section Linux ............................... 170

## Chapter 8. Client migration scenario ................................. 173
- 8.1 Client migration ................................................................. 174
- 8.1.1 Assess the client usage ................................................ 174
- 8.2 Migration plan details ................................................... 175
- 8.2.1 Client approach ....................................................... 175
- 8.2.2 Graphical environment ................................................. 175
- 8.2.3 Hardware ................................................................................ 175
- 8.2.4 Application continuity ....................................... 176
- 8.2.5 Windows networking ................................................. 177
- 8.3 Performing the migration ................................................. 178
- 8.3.1 Basic installation tasks ................................................ 178
- 8.3.2 Integrating existing network services ........................ 179
- 8.3.3 Application configuration and installation ................ 184
- 8.3.4 Screen captures: Client migrated to Linux ................. 189

## Chapter 9. Integration how-tos. .......................................... 195
- 9.1 How to join a Windows domain ........................................ 196
- 9.1.1 Joining an NT 4 domain ....................................... 196
- 9.1.2 Joining an Active Directory domain ................... 197
- 9.2 Using winbind to make domain users known locally ............ 199
- 9.2.1 Common implementation of winbind ................ 199
- 9.2.2 Alternate implementations of winbind ............ 202
- 9.3 How to use LDAP to connect to Active Directory ......... 204
- 9.4 Pluggable Authentication Modules and the domain ........ 207
- 9.4.1 How to authenticate users using winbind and PAM .. 208
- 9.4.2 How to authenticate users using LDAP and PAM .... 209
- 9.4.3 PAM and home directories ............................................ 212
- 9.5 How to mount a share on the Linux client ............... 214
- 9.5.1 Mounting a share using smbfs ................................. 214
- 9.5.2 Mounting a share using CIFS ................................. 215
- 9.5.3 Use of smclient ................................ 215

Linux Client Migration Cookbook, Version 2
