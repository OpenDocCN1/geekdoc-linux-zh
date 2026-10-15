
## PART II CONFIGURING LINUX NETWORKING 105

## 5 BASIC LINUX CONFIGURATION 107
- Installing Linux ................................................ 108
- Partitioning Your Hard Drives ................................... 109
- Modifying an Existing Partition Scheme ........................... 113
- Running the Red Hat Installer ................................... 114
- Packages to Select and Leave Behind ............................... 120
- Final Installation Configuration ................................. 122
- Testing the Installation ......................................... 123
- Configuration Files and Tools .................................... 124
- The /etc Directory and Its Contents ............................... 124
- Using Linuxconf .................................................. 125
- Using LILO to Boot Linux ......................................... 127
- Setting Up User Accounts .......................................... 131
- The Importance of User Accounts ................................... 131
- Using Linuxconf ................................................... 132
- Creating an Account with Text-Mode Tools .......................... 134
- Account Creation Tips ............................................. 135
- Summary ............................................................ 137

## 6 COMPILING A KERNEL FOR NETWORKING 139
- Understanding the Compile Process ................................ 140
- Just What Is Compilation? ......................................... 140
- Advantages and Disadvantages of Compiling Your Own Kernel ......... 140
- Linux Kernel Versions ............................................. 142
- Linux Kernel History .............................................. 142
- Obtaining a Kernel ................................................ 143
- Setting Kernel Compile Options .................................... 144
- Preliminary Options ............................................... 147
- Block Devices ..................................................... 147
- Networking Options ................................................ 148
- SCSI Support ...................................................... 149
- Network Device Support ............................................. 149
- Character Devices ................................................. 150
- Mice ................................................................ 151
- Filesystems ....................................................... 151
- Compiling and Installing a Kernel .................................. 153
- Compiling the Kernel ............................................... 154
- Preparing to Use the Compiled Kernel ............................... 155
- Rebooting Your System .............................................. 158
- Alternative Methods of Booting .................................... 160
- Summary ............................................................ 160

## 7 SETTING ETHERNET OPTIONS 161
- Obtaining the Necessary Information........................................163
- Network Driver Configuration................................................164
- Configuring a System with a Fixed Address...................................166
- Setting the Machine Name.....................................................166
- The /etc/hosts File..........................................................168
- Activating Interfaces........................................................169
- Routing Network Traffic......................................................171
- Preliminary Testing..........................................................172
- Setting the DNS Server........................................................173
- Using DHCP for Dynamic Configuration........................................179
- Using DHCP as a Client.......................................................179
- Configuring a DHCP Server....................................................181
- Using linuxconf to Configure Networking.....................................182
- Setting Basic Host Information...............................................182
- Name Server Specification....................................................182
- Additional Options...........................................................184
- Summary........................................................................184

## 8 USING PPP FOR DIALUP CONNECTIONS 185
- Obtaining a PPP Account......................................................186
- Configuring Your Serial Ports................................................188
- Setting Kernel Options.......................................................188
- Checking Your Device File....................................................190
- Using a Terminal Program to Test Your Modem................................191
- PPP Authentication...........................................................193
- Creating PPP Scripts.........................................................195
- Creating the ppp-on Script...................................................195
- Creating the ppp-on-dialer Script...........................................197
- Configuring for DNS..........................................................198
- Creating the ppp-off Script..................................................198
- Testing Your Link............................................................199
- Using a GUI PPP Dialer.......................................................199
- Setting Up Dial-on-Demand for Automatic Connections.......................203
- Necessary Kernel Options....................................................203
- Configuring Dial-on-Demand Services........................................204
- When to Use Dial-on-Demand..................................................205
- PPP Problem Solving..........................................................206
- General Problem-Solving Advice..............................................206
- Modem Connectivity Problems.................................................208
- Authentication Failure.......................................................209
- Postconnection Hangups and Logouts..........................................209
- Summary........................................................................211
