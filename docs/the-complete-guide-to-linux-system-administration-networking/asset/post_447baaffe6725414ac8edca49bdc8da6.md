
client — A program or computer that is requesting information or service from another program or computer. See also server.

DHCP server — A computer that responds to requests from hosts on a network, providing them with an IP address and other network configuration information.

DNS server — A server that responds to requests from clients needing a domain name converted to (resolved to) an IP address.

Domain Name System (DNS) — The protocol used to convert domain names such as www.course.com into IP addresses such as 198.60.22.5.

Dynamic Host Configuration Protocol (DHCP) — The protocol used by clients and DHCP servers to provide an IP address and other network configuration data to computers on a network. See also DHCP server.

Ethernet — The most widely used type of networking hardware.

File Transfer Protocol (FTP) — Protocol designed for transferring files between a server and one or more client computers.

gateway — A computer attached to two or more networks such that computers on one network can reach other networks by sending data packets to the gateway computer.

Internet Protocol (IP) — Protocol used for all network communication in Linux. Used in conjunction with other protocols such as TCP.

IP address — A numeric address such as 198.60.45.5 that is uniquely associated with one computer on the network.

KGet — Graphical utility used to manage downloads of Web pages.

Lynx — A text-mode Web browser.

mirroring — Making a copy of a Web site, FTP site, or other collection of files, typically across a network connection.

network mask — A numeric code that resembles an IP address. Used to correctly route data packets between different networks.

OpenSSH — The free version of SSH utilities included in most Linux distributions.

public key encryption — A method of encrypting information using a public and private key, such that the private key is never sent over the network.

recursive — To repeat a procedure on successive sets of data or levels.

resolve — To convert a domain name into an IP address using the DNS protocol.

router — A computer connected to two or more networks that transfers data packets between those networks to reach their correct destination. Also called a gateway.

routing — The process of determining where to send data packets on a network based on factors such as the sender's IP address and network mask.

r-utilities (for "remote utilities") — Programs that allow a user to access remote hosts to run programs, transfer files, or perform other functions within a trusted network.

Secure Shell (SSH) — A protocol that provides network connectivity equivalent to an encrypted version of Telnet, plus additional support to allow encryption of other protocols.

server — A computer or program that provides data or a service to another program or computer. See also client.

ssh-agent — A part of the SSH suite that helps manage key pairs and authentication among multiple SSH-capable systems.

Telnet — A terminal emulation program that allows a user to log in to a remote computer as if sitting at that computer's keyboard.

Transmission Control Protocol (TCP) — A protocol that works with the Internet Protocol (IP) to provide stable connections for data transfer services such as the Web or FTP.

VT100 — The most widely supported dumb terminal standard.

## Review Questions

- 1. Name three types of remote connectivity supported by Linux and explain why one is preferred over the other two.

- 2. One advantage of Telnet is that:
  a. It provides a secure connection between any two Internet hosts.
  b. It provides a graphical interface for easier use.
  c. It can be used on many different platforms, including Linux and Windows.
  d. Other protocols such as FTP can use Telnet for greater stability.

- 3. Name three utilities that are part of the r-utilities suite and explain what each does.

- 4. The rcp program is able to copy files between:
  a. two remote systems
  b. the local system and a remote system that has .rhosts configured
  c. any recursive directories
  d. any two computers that are configured to use the r-utilities programs

- 5. Name the three types of authentication that SSH can use to connect to a remote system. Which is preferred as the most secure?

- 6. Which utility is used to prepare a set of keys needed to use public key encryption within SSH?
  a. sshd
  b. ssh-keygen
  c. ssh-agent
  d. slogin

- 9. If you have installed and configured r-utilities, then including a host and user name in your .rhosts file allows a person using the rcp command on another host to:
  a. Copy files to or from your home directory without entering a password.
  b. Also use login without entering a password.
  c. Execute the command if /etc/host.equiv also lists the remote host.
  d. View the output of the rlogind daemon.

- 10. SSH is commonly used in place of Telnet because:
  a. SSH provides a secure communications channel that is much more immune to security attacks.
  b. Telnet patents do not expire for several more years.
  c. SSH is strictly open source and Telnet is not.
  d. SSH protocols use a more robust encryption algorithm than that used by Telnet.

- 11. When using Telnet you might refer to VT100 because it is:
  a. a standard protocol designation used by Telnet
  b. the port used by default to connect to the Telnet server
  c. the most commonly used terminal emulation standard
  d. the speed at which terminal emulation connections are typically handled

- 12. Telnet is considered dangerous because:
  a. It provides access to networking stacks, to which only the root user should have access.
  b. It transmits data—including passwords—without encrypting them, so anyone on the network can see them by using special software.
  c. It causes an increased number of Ethernet collisions by ramping up network traffic with broadcast messages to the local network segment.
  d. It requires that a user provide a password to gain access to a remote system.

- 13. When using the wget command, you should include the http:// designation to download a Web page so that:
  a. The program knows which protocol to use when accessing the server.
  b. The program can convert Web links for local access.
  c. The entire Web site is downloaded.
  d. wget is not used in the background.

- 14. Suppose you want to mirror a Web site to your local computer in order to study the information it contains. You intend to update the mirror once each month to view changes in the Web pages on the site. You are concerned that the Web site administrator will block access if he realizes you are mirroring the entire site instead of using a regular browser to access it. In order to reduce the chance that the wget program creates suspicion, you can:
  a. Use the -k option with wget so that information from the remote Web site is converted for use locally.
  b. Use traceroute to see how packets are reaching the Web server.
  c. Use the --random-wait option with wget.
  d. Use the -m option with wget so that mirroring is enabled.

- 15. The rsync program is best suited for:
  a. synchronizing collections of files such as software development files
  b. mirroring FTP sites
  c. mirroring Web sites
  d. downloading large collections of e-mails

- 16. On a publicly available anonymous FTP server, the first level subdirectory that you should go to when locating files to download is virtually always:
  a. /anonymous
  b. /ftp
  c. /bin
  d. /pub

- 17. A graphical FTP client can be more convenient than a text-mode FTP client such as ncftp because:
  a. The graphical program lets you perform standard file operations on a remote server when you are logged in to the FTP server using a regular user account.
  b. The graphical program lets you see lists of files locally and remotely and drag and drop multiple files between systems.
  c. ncftp doesn't support features such as tab completion of file names.
  d. The graphical programs are always installed by default and text-mode programs might not be available on some systems.

- 18. The ncftp package includes a utility that is similar in functionality to wget. This utility is called:
  a. ncftpget
  b. ncftppput
  c. mget
  d. kget
