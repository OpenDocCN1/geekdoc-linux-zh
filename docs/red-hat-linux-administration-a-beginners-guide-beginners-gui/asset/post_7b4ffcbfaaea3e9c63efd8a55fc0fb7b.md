
# PART III
# Internet Services

## 10 The Domain Name Service (DNS) 291

- Critical Skill 10.1 Understanding the History Behind DNS: The /etc/hosts File 293
- Critical Skill 10.2 Exploring the Guts of DNS 295
  - Domains and Hosts 295
  - Ask the Expert 295
  - Subdomains 297
  - in-addr.arpa Domain 298
  - Types of Servers 300
- Critical Skill 10.3 Installing a DNS Server 301
- Critical Skill 10.4 Configuring Clients 304
  - Client-Side DNS (a.k.a. the Resolver) 304
- Critical Skill 10.5 Getting Ready for DNS Servers: The named.conf File 308
  - The Specifics 309
- Critical Skill 10.6 Configuring Servers 318
  - Updating the named.conf File for a Primary Zone 319
  - Updating the named.conf File for a Secondary Zone 320
  - Updating the named.conf File for a Caching Zone 321
  - DNS Records Types 322
- Critical Skill 10.7 Putting It All Together 327
  - A Complete Configuration 328
- Project 10-1 Configuring a Domain Using the GUI Tool 331
- Critical Skill 10.8 Using the DNS Toolbox 333
  - rndc 333
  - host 333
  - dig 334
  - whois 335
- Other References 336
- Module Summary 337
- Module 10 Mastery Check 338

## 11 Transferring Files with FTP 339

- Critical Skill 11.1 Defining the Mechanics of FTP 340
  - Client/Server Interactions 341
- Critical Skill 11.2 Setting Up vsftp 343
  - Read the READMEs 344
  - Fixing Your xinetd.conf File 344
- Critical Skill 11.3 Configuring vsftpd 346
  - General Configuration Options 348
  - Controlling Access to FTP 350
  - Ask the Expert 350
  - Configuring Host Access 352
- Critical Skill 11.4 Configuring a Virtual FTP Server 352
- Project 11-1 Setting Up Your FTP Server 354
- Ask the Expert 354
- Module Summary 355
- Module 11 Mastery Check 356

## 12 Setting Up Your Web Server Using Apache 357

- Critical Skill 12.1 Explaining the Mechanics of HTTP 358
  - Headers 359
  - Nonstandard Ports 360
  - Process Ownership and Security 360
- Critical Skill 12.2 Setting Up the Apache HTTP Server 362
  - Changes in Apache 2 362
  - Ask the Expert 362
  - Apache Modules 363
  - Starting Up and Shutting Down Apache 363
  - Testing Your Installation 364
- Critical Skill 12.3 Configuring Apache 365
- Project 12-1 Creating a Simple Root-Level Page 366
  - Apache Configuration Files 366
  - Common Configuration Changes 367
  - Ask the Expert 367
  - Configuring Virtual Domains 370
  - GUI Configuration 372
- Critical Skill 12.4 Performing Basic Troubleshooting with Apache 373

## 9 Securing an Individual Server 261

- Critical Skill 9.1 Keeping Your System up2date 262
  - Using the Red Hat Network 262
  - Manually Performing Security Updates 270
- Project 9-1 Getting Your System up2date 270
- Critical Skill 9.2 Understanding TCP/IP and Network Security 271
  - The Importance of Port Numbers 271
  - Port Dangers 272
- Critical Skill 9.3 Using Tracking Services 273
  - Using the netstat Command 274
  - Security Implications of netstat’s Output 275
  - Shutting Down Services 276
- Critical Skill 9.4 Monitoring Your System 278
  - Making the Best Use of syslog 278
  - Monitoring Bandwidth with MRTG 279
  - COPS 280
  - Tripwire 280
  - Nessus 280
  - SATAN 281
- Ask the Expert 281
- Project 9-2 Running a Nessus Scan 282
- Critical Skill 9.5 Employing a Checklist 284
- Critical Skill 9.6 Finding Helpful Resources Online 285
  - CERT 285
  - BugTraq 285
  - Linux Security 286
  - Security Focus 286
- Critical Skill 9.7 Being Aware of Security Miscellaneous 286
- Module Summary 287
- Module 9 Mastery Check 287

## Module 8

- Running LILO 227
  - Adding a New Kernel to Boot 228
- Project 8-1 Modifying Your GRUB Configuration 229
  - Step by Step 229
- Critical Skill 8.2 Knowing the Boot Process 230
  - Kernel Execution 230
  - The init Process 230
- Critical Skill 8.3 Learning about the init Service 232
  - The /etc/inittab File 232
  - The telinit Command 234
- Critical Skill 8.4 Configuring and Using the xinetd Process 234
  - The /etc/xinetd.conf File 235
- Critical Skill 8.5 Managing the syslogd Daemon 240
  - Invoking syslogd 240
  - The /etc/syslog.conf File 241
- Critical Skill 8.6 Using the cron Program 246
  - The crontab File 246
  - Using the cron GUI 247
  - The /etc/cron.* Directories 248
- Critical Skill 8.7 Enabling and Disabling Services 250
  - Graphical Service Managers 250
  - rc Scripts 252
- Project 8-2 Creating an rc Script 256
- Module Summary 258
- Module 8 Mastery Check 258
