
## More Information
712

## Setting Up an LDAP Server
713

### Prerequisites
713

### Note
713

### Step-by-Step Setup
713

## Other Tools for Working with LDAP
720

### Evolution Mail
720

### Kopano
722

## Chapter Summary
723

## Exercises
724

## Advanced Exercises
724

# CHAPTER 22: NFS: SHARING FILESYSTEMS
727

## Introduction
728

## More Information
730

## Setting Up an NFS Client
730

### Prerequisites
730

### JumpStart I: Mounting a Remote Directory Hierarchy
730

### mount: Mounts a Directory Hierarchy
732

### Improving Performance
734

### /etc/fstab: Mounts Directory Hierarchies Automatically
735

## Setting Up an NFS Server
736

### Prerequisites
736

### Notes
736

### JumpStart II: Configuring an NFS Server Using system-config-nfs
737

### Exporting a Directory Hierarchy
738

### exports: Maintains the List of Exported Directory Hierarchies
742

### Testing the Server Setup
743

### autofs: Automatically Mounts Directory Hierarchies
744

## Chapter Summary
746

## Exercises
746

## Advanced Exercises
747

# CHAPTER 23: SAMBA: INTEGRATING LINUX AND WINDOWS
749

## Introduction
750

## About Samba
751

### Prerequisites
751

### More Information
751

### Notes
751

## Samba Users, User Maps, and Passwords
752

## JumpStart: Configuring a Samba Server Using system-config-samba
753

## swat: Configures a Samba Server
755

## Manually Configuring a Samba Server
759

## Parameters in the smbd.conf File
760

## The [homes] Share: Sharing Users' Home Directories
765

## Accessing Linux Shares from Windows
765

### Browsing Shares
765

### Mapping a Share
766

## Accessing Windows Shares from Linux
766

### smbtree: Displays Windows Shares
766

### smbclient: Connects to Windows Shares
767

### Browsing Windows Networks
767

### Mounting Windows Shares
767

## Troubleshooting
768

## Chapter Summary
770

## Exercises
771

## Advanced Exercises
771

# CHAPTER 24: DNS/BIND: TRACKING DOMAIN NAMES AND ADDRESSES
773

## Introduction to DNS
774

### Nodes, Domains, and Subdomains
774

### Zones
776

### Queries
777

### Servers
778

### Resource Records
779

### DNS Query and Response
782

### Reverse Name Resolution
783

## About DNS
785

### How DNS Works
785

### Prerequisites
785

### More Information
786

### Notes
786

### JumpStart I: Setting Up a DNS Cache
787

### JumpStart II: Setting Up a Domain Using system-config-bind
789

#### Notes
789

#### Using the BIND Configuration GUI Window
790

### Setting Up a Domain Server
791

#### Adding Resource Records
792

### Setting Up BIND
793

#### named.conf: The named Configuration File
794

#### Zone Files
796

#### A DNS Cache
797

#### DNS Glue Records
802

#### TSIGs: Transaction Signatures
803

#### Running BIND in a chroot Jail
804

## Troubleshooting
805

### A Full-Functioned Nameserver
807

### A Slave Server
810

### A Split Horizon Server
811

## Chapter Summary
816

## Exercises
816

## Advanced Exercises
817

# CHAPTER 25: iptables: SETTING UP A FIREWALL
819

## How iptables Works
820

## About iptables
822

### More Information
822

### Prerequisites
823

### Notes
823

### JumpStart: Building a Firewall Using system-config-firewall
824

## Anatomy of an iptables Command
825

### Building a Set of Rules
826

### Commands
827

### Packet Match Criteria
828

### Display Criteria
828

### Match Extensions
829

### Targets
831

### Copying Rules to and from the Kernel
832

## system-config-firewall: Generates a Set of Rules
833

## Sharing an Internet Connection Using NAT
835

### Connecting Several Clients to a Single Internet Connection
836

### Connecting Several Servers to a Single Internet Connection
838

## Chapter Summary
839

## Exercises
839

## Advanced Exercises
839

# CHAPTER 26: APACHE (httpd): SETTING UP A WEB SERVER
841

## Introduction
842

## About Apache
842

### Prerequisites
843

### More Information
843

### Notes
844

### JumpStart I: Getting Apache Up and Running
844

### Modifying the httpd.conf Configuration File
845

### Testing Apache
845

### Putting Your Content in Place
846

### JumpStart II: Setting Up Apache Using system-config-httpd
846

# CONTENTS

## Filesystem Layout
848

## Configuration Directives
850

### Directives I: Directives You May Want to Modify as You Get Started
850

### Contexts and Containers
854

### Directives II: Advanced Directives
858

## The Fedora/RHEL httpd.conf File
870

### Section 1: Global Environment
871

### Section 2: Main Server Configuration
872

### Section 3: Virtual Hosts
873

### Redirects
873

### Multiviews
874

### Server-Generated Directory Listings (Indexing)
874

### Virtual Hosts
874

## Troubleshooting
875

## Modules
876

### Module List
876

### mod_cgi and CGI Scripts
877

### mod_ssl
877

### Authentication Modules and .htaccess
880

### Scripting Modules
881

### webalizer: Analyzes Web Traffic
881

### MRTG: Monitors Traffic Loads
882

### Error Codes
882

## Chapter Summary
883

## Exercises
884

## Advanced Exercises
884

# PART VI: PROGRAMMING TOOLS
885

# CHAPTER 27: PROGRAMMING THE BOURNE AGAIN SHELL
887

## Control Structures
888

### if...then
888

### if...then...else
892

### if...then...elif
895

### for...in
901

### for
902

### while
904

### until
908

### break and continue
910

### case
911

### select
917

### Here Document
919

## File Descriptors
921

## Parameters and Variables
924

### Array Variables
924

### Locality of Variables
926

### Special Parameters
928

### Positional Parameters
930

### Expanding Null and Unset Variables
935

## Builtin Commands
936

### type: Displays Information About a Command
937

### read: Accepts User Input
937

### exec: Executes a Command
940

### trap: Catches a Signal
943

### kill: Aborts a Process
946

### getopts: Parses Options
946

### A Partial List of Builtins
949

## Expressions
950

### Arithmetic Evaluation
950

### Logical Evaluation (Conditional Expressions)
951

### String Pattern Matching
952

### Operators
953

## Shell Programs
958

### A Recursive Shell Script
959

### The quiz Shell Script
962

## Chapter Summary
968

## Exercises
970

## Advanced Exercises
972

# CHAPTER 28: THE PERL SCRIPTING LANGUAGE
975

## Introduction to Perl
976

### More Information
976

### Help
977

#### perldoc
977

#### Terminology
979

### Running a Perl Program
980

### Syntax
981

### Variables
983

#### Scalar Variables
985

#### Array Variables
987

#### Hash Variables
990

### Control Structures
991

#### if/unless
991

#### if...else
993

#### if...elsif...else
994

#### foreach/for
995

#### last and next
996

#### while/until
998

### Working with Files
1000

### Sort
1003

### Subroutines
1005

### Regular Expressions
1007

#### Syntax and the =\ Operator
1008

### CPAN Modules
1013

### Examples
1015

## Chapter Summary
1019

## Exercises
1019

## Advanced Exercises
1020

# PART VII: APPENDIXES
1021

# APPENDIX A: REGULAR EXPRESSIONS
1023

## Characters
1024

## Delimiters
1024

## Simple Strings
1024

## Special Characters
1024

### Periods
1025

### Brackets
1025

### Asterisks
1026

### Carets and Dollar Signs
1026

### Quoting Special Characters
1027

## Rules
1027

### Longest Match Possible
1027

### Empty Regular Expressions
1028

## Bracketing Expressions
1028

## The Replacement String
1028

### Ampersand
1029

### Quoted Digit
1029

## Extended Regular Expressions
1029

## Appendix Summary
1031

# APPENDIX B: HELP
1033

## Solving a Problem
1034

## Finding Linux-Related Information
1035

### Documentation
1035

### Useful Linux Sites
1036

### Linux Newsgroups
1037

### Mailing Lists
1037

### Words
1038

### Software
1038

### Office Suites and Word Processors
1040

## Specifying a Terminal
1040

# APPENDIX C: SECURITY
1043

## Encryption
1044

### Public Key Encryptions
1045

### Symmetric Key Encryptions
1046

### Encryptions Implementation
1047

### GnuPG/PGP
1048

## File Security
1049

## Email Security
1049

### MTA (Mail Transfer Agents)
1049

### MUA (Mail User Agents)
1050

## Network Security
1050

### Network Security Solutions
1051

### Network Security Guidelines
1051

## Host Security
1053

### Login Security
1054

### Remote Access Security
1055

### Viruses and Worms
1056

### Physical Security
1056

## Security Resources
1058

## Appendix Summary
1061

# APPENDIX D: THE FREE SOFTWARE DEFINITION
1063

# GLOSSARY
1067

# INDEX
1117
