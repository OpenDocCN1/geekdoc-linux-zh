
# CONTENTS

- Delegating Authority . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 474
- Add Authority for subdomain.domain.com on sylvia . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 475
- Test the subdomain.domain.com Local Resolution . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 476
- Delegate from mainerv to sylvia for the Subdomain . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 477
- Test the subdomain.domain.com Delegation . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 477

- Adding a Slave DNS Server . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 478
- Adding Slave Zones to mydesk . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 479
- Adding Second Nameservers to mainerv . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 480

- Troubleshooting DNS . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 481
- Using Scripting to Stress-Test Your DNS Setup . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 481
- Debugging with Dumps and Logs . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 482
- Checking Your DNS Configuration with dnswhack . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 483

- DNS Resources . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 484
- Automatically Configuring Clients with DHCP . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 485
- Configuring a DHCP Server . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 485
- Configuring a Linux-Based DHCP Client . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 488
- Configuring a Windows-Based DHCP Client . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 489
- Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 490

# 15 NIS: Network Information Service 491

- Understanding NIS . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 492
- NIS Domains . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 492
- The Different Servers . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 493
- Installing the Software . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 493
- Configuring a Master NIS Server . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 494
- Starting a Daemon on Boot . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 498
- Configuring a NIS Client . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 499
- Configuring a NIS Client with 11newcoff . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 499
- Configuring a NIS Client Manually . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 500
- Testing the Client . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 502
- Configuring a NIS Secondary Server . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 503
- Using NISnims in Your /etc/passwd File . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 505
- Using Netgroups . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 505
- Some Troubleshooting Tips . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 507
- Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 507

# 16 NFS: Network Filesystem 509

- Installing NFS . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 511
- Starting and Stopping the NFS Daemons . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 512
- Status of NFS . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 512
- Configuring NFS Servers and Clients . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 512
- Setting Up the /etc/exports File . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 513
- Using mount to Mount an Exported Filesystem . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 515
- Unmounting a Filesystem ........................................516
- Configuring the /etc/fstab File to Mount Filesystems Automatically ................................517
- Exporting Filesystems with linuxconf ...........................519
- Complete Sample Configuration Files ....................521
- Summary ............................522

# **17 Samba 523**

- Installing Samba ........................................525
- Getting a Simple Samba Setup Running .........525
  - Testing with a Linux Client ...........................527
  - Testing with a Windows Client ........................528
- Configuring Samba ....................................532
  - The [global] Section ................................533
  - The [homes] Section ..................................534
  - The [printers] Section .................................536
- Configuring a Samba File Server with linuxconf 539
- Sharing Files and Print Services ................540
- Optimizing Samba Performance ............................541
- Testing Your Configuration .............................543
  - Testing with smbstatus .............................544
- Running the Samba Server ..............................545
- Accessing Shares ................................545
  - Using smbclient on a Linux Client .....................545
  - Mounting Shares on a Linux Client ...........................548
- Common smb.conf Options .............................549
- Special Conventions .....................................549
  - read only= Versus writeable= Versus writable= ............550
  - write ok= (S) .............................550
  - valid users= (S) ......................................550
  - invalid users= (S) ................................550
  - read list= (S) .....................................551
  - write list= (S) .....................................551
  - path= (S) ........................................551
  - create mask= and create mode= (S) ......................552
  - browseable= (S) ...................................552
  - printable= (S) .......................................553
  - hosts allow= Versus hosts deny= Versus allow hosts=
  - Versus deny hosts= (S) ............................553
  - public= and guest ok= (G) .....................553
  - comment= (S) and server string= (G) ...................554
  - domain logons= (G) ..............................554
  - encrypt passwords= and smb passwd file= (G) ....554
  - config file= (G) ................................554
