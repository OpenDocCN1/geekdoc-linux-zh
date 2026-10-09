
# CHAPTER 7: THE LINUX UTILITIES 215

## Basic Utilities 216

- *cat*: Joins and Displays Files 216
- *date*: Displays the System Time and Date 218
- *echo*: Displays Arguments 219
- *hostname*: Displays the System Name 219
- *less Is more*: Display a Text File One Screen at a Time 220
- *ls*: Displays Information About Files 221
- *rm*: Removes a File (Deletes a Link) 222

## Working with Files 224

- *cp*: Copies Files 224
- *cut*: Selects Characters or Fields from Input Lines 225
- *diff*: Displays the Differences Between Two Text Files 227
- *file*: Displays the Classification of a File 229
- *find*: Finds Files Based on Criteria 229
- *grep*: Searches for a Pattern in Files 232
- *head*: Displays the Beginning of a File 235
- *lpr*: Sends Files to Printers 235
- *mv*: Renames or Moves a File 237
- *sort*: Sorts and/or Merges Files 239
- *tail*: Displays the Last Part of a File 241
- *touch*: Changes File Modification and Access Times 243
- *wc*: Displays the Number of Lines, Words, and Bytes in Files 244

## Compressing and Archiving Files 245

- *xz, bzip2,* and *gzip*: Compress and Decompress Files 245
- *tar*: Stores or Extracts Files to/from an Archive File 249

## Displaying User and System Information 252

- *free*: Displays Memory Usage Information 253
- *uptime*: Displays System Load and Duration Information 253
- *w*: Lists Users on the System 254
- *who*: Lists Users on the System 254

## Miscellaneous Utilities 255

- *which* and *whereis*: Locate a Utility 255
- *locate*: Searches for a File 256
- *script*: Records a Shell Session 257
- *tr*: Replaces Specific Characters 258
- *unix2dos*: Converts Linux Files to Windows and Macintosh Format 260
- *xargs*: Converts Standard Input to Command Lines 260

## Editing Files 262

- Tutorial: Using *vim* to Create and Edit a File 262
- Tutorial: Using *nano* to Create and Edit a File 270

## Chapter Summary 273

## Exercises 275

## Advanced Exercises 276

# CHAPTER 8: NETWORKING AND THE INTERNET 279

## Introduction to Networking 280

## Types of Networks and How They Work 282

- Broadcast Networks 282
- Point-to-Point Networks 283
    - Switched Networks 283
    - LAN: Local Area Network 284
    - WAN: Wide Area Network 287
- Internetworking Through Gateways and Routers 287

## Network Protocols 290

- IPv4 292
- IPv6 293
- Host Address 296
- CIDR: Classless Inter-Domain Routing 300
- Hostnames 300

## Communicate over a Network 301

- Mailing List Servers 301

## Network Utilities 302

- Trusted Hosts 302
- OpenSSH Tools 303
    - telnet: Logs In on a Remote System 303
    - ftp: Transfers Files over a Network 305
    - ping: Tests a Network Connection 305
    - traceroute: Traces a Route over the Internet 306
    - host and dig: Query Internet Nameservers 307
    - whois: Looks Up Information About an Internet Site 308

## Distributed Computing 309

- The Client/Server Model 309
- DNS: Domain Name Service 310
- Ports 312
- NFS: Network Information Service 313
- NIS: Network Filesystem 313
- Network Services 313
- Common Daemons 314
- Proxy Servers 316
- RPC Network Services 317

## WWW: World Wide Web 319

- Browsers 320
- Search Engines 320
- URL: Uniform Resource Locator 320

## Chapter Summary 321

## Exercises 322

## Advanced Exercises 322

# PART III SYSTEM ADMINISTRATION 325

## CHAPTER 9: THE BOURNE AGAIN SHELL (bash) 327

- Background 328
- Startup Files 329
- Login Shells 330
- Interactive Nonlogin Shells 330
- Noninteractive Shells 331
- Setting Up Startup Files 331
- . (Dot) or source: Runs a Startup File in the Current Shell 332
- Commands That Are Symbols 333
- Redirecting Standard Error 333
- Writing and Executing a Shell Script 336
- chmod: Makes a File Executable 337
- #!/ Specifies a Shell 338
- # Begins a Comment 340
- Executing a Shell Script 340
- Control Operators: Separate and Group Commands 341
    - ; and NEWLINE Separate Commands 341
    - ! and & Separate Commands and Do Something Else 342
    - && and || Boolean Control Operators 343
    - () Groups Commands 344
    - \ Continues a Command 345
- Job Control 346
    - jobs: Lists Jobs 346
    - tg: Brings a Job to the Foreground 347
    - Suspending a Job 348
    - bg: Sends a Job to the Background 348
- Manipulating the Directory Stack 349
    - dirs: Displays the Stack 349
    - pushd: Pushes a Directory on the Stack 350
    - popd: Pops a Directory off the Stack 351
- Parameters and Variables 352
    - User-Created Variables 353
    - Variable Attributes 356
    - Keyword Variables 358
    - Special Characters 366
- Locale 368
    - LC_: Locale Variables 368
    - locale: Displays Locale Information 369
- Time 371

- Processes 373
    - Process Structure 373
    - Process Identification 374
    - Executing a Command 375
- History 376
    - Variables That Control History 377
    - Reexecuting and Editing Commands 378
    - The Readline Library 386
- Aliases 392
    - Single Versus Double Quotation Marks in Aliases 393
    - Examples of Aliases 394
- Functions 396
- Controlling **bash**: Features and Options 398
    - **bash** Command-Line Options 399
    - Shell Features 399
    - Processing the Command Line 403
    - History Expansion 404
    - Alias Substitution 404
    - Parsing and Scanning the Command Line 404
    - Command-Line Expansion 404
- Chapter Summary 414
- Exercises 415
- Advanced Exercises 417

## CHAPTER 10: SYSTEM ADMINISTRATION: CORE CONCEPTS 419

- Running Commands with root Privileges 422
    - The Special Powers of a Privileged User 422
    - Gaining **root** Privileges 423
    - Real UID Versus Effective UID 425
    - Using **su** to Gain **root** Privileges 425
    - Using **sudo** to Gain **root** Privileges 428
    - Locking the **root** Account (Removing the **root** Password) 438
- The **systemd** init Daemon 438
    - More Information 439
    - Service Units and Target Units 439
    - Runlevels 440
    - Wants and Requires 440
    - */etc/systemd/system* Hierarchy: Controls Services and the Persistent Runlevel 441
    - Custom Service Files 442
    - Determining Whether **systemd** Runs a Daemon Natively 443
    - Setting and Changing Runlevels 444
    - Configuring Daemons (Services) 445
- SysVinit (rc) Scripts: Start and Stop System Services 448
    - System Operation 448
    - Runlevels 449
    - Booting the System 450
        - Single-User Mode 450
        - Going to Graphical Multituser Mode 452
    - Logging In 452
    - Logging Out 453
    - Bringing the System Down 454
        - Crash 455
        - Rescue an Installed System 456
        - Avoiding a Trojan Horse 458
    - X Window System 459
- System Administration Tools 464
    - Textual Administration Utilities 464
    - Graphical Configuration Tools 470
- SELinux 472
- PAM 476
- Setting Up a Server 481
    - Standard Rules in Configuration Files 481
    - rpcinfo: Displays Information About rpcbind 483
    - Securing a Server 485
- DHCP: Configures Network Interfaces 491
    - How DHCP Works 491
    - DHCP Client 492
    - DHCP Server 492
- nsswitch.conf: Which Service to Look at First 495
    - Information 495
    - Methods 496
    - Search Order 496
    - Action Items 496
    - compat Method: ∗ in passwd, group, and shadow Files 497
- Getting Help 498
- Chapter Summary 498
- Exercises 499
- Advanced Exercises 500

## CHAPTER 11: FILES, DIRECTORIES, AND FILESYSTEMS 501

- Important Files and Directories 502
- File Types 514
    - Ordinary Files, Directories, Links, and Inodes 514
    - Device Special Files 515
- Filesystems 519
    - mount: Mounts a Filesystem 520
    - unmount: Unmounts a Filesystem 523
    - du: Displays Disk Usage Information 523
    - fstab: Keeps Track of Filesystems 524
    - fsck: Checks Filesystem Integrity 525
    - tune2fs: Changes Filesystem Parameters 526
- The XFS Filesystem 527
- Chapter Summary 529
- Exercises 530
- Advanced Exercises 530

## CHAPTER 12: FINDING, DOWNLOADING, AND INSTALLING SOFTWARE 531

- Introduction 532
- JumpStart: Installing and Removing Software Packages Using yum 534
- Finding the Package That Holds an Application or File You Need 536
- yum: Keeps the System Up-to-Date 538
    - Updating Packages 538
    - yum Commands 539
    - yum Package Groups 540
    - Downloading RPM Package Files with yumdownloader 540
    - yum.conf: Configures yum 541
    - yum Repositories 542
- BitTorrent 543
    - Prerequisites 544
    - transmission-cli: Downloading a BitTorrent File 544
- RPM: The RPM Package Manager 546
    - Querying Packages and Files 547
    - Installing, Upgrading, and Removing Packages 548
    - Installing a Linux Kernel Binary 549
- Installing Non-rpm Software 550
    - The /opt and /usr/local Directories 550
    - GNU Configure and Build System 550
- Keeping Software Up-to-Date 552
    - Bugs 552
    - Errata 553
- curl: Downloads Files Noninteractively 553
- Chapter Summary 553
- Exercises 554
- Advanced Exercises 554
