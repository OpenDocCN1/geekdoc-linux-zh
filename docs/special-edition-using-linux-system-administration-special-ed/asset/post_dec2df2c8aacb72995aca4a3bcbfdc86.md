
- Using Wildcard Mail Exchangers for Your Domain 341
- Other Mail Relaying Problems 341

### 17 Fax Servers 343

- What Are Fax Servers? 344
- Fax Software for Linux 344
- HylaFAX 345
  - Obtaining HylaFAX 345
  - Installing HylaFAX 346
  - Configuring HylaFAX Server 349
  - Testing HylaFAX 356
  - Automating Distribution of Received Faxes 359
  - HylaFAX Client Setup 360
  - Setting Up an Email-Fax Gateway 363
  - HylaFAX Transfer Logs 366
  - HylaFAX cron Jobs 367
  - Troubleshooting HylaFAX 367
  - An Example of a Client-Side Problem 368
  - An Example of a Server-Side Problem 368
  - Debugging Communication Problems 369
- Using Efax 371
  - Installing Efax 371
  - Configuring Efax 372
  - Sending Faxes with Efax 373
  - Receiving Faxes with Efax 374
  - Setting Up a Fax Print Server 375
- Extending Efax with Qfax 377
  - Installing Qfax 377
  - Sending Faxes by Email 382
  - Managing Qfax 383
- Troubleshooting Efax and Qfax 384

## IV Security and Stability 385

### 18 General Security Issues 387

- Security in a Networked World 388
  - Physical Security 389
  - Usage and Security Policies 389
  - System Security 392
  - Network Security 393
  - Internet Security 393
- Security Tools 393
- Keeping Systems Secure 395
  - Monitor Log Entries 395
  - Apply Software Updates 395
  - React to Security Breaches 396
  - Monitor Sources of Security Information 396

### 19 Linux and Firewalls 399

- Firewalls and the Internet 400
- Types of Firewalls 401
  - Packet-Filtering Firewalls 401
  - Proxy Server Firewalls 403
  - IP Masquerading Proxy Servers 403
- Firewalls and Network Architecture 404
- Setting Up a Linux Firewall 406
  - IP Packet Filtering and IP Masquerading
  - Using IPCHAINS 407
  - Putting It All Together 418
  - IP Port Forwarding 428
- Troubleshooting 429
  - ipchains -L Freezes 429
  - DNS Lookups Fail Part of the Time 429
  - IP Masquerading Does Not Work 430
  - 4096 Masqueraded TCP and UDP Connections Are Insufficient 430

### 20 Log Management and Analysis 431

- Logging Activity in Linux 432
- The syslog Daemon 433
  - Making Changes to the `syslog.conf` File 436
- Log Rotation 436
  - The logrotate Utility 437
- Case Study: Useful Scripts 441
  - Source Code for su-report 442
  - Source Code for failed-su 442

## V The Internet and the Intranet 445

### 21 Using Linux as an Intranet Server 447

- Understanding Intranets 448
  - Linux As a Web Server 448
  - Linux As a Database Server 451
  - Linux As a News Server 452
  - Linux As a Mail Server 452
- Hardware Requirements 453

### 22 DNS 455

- The Domain Name System 456
- DNS Name Resolution 457
  - Setting Up Name Servers 458
  - Resolving Names 468
  - DNS Maintenance 472
- Load Balancing with DNS 473
- Securing DNS 474
  - Restricting Zone Transfers to Designated Slave Servers Only 474
  - Restricting Zone Transfers from Secondary Servers 475
  - Restricting Queries to Your Name Server 475
- Useful Scripts 476
- Troubleshooting 476
  - Domain Names Missing the Trailing Dot 476
  - Forgetting to Increment the SOA Serial Number 477
  - Forgetting to Signal named After Making Changes to Zone Data 477
  - Forgetting Reverse DNS Records 478
  - Invalid Glue Record 478
  - Lack of Coordination Among DNS Administrators 478
  - Misconfigured `resolv.conf` File 478
  - Outdated `root.hints` File 478

### 23 Apache and the World Wide Web 481

- Linux As a Web Server Platform 482
- Apache’s Role as a Linux HTTP Server 482
- Configuring Apache 483
  - The `httpd.conf` File 483
  - The `srm.conf` File 492
  - The `access.conf` File 497
- Apache Modules 499
- Managing Apache 501
  - Starting the Server 501
  - Stopping the Server 502
  - Restarting the Server 502
  - Testing the Server’s Status and Configuration Files 502
- Virtual Hosting with Apache 502
  - Creating DNS Entries for Each Site 503
  - Creating a Directory Hierarchy for the Sites 504
  - Configuring Apache to Serve Each Site 504
  - Providing Backward Compatibility 505
- Monitoring Your Web Site Through the Logs 507
  - The Access Log File 507
  - The Error Log File 510
  - Managing Logs 511
- Basic Web Site Security 512
  - Set Your File and Directory Permissions Correctly 512
  - Consider Your Use of Server-Side Includes Carefully 513
  - Consider Allowing Users Access to CGI-BIN Scripts Carefully 513
  - Examine Your CGI-BIN Scripts 514
  - Do Not Allow Users to Override Global Settings 514
  - Deny Default Access 515
- Troubleshooting 515

### 24 Linux Database Servers 517

- Linux As a Database Server 518
- Creating a Linux Database Server 519
  - Determining Your Database Server's Hardware Requirements 519
  - Obtaining and Installing MySQL 520
  - Configuring and Testing MySQL 521
- Database Management 528
  - Starting and Stopping the Server 528
  - Connecting to the Server 528
  - Creating and Deleting Databases and Tables 529
  - Interacting with Databases Using SQL 533
  - Backing Up Your Databases 538
  - Managing Users and Permissions 539
- Troubleshooting 542
  - Receiving the MySQL server has gone away Error 542
  - Receiving the Host `<host name>` is blocked Error 542
  - Receiving the Too many connections Error 543
  - Receiving the Out of memory Error When Executing a SQL Command 543
  - Receiving the Access Denied Error 543

### 25 Dynamic, Data-Driven Web Sites 545

- Understanding Dynamic, Interactive Web Sites 546
  - CGI-BIN Programming 546
  - Server API Programming 548
- Software for Connecting Web Sites to Databases 549
  - PHP 549
  - Zope 549
  - Web+ 550
  - ColdFusion 550
- Installing PHP 551
  - PHP Installation Configuration Parameters 552
- An Overview of PHP Scripting 560
  - Creating a Simple Dynamic Web Site with PHP 562
- Troubleshooting 565
  - PHP Stops Working After Installing FrontPage Extensions for Apache 566
  - PHP Files Are Displayed As Source Code by Apache 566
  - PHP Fails to Compile Because of a Missing Library 566
  - PHP Fails to Connect to My Database Server 567

### 26 News Services 569

- A Brief History of Usenet 570
- News Group Hierarchies 570
- Hardware Requirements 571
- Installing INN 2.2.1 571
- General Overview of INN 572
  - Receiving Incoming News Feeds 573
  - Processing Outgoing News Feeds 574
  - Servicing News Readers and Facilitating the Reading and Posting of Articles 574
  - Expiring Articles 574
  - Logging All Activity 574
- Configuring INN 574
  - Selecting a Storage Method for News Articles 575
  - Editing `inn.conf` 576
  - Editing the `newsfeeds` File 576
  - Editing `incoming.conf` 579
  - Using the `cycbuff.conf` File for CNFS 580
  - Editing `storage.conf` for CNFS and `timehash` 580
  - Using the `overview.ctl` File with CNFS and `timehash` Storage 582
  - Controlling Client Access with the `nnrpd.access` File 582
  - Controlling Article Expiration with `expire.ctl` 583
  - Creating an Article Spool for CNFS Storage 584
  - Creating News History Database Files 584
  - Specifying Sites to Feed to with the `nntpsend.ctl` File 585
  - Controlling Daily Maintenance with the `news.daily` Script 586
  - Starting INN at Boot Time with `rc.news` 586
- Understanding INN Log Files 586
  - Other Log Files 587
- Administering INN 587
- Troubleshooting 588
  - When a Server Is Throttled 588
  - When the History File Is Too Large 589
  - When Multiple `innwatch` Processes Run 589
  - Editing the `active` File 589
  - Handling the `history.n.` Files 589
  - When the `active` File Is Corrupted or Deleted 590

### 27 FTP Servers 591

- Understanding FTP 592
- Washington University FTP Server—WU-FTPD 593
  - WU-FTPD Configuration Files 593
  - Building WU-FTPD from Source 594
  - Anonymous FTP Setup 596
  - Using the `ftpaccess` File 600
  - Using the `ftpconversions` File 604
  - Allowing Uploads into the Incoming Directory 605
  - Other WU-FTPD Utilities 608
  - The FTP Xferlog File 610
- The Professional FTP Daemon—ProFTPD 611
  - Installing a Precompiled Binary 612
  - Building from Source 613
  - Configuring ProFTPD 613
  - The `proftpd.conf` File 614
  - Virtual FTP Servers 616
- Useful Scripts 618
- Troubleshooting 621

## VI Appendices 623

### A Linux Command Reference 625

- AT 625
  - Name 625
  - Synopsis 625
  - Description 625
  - Options 626
  - Files 627
  - See Also 627
  - Bugs 627
  - Author 627
- CAT 627
  - Name 627
  - Synopsis 627
  - Description 628
  - Reporting Bugs 628
  - See Also 628
  - Copyright 628
