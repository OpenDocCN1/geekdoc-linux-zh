
![](img/c99d6f526a5f9fa62f2c34daada85ad7_365_0.png)

**Figure 10.2** Vshell SSH server requiring both username/password and public keys for authentication.

Now that the authentication requirement has been completed, you need to ensure that the proper port-forwarding items have been configured. Figure 10.3 shows the correct port-forwarding options to be used in order to meet the requirement to access e-mail, file sharing, and Web servers. Be sure to select the appropriate e-mail client for the application setting in the mail port-forwarding option.

Lastly, ensure that the CONNECT string is configured appropriately if any SecureCRT client ever needs to connect via a proxy server, as shown in Figure 10.4. Remember to remind users to check the “Use firewall to connect” option when they need to access the SSH server via a proxy server.

Now that SecureCRT has been configured for both authentication and port-forwarding requirements, SSH Communications’ SFTP client needs to be configured in order to support the file-sharing requirement. Since SFTP will be port forwarding via the SSH connection to/from the file server’s SSH server, very little configuration needs to be done on the SFTP client, aside from pointing the IP address to 127.0.0.1 on port 22, as shown in Figure 10.5.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_366_0.png)

**Figure 10.3** SecureCRT port-forwarding options in order to meet the requirements in case-study #1.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_366_1.png)

**Figure 10.4** CONNECT string in SecureCRT.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_367_0.png)

**Figure 10.5** SFTP client’s configuration.

# SSH Server Configuration

I will now shift gears to the SSH servers, specifically the main VShell SSH server (11.17.6.12), which will be used for remote access, and the secondary VShell SSH server on the file server (172.16.1.100), which will be used only for the SFTP subsystem. On the main VShell SSH server (11.17.6.12), you need to configure three items: access control, triple-DES or above cipher options, and port-forwarding filters.

First, set the access-control options for the VShell server. Under VShell’s Access Control section, you need to ensure that everyone has access to connect to the SSH server, but only for port-forwarding reasons, as shown in Figure 10.6.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_368_0.png)

**Figure 10.6** Access Control section for VShell.

Second, set the cipher options for the VShell server. Under VShell’s General section, there is a subsection called Cipher. Ensure that 3DES has been checked. This will meet the encryption requirement listed previously.

Lastly, set the port-forwarding filters for the VShell server. Under VShell’s Port Forwarding section, you will need to ensure that only port forwarding can be allowed to the identified e-mail, Web, and file servers. This setting is optional, since the firewall will block any port-forwarding connections by SSH clients that are not allowed; however, this step adds an extra level of security. The port-forwarding filters are shown in Figure 10.7.

The configuration on the VShell SSH server is minimal when compared with the primary SSH server. Because the VShell SSH server is being used only for its SFTP subsystem on the file server (172.16.1.100), only access control and SFTP need to be configured.

First, set the access-control options for the VShell server on the file server. Under VShell’s Access Control section, you will need to ensure that everyone has access to connect to the SSH server, but only for SFTP, as shown in Figure 10.8.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_369_0.png)

**Figure 10.7** Port-forwarding filters for VShell.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_369_1.png)

**Figure 10.8** Access Control setting on the file server’s VShell service.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_370_0.png)

**Figure 10.9** SFTP settings on the file server’s VShell service.

Next, set the SFTP options for the SFTP subsystem on the file server. The file server’s root-file directory is called Common and is located on a separate 500GB hard drive labeled X, which will be the partition (drive) for the SFTP root directory. Using VShell SFTP will limit all remote-access clients to that directory only and any subdirectories and/or files, as shown in Figure 10.9.

The last order of business is to configure the other clients to use the established SSH connection for communication. While limited space does not allow each step to be described in detail (see Chapter 7 for more detailed steps), the basic idea is to use the loopback interface, 127.0.0.1, for each IP address of the desired server and port, as shown in Table 10.2.

**Table 10.2** Client Specifications

| SERVICE | IP ADDRESS | PORT |
| :--- | :--- | :--- |
| Mail Relay | 127.0.0.1 | 25 |
| Mail Server | 127.0.0.1 | 110 |
| SFTP | 127.0.0.1 | 22 |
| Web (http://127.0.0.1) | 127.0.0.1 | 80 |

## Results Checklist

After the client setup has been completed, the requirements of case study # 1 will have all been met, as described in Table 10.3.

**Table 10.3 Business Requirements and Results**

| **BUSINESS REQUIREMENT** | **RESULTS** |
| :--- | :--- |
| Must support strong level on encryption (Triple-DES or above) | The VShell SSH server has been configured to use 3DES or above. |
| Must be accessible from all types of networks, including NAT\d networks, remote offices, hotel rooms, behind internal proxy servers, and organizations that only allow TCP port 80 and 443 outbound | All SSH architecture can always work from NAT\d networks, including remote offices and hotel rooms. VShell SSH server has been configured to listen on port 443, which makes it accessible to clients behind internal proxy servers and organizations that allow only TCP port 443 outbound. |
| Must support two-factor authentication | VShell has been configured to require a username/password and a public key for authentication, as shown in Figure 10.2. |
| Must be able to provide easy access to e-mail and intranet servers from internal networks, DMZ networks, and extranets | SecureCRT and VShell have been configured to allow port forwarding to access e-mail and intranet servers. The perimeter firewall allows communication from the SSH server to the appropriate server. |
| Must be able to provide secure file-sharing access | A separate VShell service has been installed on the file server, limited only for the SFTP subsystem and disabled for other utilities (remote access, port-forwarding, and remote execution). |
| Must require a single action from novice end-users for e-mail | The application option has been set on SecureCRT's port-forwarding option, which automatically executes the mail client after the SSH session has been established. |
| Must provide stable and consistent performance | SSH always provides stable and consistent performance after implementation. |

# Case Study #2: Secure Wireless Connectivity

The following case study examines an organization called Virtucion. Virtucion is a domestic corporation headquartered in Fremont, California. Virtucion is a think-tank organization that generates test questions for the Iowa standard-test program. Any leakage of test questions, whether they are notes, e-mails, chat messages, Web pages, or documents, would undermine the integrity of the Iowa test results. While most Virtucion employees work on the Virtucion campus, employees are often encouraged to work anywhere and anytime on the Virtucion grounds, whether it is in a conference room, a neighbor’s cube, or even outside on a box.

## The Problem

Virtucion needs to provide secure wireless connectivity for all its internal users. All buildings on the Virtucion campus should be equipped with wireless (802.11) connectivity for all employees, including conference rooms, outdoor lunch areas, and internal cubes and offices.

## Business Requirements

The following are the business requirements provided by Virtucion:

- Must support strong level on encryption (Triple-DES or above) and should not expose the internal corporate network to malicious activity
- Must provide complete access for two core-computing aspects of the organization, which are external Web access and internal e-mail
- External visitors, contractors/consultants, and war-drivers should be completely restricted from accessing the wireless network, even for external Web-access purposes
- Must require only a single action from novice end-users for e-mail and external Web access
- Must provide stable and consistent performance

Secure wireless connectivity for internal employees is a must in many organizations. Despite the overwhelming number of security exposures in 802.11 wireless networks, many organizations cannot afford to ignore wireless for much longer. This case study focuses on how to use SSH to secure wireless (802.11) networks.
