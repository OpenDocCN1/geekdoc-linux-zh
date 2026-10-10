
## System Rescue
289

## The Fedora Rescue Disc
290

## Backing Up and Restoring the Master Boot Record
290

## Manually Restoring the Partition Table
290

## Booting the System from the Rescue Disc
291

## Using the Recovery Facility from the Installation Disc
292

## Reference
294

# 14 Networking
297

## Using Network Configuration Tools
297

## Using Graphical Configuration Tools
298

## Command-Line Network Interface Configuration
300

## Network Configuration Files
305

## Laying the Foundation: The localhost Interface
308

### Checking for the Availability of the Loopback Interface
308

### Configuring the Loopback Interface Manually
308

## Networking with TCP/IP
309

## Advanced Wireless Networking
310

### Support for Wireless Networking in Fedora
311

### TCP/IP Addressing
312

## Dynamic Host Configuration Protocol
314

### How DHCP Works
314

### DHCP Software Installation
315

### Using DHCP to Configure Network Hosts
316

### Other Uses for DHCP
319

## Using IP Masquerading in Fedora
319

### Ports
320

## Beyond the Network and Onto the Internet
321

### Common Configuration Information
321

### Configuring DSL Access
322

### Understanding Point-to-Point Protocol over Ethernet
323

### Configuring a PPoE Connection Manually
323

### Configuring Dialup Internet Access
325

### Configuring a Dialup Connection Manually
325

### Using the Fedora Internet Configuration Wizard
328

### Troubleshooting Connection Problems
331

## Reference
333

- General
- DHCP
- Wireless
- Books

# 15 Remote Access with SSH
335

## Setting Up a Telnet Server
336

## Setting Up an SSH Server
336

## The SSH Tools
337

- Using scp to Copy Individual Files Between Machines
338
- Using sftp to Copy Many Files Between Machines
339
- Using ssh-keygen to Enable Key-Based Logins
339

## Remote X
341

### XDMCP
341

### VNC
342

## Reference
343

# 16 Xen
345

## Why Virtualization Is a Smart Idea
345

## Virtualization versus Paravirtualization
346

## How Xen Works
347

## Installing Xen
347

## Setting Up Guest Operating Systems
348

## Runtime Configuration
349

## Reference
350

# Part IV: Fedora As a Server

# 17 Apache Web Server Management
353

## About the Apache Web Server
353

## Installing the Apache Server
355

- Installing Through Pirut
355
- Installing from the RPM
355
- Building the Source Yourself
357

## Starting and Stopping Apache
359

- Starting the Apache Server Manually
360
- Using /etc/rc.d/init.d/httpd
361
- Controlling Apache with Fedora's service Command
362
- Controlling Apache with Fedora's chkconfig Command
363

## Graphic Interface Configuration of Apache
364

- Configuring Virtual Host Properties
365
- Configuring the Server
366
- Configuring Apache for Peak Performance
366

## Runtime Server Configuration Settings
367

- Runtime Configuration Directives
367
- Editing httpd.conf
368
- Apache Multiprocessing Modules
370
- Using .htaccess Configuration Files
371

## File System Authentication and Access Control
372

- Restricting Access with allow and deny
373
- Authentication
374
- Final Words on Access Control
376

## Apache Modules
377

- mod_access
378
- mod_alias
378
- mod_asis
378
- mod_auth
379
- mod_auth_anon
379
- mod_auth_dbm
379
- mod_auth_digest
379
- mod_autoindex
379
- mod_cgi
379
- mod_dir and mod_env
380
- mod_expires
380
- mod_headers
380
- mod_info and mod_log_config
380
- mod_mime and mod_mime_magic
381
- mod_negotiation
381
- mod_proxy
381
- mod_rewrite
381
- mod_setenvif
381
- mod_speling
381
- mod_status
382
- mod_ssl
382
- mod_unique_id
382
- mod_userdir
382
- mod_vhost_alias
382

## Virtual Hosting
382

- Address-Based Virtual Hosts
383
- Name-Based Virtual Hosts
383

## Logging
384

## Reference
386

# 18 Administering Database Services
389

## A Brief Review of Database Basics
390

## How Relational Databases Work
391

## Understanding SQL Basics
393

## Choosing a Database: MySQL Versus PostgreSQL
397

- Speed
398
- Data Locking
398
- ACID Compliance in Transaction Processing to Protect Data Integrity
399
- SQL Subqueries
399
- Procedural Languages and Triggers
400

## Configuring MySQL
400

- Setting a Password for the MySQL Root User
401
- Creating a Database in MySQL
401
- Granting and Revoking Privileges in MySQL
402

## Configuring PostgreSQL
403

- Initializing the Data Directory in PostgreSQL
404
- Creating a Database in PostgreSQL
405
- Creating Database Users in PostgreSQL
406
- Deleting Database Users in PostgreSQL
407
- Granting and Revoking Privileges in PostgreSQL
407

## Database Clients
408

- SSH Access to a Database
409
- Local GUI Client Access to a Database
410
- Web Access to a Database
410
- The MySQL Command-Line Client
411
- The PostgreSQL Command-Line Client
413
- Graphical Clients
413

## Reference
414

# 19 File and Print
415

## Using the Network File System
415

- NFS Server Configuration
416
- NFS Client Configuration
418

## Putting Samba to Work
419

- Configuring Samba with system-config-samba
420
- Configuring Samba with SWAT
421
- Manually Configuring Samba with /etc/samba/smb.conf
425
- Testing Samba with the testparm Command
428
- Starting the smbd Daemon
429
- Mounting Samba Shares
430

## Network and Remote Printing with Fedora
431

- Enabling Network Printing on a LAN
431
- Session Message Block Printing
434
- Network-Attached Printer Configuration and Printing
435
- Using the Common UNIX Printing System GUI
437
- Console Print Control
440
- Using Basic Print Commands
441
- Managing Print Jobs
441
- Avoiding Printer Support Problems
443
- All-in-One (Print/Fax/Scan) Devices
443
- Using USB and Legacy Printers
443

## Reference
444

# 20 Remote File Serving with FTP
445

## Choosing an FTP Server
445

- Choosing an Authenticated or Anonymous Server
446
- Fedora FTP Server Packages
446
- Other FTP Servers
446

## Installing FTP Software
447

## The FTP User
448

## xinetd Configuration for wu-ftpd
450

- Configuring xinetd for the wu-ftp Server
450

## Starting the Very Secure FTP Server (vsftpd) Package
451

## Configuring the Very Secure FTP Server
452

- Controlling Anonymous Access
452
- Other vsftpd Server Configuration Files
453

## Configuring the wu-ftpd Server
455

### Using Commands in the ftpaccess File to Configure wu-ftpd
456

- Configure Access Control
456
- Configure User Information
459
- Configure System Logging
463
- Configure Permission Control
464
- Configure Commands Directed Toward the cdpath
466
- Structure of the shutdown File
467

### Configuring FTP Server File-Conversion Actions
468

- Strip Prefix
468
- Strip Postfix
468
- Add-On Prefix
468

# 21 Handling Electronic Mail
479

## How Email Is Sent and Received
479

- The Mail Transport Agent
480
- Choosing an MTA
482
- The Mail Delivery Agent
483
- The Mail User Agent
483

## Basic Sendmail Configuration and Operation
484

- Configuring Masquerading
485
- Using Smart Hosts
485
- Setting Message Delivery Intervals
486
- Building the sendmail.cf File
487
- Mail Relaying
487
- Forwarding Email with Aliases
488
- Rejecting Email from Specified Sites
488

## Introducing Postfix
489

- Making the Switch
490

## Using Fetchmail to Retrieve Mail
491

- Installing Fetchmail
491
- Configuring Fetchmail
491

## Choosing a Mail Delivery Agent
495

- Procmail
495
- Spamassassin
495
- Squirrelmail
496
- Virus Scanners
496
- Special Mail Delivery Agents
496

## Mail Daemons
497

## Alternatives to Microsoft Exchange Server
497

- Microsoft Exchange Server/Outlook Client
498
- CommuniGate Pro
498
- Oracle Collaboration Suite
498
- Open XChange
498

## Reference
499

- Web Resources
499
- Books
500

# 22 Setting Up a Proxy Server
501

## What Is a Proxy Server?
501

## Installing Squid
502

## Configuring Clients
502

## Access Control Lists
503

- Specifying Client IP Addresses
508

## Sample Configurations
509

## Reference
510
