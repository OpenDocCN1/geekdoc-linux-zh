
**Storage Management System (SMS)** — The NetWare backup service that includes several NetWare Loadable Modules along with software that enables the host server to back up data from one or more target servers.

**target servers** — Servers with data that has been backed up by the host server.

**trusted network** — A network with an IP address range that’s known to be safe or can be controlled and monitored by your organization.

**unknown network** — A network that’s not specified as a trusted or untrusted network in a firewall. Firewalls treat unknown networks as trusted networks.

**untrusted network** — An IP address range that might contain attackers or other malicious entities. Packets from networks listed as untrusted are inspected by the network firewall.

**virtual private network (VPN)** — A trusted network that sends packets over an untrusted network, such as the Internet.

**viruses** — Self-replicating programs that can be embedded in software to propagate between computers and can eventually be triggered to affect computer performance or destroy data.

**Web Services** — A set of hardware and software components that provide World Wide Web and FTP information services to clients on the Internet or company intranet.

## REVIEW QUESTIONS

1. Which of the following is an example of a Web Services component? (Choose all that apply.)
   - a. FTP Server
   - b. Apache Web Server
   - c. iFolder
   - d. NetStorage

2. Tomcat is an example of which of the following?
   - a. Web server
   - b. Java servlet
   - c. servlet engine
   - d. FTP server

3. Which of the following does NetWare 6.5 use to provide Net Services?
   - a. Enterprise Web Server
   - b. Apache Web Server
   - c. Tomcat
   - d. Web Manager

4. Which of the following provides customized Web pages to users based on their access rights and privileges?
   - a. Web servers
   - b. Novell Portal Services
   - c. iManager
   - d. Remote Manager

5. Java servlets require which of the following to run?
   - a. Enterprise Web Server
   - b. FTP Server
   - c. NetWare Web Manager
   - d. Tomcat

6. Which of the following is an example of a Java servlet?
   - a. Tomcat
   - b. Enterprise Web Server
   - c. Novell Portal Services
   - d. iFolder

7. The __________________ tab in the FTP Server Administration window is used to configure anonymous user access.

8. In public key cryptography, which of the following keys is digitally signed by a CA?
   - a. public
   - b. private
   - c. digital
   - d. certificate

9. In public key cryptography, which of the following keys is used to decrypt data packets?
   - a. public
   - b. private
   - c. digital
   - d. certificate

10. In public key cryptography, the CA is responsible for which of the following? (Choose all that apply.)
   - a. creating public and private keys
   - b. encrypting data
   - c. verifying that users are who they claim to be
   - d. signing and issuing public key certificates

11. Which of the following attacks involves sending large Echo packets?
   - a. ping of death
   - b. SYN packet flooding
   - c. teardrop
   - d. land

12. Which of the following attacks involves a failure to send ACK packets?
   - a. ping of death
   - b. SYN packet flooding
   - c. teardrop
   - d. land

13. Which of the following is a form of firewall packet filtering that uses port numbers and service types?
   - a. proxy filtering
   - b. circuit-level gateway
   - c. packet filtering
   - d. echo filtering

14. Which of the following is a form of firewall security that checks only packet source IP addresses?
   - a. proxy services
   - b. circuit-level gateway
   - c. packet filtering
   - d. echo filtering

15. Which of the following acts as an independent program that does not replicate but can infiltrate legitimate programs to alter or destroy data?
   - a. worm
   - b. polymorphic virus
   - c. stealth virus
   - d. Trojan program

16. Which of the following is not classified as a denial-of-service attack?
   - a. land attacks
   - b. oversized packets
   - c. Trojan program
   - d. SYN packet flooding

17. Which of the following is a firewall application that examines destination and source addresses to determine whether a packet is from a trusted network?
   - a. packet filtering
   - b. circuit-level gateway
   - c. proxy service
   - d. VPN

18. Which of the following firewall technologies is the best choice for Universal AeroSpace to control the type of information sent between the network and clients?
   - a. proxy service
   - b. circuit-level gateway
   - c. NAT
   - d. VPN

19. Eric is concerned about maintaining a secure channel when using the Internet to connect to servers at the AeroDyn facility. Which of the following technologies should he use?
   - a. NAT
   - b. circuit-level gateway
   - c. packet filtering
   - d. VPN

20. Which of the following firewall technologies can hide client IP addresses on a private network from the Internet?
   - a. packet filtering
   - b. circuit-level gateway
   - c. NAT
   - d. VPN

21. Which of the following is a basic component of public key cryptography? (Choose all that apply.)
   - a. VPN
   - b. CA
   - c. public and private keys
   - d. certificate signing

22. Which of the following is not a firewall technology?
   - a. packet filtering
   - b. NAT
   - c. VPN
   - d. virus scanning

## CASE PROJECTS

### Case Project 11-1: Identifying Net and Web Services

In Table 11-4, identify each type of server as a Web Services or Net Services component and supply a brief explanation of what makes it that type of service.

| **Service** | **Type of Service** | **Explanation** |
| :--- | :--- | :--- |
| IFolder | | |
| Apache Web Server | | |
| FTP Server | | |
| Web Manager | | |
| Novell Portal Services | | |

### Case Project 11-2: Developing a Security Plan for AeroDyn

The AeroDyn facility is planning to use FTP Server so that users can download files. In this project, you develop a plan to secure the AeroDyn facility from outside attacks. Your plan should include a diagram of the following network components and a brief description of what type of attacks you plan to prevent:

- □ Router
- □ Firewall
- □ AeroDyn internal private network

### Case Project 11-3: Developing a Virus Protection Plan

Luke McMann wants you to research the antivirus software listed in this chapter, and then make a recommendation that includes the vendor, product, and price for a 30-station network. Your recommendation should include two antivirus software packages and explain why you think this antivirus software would be a good choice for the AeroDyn network.

## Hands-On Projects

### Hands-on Project 11-1: Creating a Web Site

Eric wants you to create a demonstration Web site for the Engineering Department. He plans to use it at the next management meeting to show managers how to use the Web server to access other Web pages by supplying the Web site name after the Universal AeroSpace URL. The Web site should simply consist of a heading and a simple graphic in the IT\Web\Engineer directory. Follow these steps:

1. If you’re using a shared classroom server, ask your instructor for the path to your virtual document directory. If you’re using a dedicated server, create a virtual document directory by following these steps:
   - a. Start your Web browser, and enter the URL `https://IPaddress:2200` (replacing `IPaddress` with the IP address of your server). If necessary, click **Yes** to close the security alert message box and open the Login window. Enter your administrative user name and password and then click **Login**.
   - b. Click to expand the **Open Source** heading on the left, and then click the **Apache 2.0** link. Click **Administer Single Apache Server** under the Apache 2.0 Links heading on the right to display the Server Status window.
   - c. Click the **Content Management** button, and then click **Additional Document Directories**.
   - d. Enter **Engineering** in the URL prefix text box. (If you’re using a shared classroom server, precede “Engineering” with your assigned student number.)
   - e. Enter the path to your CORP:\IT\Web\Engineer directory in the Map To Directory text box.
   - f. Click **Save** to open the Save and Apply Changes dialog box. Click **Save and Apply** to apply your changes to the Httpd.conf file and display the Success! message box. Click **OK** to return to Apache Manager.

2. Copy the **Radiance.jpg** file from the C:\WINNT\Web\Wallpaper directory to your CORP:\IT\Web\Engineer directory.

3. Create a simple HTML document that displays the Radiance.jpg file with the heading “Universal AeroSpace.”

4. Save the document as **Index.html** in your CORP:\IT\Web\Engineer directory.

5. Test the Web site by starting your Web browser and then entering the URL `https://IPaddress/Engineering` (replacing `IPaddress` with the IP address of your server and preceding “Engineering” with your assigned student number if you’re using a shared classroom server).

6. After your test document is displayed, have your instructor check your work.
