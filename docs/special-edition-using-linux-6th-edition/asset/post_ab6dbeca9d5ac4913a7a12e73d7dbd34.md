
- Account Setup 230
  - Key Configuration File 231
  - Passwords 232
  - Adding Users 234
  - Deleting or Disabling Users 236
- Groups 237
  - Creating a Group 237
  - Adding User Accounts to a Group 238
  - Removing User Accounts from a Group 238
  - Other Utilities 238
- Permissions 239
  - Changing Permissions 240
  - SUID/SGID and the Sticky Bit 243
  - Changing User or Group Ownership 244
  - Other Permissions 244
- Troubleshooting 245

## 12 Boot Loaders 247

- What Is LILO? 248
- Boot Stages 249
- How Does LILO Work? 251
  - Disk Organization 251
  - LILO Locations 253
  - Booting Basics 253
- Basic Configuration 255
- How to Install LILO 258
  - Installing LILO 258
  - Uninstalling LILO 259
- Dual Booting 259
- Parameters 261
- Debugging LILO 262
  - Map Installer 262
  - Boot Loader Messages 262
- Other Boot Loader Options 263
- GRUB 263
  - Using GRUB 264
  - /boot/grub 265
- Author Recommendations 267
- Troubleshooting 267

## 13 System Initialization 269

- About Initialization 270
- init: Where It All Begins 270
- inittab Specifics 273
  - Hands-On init 274
  - init Obscurities 274
  - The inittab File from Top to Bottom 275
- The rc Scripts 278
  - The Startup Scripts 281
- Emergencies 282
- Troubleshooting 284

## 14 Customizing Your Shell Environment 287

- Beyond the Login Prompt 288
- What Is a Shell? 289
- Types of Shells 290
  - The Bourne Shell 290
  - The C Shell 291
- Interactive Shell Use 291
- Default Shell Environment 292
  - Variables 292
  - Aliases and Functions 297
- Customizing Your Environment 299
- Shell Programming (Scripts) 301
  - Solving the Script Command Dilemma 301
  - Addressing the Script Environment Quandary 301
- Redirection 302
- Debugging 303
- Case Study: Scripting Suggestions 303

## 15 Understanding PAM 305

- Encryption and Authentication 306
- Using PAM 307
  - Reading the /etc/pam.d Files 307
  - Understanding the Modules 309
  - Stacking Modules 312
  - Modifying Your PAM Configuration 312
- Troubleshooting 313

## 16 Software Package Management 315

- Introduction to Package Management 316
  - What Is Package Management? 316
  - What Is a Package? 317
  - Where to Find Packages 322
  - Working with rpm 322
- Installing New Software 324
  - Finding the Package You Want to Install 324
  - Deciding Which Utility to Use 325
  - Security Concerns 325
  - Steps Performed During an Installation 326
  - The Actual Install 326
- Removing a Package 327
  - Dealing with a Dependency Problem 327
  - Other Types of Removal Problems 328
- Upgrading a Package 329
  - How Are Configuration Files Dealt With? 329
- Verifying Packages 330
  - Verifying Package Signatures 330
- Troubleshooting 331

## 17 Building/Rebuilding a Package 333

- Working with TAR Files 334
  - Installation Steps 334
  - Common Installation Aids 335
- Library Compatibility 336
  - How Shared Libraries Are Versioned 336
  - Using ldd to Discover Required Shared Libraries 337
- Advanced RPM Package Querying 339
  - Extracting the Contents of an rpm (rpm2cpio) 339
  - Finding Out Which RPM Package Owns a File 339
  - Customizing the Format of RPM Package Queries 339
  - Analyzing Disk Space Used by Packages 341
- Building from Source RPMs 341
  - Why Would You Want to Rebuild an RPM Package? 342
  - Steps in the Build Process 343
  - Directories Involved in the Build Process 343
  - Locating and Installing Source RPMs 344
  - Rebuilding the Package 344
  - The spec File 345
  - Building a Package 349
  - Packaging Miscellany 351
- Project: Modifying a Package 352

## 18 Building a Custom Kernel 355

- The Linux Kernel 356
- Building a New Kernel 356
  - Obtaining the Kernel Source (Step 1) 357
  - Preparing the Source Tree (Step 2) 357
  - Configuring the Source (Step 3) 358
  - Building the Source and Installing the Modules (Step 4) 363
- Moving the Kernel (Step 5) 365
- Configuring and Running LILO (Step 6) 365
- Verifying Module Support (Step 7) 367
- Rebooting the System (Step 8) 367
- Patching a Kernel 367
- Troubleshooting 368

## 19 Kernel Modules 371

- The Linux Kernel, Modules, and Drivers 372
- Module Versions 376
- Module Management 377
  - Manual Loading 378
  - Automatic Loading 379
- Modules Available Outside the Kernel Sources 382
  - Upgrading pcmcia-cs 383
- Troubleshooting 387

## 20 Building a VPN (FreeS/WAN) 389

- Getting Started 390
- Building the FreeS/WAN Kernel 390
- VPN Planning 391
- VPN Configuration 392
  - ipsec.conf 393
- Troubleshooting 397

## 21 System Auditing and System Logging 399

- syslog 400
  - syslogd 400
  - syslog.conf 401
- klogd 404
- Tripwire 404
- Troubleshooting 405

## IV Networking with Linux

### 22 Networking 409

- IP 410
  - IP Addressing 410
  - IP Networks and CIDR 411
  - VLSM 412
- Ports 414
- TCP 415
- UDP 416
- ICMP 416
- Network Startup Under OpenLinux 417
- Network Startup Under Debian 418
- Network Startup Under Red Hat 418
- ifconfig 419
- route 420
- Checking Your Network 421
  - ping 421
  - traceroute 422
  - netstat 422
  - fuser 425
  - Name Resolution 426
- Troubleshooting 427

### 23 Using DHCP 429

- Background 430
- ARP 430
- BOOTP 431
- DHCP 432
- Configuring DHCPD 433
- Global Parameters 434
- Subnet Statement 434
- Shared Network Statement 435
- Group Statement 436
- Configuring DHCP for BOOTP 437
- DNS and DHCP 437
- Configuring DHCP Clients 438
- DHCP Messages and Overview of the DHCP Process 439
- New DHCP Clients 439
- Continuing Leases 440
- Troubleshooting 441

### 24 Connecting to an ISP 443

- ISP Connections 444
- Dial-Up Connections with PPP 445
  - Getting Started with PPP 445
  - PPP Setup Steps 446
- Using ksaferppp 454
  - ksaferppp Setup 454
- Setting Up Automatic Demand Dialing 456
- Distribution-Specific Information 458
- Troubleshooting 458

### 25 Email Clients and Servers 459

- Email—What Is It? 460
- How Does Email Work? 460
- User Agents 461
  - Character-Based Email Clients 462
  - Netscape Messenger 462
  - KMail 464
- Mail Transport Agent Configuration 465
  - sendmail Configuration Files 466
  - Aliases 470
- Notes on Debian Systems 472
- Notes on Red Hat Systems 472
- Delivery Agents 472
  - A POP Server 473
  - An IMAP Server 473
  - Enabling POP and IMAP Services 473
  - fetchmail 473
  - mbox 474
- Encryption and Pretty Good Privacy (PGP) 474
  - Setting Up GPG for Use 475
  - Using GPG 479
- Troubleshooting 482

### 26 DNS and BIND 485

- About DNS 486
- What Is BIND? 487
  - About Domains 487
  - Root Name Servers 488
  - Types of DNS Servers 488
- BIND Files 489
  - Caldera OpenLinux 489
  - Debian 490
  - Red Hat 490
  - ndc: Name Server Daemon Control 490
  - Configuration Files and DNS Terms 490
- Name Server Tools 496
  - nslookup 496
  - dig 498
  - dnsquery 501
  - host 502
  - whois 502
- Troubleshooting 504

### 27 Sharing Files with NFS 505

- Why Share? 506
