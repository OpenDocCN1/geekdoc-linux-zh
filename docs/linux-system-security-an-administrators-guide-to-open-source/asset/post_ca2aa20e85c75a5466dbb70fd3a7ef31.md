
# 目录

## For Further Reading
Mailing List for tiger
sendmail Resources

## Chapter 14 Tripwire
- Tripwire Overview
- Obtaining and Installing Tripwire
  - Tripwire Version 1.2
- The Tripwire Configuration File
  - Extending the Configuration File
- Effectively Building the Tripwire Configuration File
  - Example Configuration File for Red Hat Linux
- The *tripwire* Command
- Tripwire Initialize Mode
  - Effective Tripwire Initialization
  - Storing the Database
- Routine Tripwire Runs—Compare Mode
  - A Note on Performance
- Tripwire Update Mode
- Summary
- For Further Reading
  - On-Line Documentation
  - Web Site

## Chapter 15 The Cryptographic and Transparent Cryptographic Filesystems
- Overview of the Cryptographic File System
- CFS Flow of Events
- Obtaining and Installing CFS
- CFS Administrative Tasks
- Using CFS
  - Creating and Attaching CFS Directories
  - The CFS Commands and Daemon Detailed
  - Using CFS over NFS
- Vulnerabilities of CFS
- Overview of TCFS
- Obtaining and Installing TCFS
- The TCFS Client Side
- The TCFS Server Side
- Using TCFS
  - Configuring TCFS for Use with PAM
  - TCFS Administrative Tasks
  - Extended Attributes for TCFS
  - Setting up the Encrypted Directory
  - TCFS Groups
  - TCFS Key Management
- Vulnerabilities of TCFS
- CFS and TCFS Comparison
- Securely Deleting Files
- Alternatives to CFS and TCFS
- Summary
- For Further Reading
  - Papers
  - E-Mail Lists

## Chapter 16 Packet Filtering with `ipchains`
We Must Censor!
- Packet Filtering
- Configuring the Kernel for `ipchains`
- `ipchains` Overview
- Behavior of a Chain
- Malformed Packets
- Analysis of an Inbound Packet
- Analysis of an Outbound Packet
- The Loopback Interface
- Custom Chains
- Introduction to Using `ipchains`
- The `ipchains` Command
- Some Simple Examples
- Packet Fragments
- IP Masquerading
- Adding Custom Chains
- ICMP Rules in a Custom Chain
- Antispoofing Rules
- Rule Ordering Is Important!
- Saving and Restoring Rules
- Rule Writing and Logging Tips
- Changing Rules
- `ipchains` Start-up Scripts
- Building Your Firewall
  - Simple Internal Network
  - Simple Internal Network Using DHCP
  - `ipchains` Isn't Just for Firewalls!
  - One More Thing
- Supplementary Utilities
- Other Examples
  - Port Forwarding
  - The `fwconfig` GUI
  - Mason
  - The Network Mapper (`nmap`)
- Additional Firewall Software
- Virtual Private Networks and Encrypted Tunnels
- The Next Generation...
- Summary
- For Further Reading
  - *iptables* Documentation
  - Masquerading Documentation
  - ISP Connectivity-Related Resources
  - General Firewall References
  - DMZ Resources
  - ICMP-Related References
- A Special Acknowledgment

## Chapter 17 Log File Management

![](img/7933c44717ab0711177ea7153f959fc5_19_0.png)

- General Log File Management
- logrotate
  - Obtaining and Installing logrotate
  - Configuring logrotate
  - Pulling It All Together
- swatch
  - Obtaining swatch
  - Installing swatch
  - Configuring and Running swatch
- logcheck
  - Obtaining logcheck
  - Major Components of logcheck
  - Configuring and Installing logcheck
  - logcheck Output
  - Troubleshooting logcheck
  - Summary

## Chapter 18 Implementing and Managing Security

![](img/7933c44717ab0711177ea7153f959fc5_19_1.png)

- So, Where Do I Start?...
- Hardening Linux
  - Selecting the Right Tools
  - Reducing the World
- What If My Systems Are Already in the Production Environment?...
- The Internal Network
- Critical Internal Servers
- Internal Maintenance
- Firewalls and the DMZ
  - External Maintenance
- Break-in Recovery
- Adding New Software
- Only through Knowledge

## Appendix A Keeping Up To Date

## Appendix B Tools Not Covered

## Glossary

## Index

# Figures

- Fig. 3.1 The TCP/IP Model
- Fig. 3.2 Difference between a Repeater and a Switch
- Fig. 3.3 Converting Cleartext into Ciphertext through Encryption
- Fig. 4.1 File Type and Permissions
- Fig. 5.1 Linux-PAM Overview
- Fig. 5.2 PAM-Controlled Password Change
- Fig. 6.1 S/Key OTP System
- Fig. 8.1 Flow of Log Messages
- Fig. 10.1 TCP_Wrappers Intercepts and Filters Requests
- Fig. 11.1 RSA Host-Based Authentication
- Fig. 11.2 Rhosts and RSA Authentication
- Fig. 11.3 RSA Authentication
- Fig. 11.4 SSH Authentication Flowchart
- Fig. 11.5 Using SSH Local Forwarding
- Fig. 12.1 The Crack Directory Tree
- Fig. 12.2 General Flow of the Guessing Process in Crack
- Fig. 12.3 Flow of the Application of Rules to a Dictionary Word
- Fig. 13.1 The tiger Directory Tree
- Fig. 14.1 Functional Overview of Tripwire
- Fig. 15.1 CFS Flow of Events
- Fig. 16.1 ipchains Flow of Events
- Fig. 16.2 Linux IP Masquerading
- Fig. 16.3 Small Internal Network Example
- Fig. 16.4 Dual Connection Requirement for ftp

# Examples

- Example 3-1 Setting Secure Permissions and Attributes on /etc/lilo.conf
- Example 3-2 Sample /etc/lilo.conf File
- Example 3-3 Booting into Single-User Mode
- Example 3-4 Symbolic Links to /usr/sbin/lpd
- Example 3-5 The GPL
- Example 4-1 Truncated Sample /etc/passwd File
- Example 4-2 Truncated Sample /etc/shadow File
- Example 4-3 Password Aging Directives in /etc/login.defs
- Example 4-4 Remaining Directives in /etc/login.defs
- Example 4-5 Restricted Shell Program
- Example 4-6 The /etc/fstab File
- Example 4-7 A More Secure /etc/fstab
- Example 5-1 Contents of /etc/pam.d
- Example 5-2 PAM Configuration File Entry Fields
- Example 5-3 The /etc/pam.d/passwd Configuration File
- Example 5-4 The /etc/pwdb.conf File
- Example 5-5 Using mas and minlen in /etc/pam.d/passwd
- Example 5-6 Unsuccessful Password Change
- Example 5-7 Successful Password Change
- Example 5-8 Sample /etc/pam.d/login File
- Example 5-9 Attempted Login with the Presence of /etc/nologin
- Example 5-10 Partial Configuration File Using pam_time required
- Example 5-11 Login Attempt with Expired Password and Outside of Permitted Times 1
- Example 5-12 Partial Configuration File Using pam_time.so requisite
- Example 5-13 Login Attempt with Expired Password and Outside of Permitted Times 2
- Example 5-14 Sample /etc/security/time.conf File
- Example 5-15 Sample /etc/security/limits.conf File
- Example 5-16 The csh Configuration File with a pam_listfile Entry
- Example 5-17 Failed csh Attempt Due to pam_listfile
