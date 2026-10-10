options to configure authentication and communication security within Active Directory through the use of the following settings:
*   **Domain controller: LDAP server signing requirements** controls whether LDAP traffic between domain controllers and clients must be signed. This setting can be configured with a value of *None* or **Require signing**.
*   **Domain member: Digitally sign or encrypt or sign secure channel data (always)** controls whether traffic between domain members and the domain controllers will be signed and encrypted at all times.
*   **Domain member: Digitally encrypt secure channel data (when client agrees)** indicates that traffic between domain members and the domain controllers will be encrypted only if the client workstations are able to do so.
*   **Domain member: Digitally sign secure channel data (when client agrees)** indicates that traffic between domain members and the domain controllers will be signed only if the client services are able to do so.
*   **Microsoft network client: Digitally sign communications (always)** indicates that Server Message Block (SMB) signing will be enabled by the SMB signing component of the SMB client at all times.
*   **Microsoft network client: Digitally sign communications (if server agrees)** indicates that SMB signing will be enabled by the SMB signing component of the SMB client only if the corresponding server service is able to do so.
*   **Microsoft network server: Digitally sign communications (always)** indicates that SMB signing will be enabled by the SMB signing component of the SMB server at all times.
*   **Microsoft network server: Digitally sign communications (if server agrees)** indicates that SMB signing will be enabled by the SMB signing component of the SMB server only if the corresponding client service is able to do so.

From this section, you can also enforce the level of NT LAN Manager (NTLM) authentication that will be allowed on your network. Although Kerberos is the default authentication protocol in an Active Directory network, NTLM authentication will be used in certain situations. The original incarnation of NTLM authentication was called LAN Manager (LM) authentication, which is now considered a weak authentication protocol that can easily be decoded by network traffic analyzers. Microsoft has improved NTLM authentication over the years by introducing first NTLM and subsequently NTLMv2. NTLM authentication levels are controlled by the Network security: NTLM authentication levels security setting, which allows you to select one of the following options:
*   Send LM and NTLM responses
*   Send LM and NTLM—use NTLMv2 session security if negotiated
*   Send NTLM response only
*   Send NTLMv2 response only
*   Send NTLMv2 response only. Refuse LM
*   Send NTLMv2 response only. Refuse LM and NTLM

By allowing only the most stringent levels of NTLM authentication on your network, you can improve the overall communications security of Active Directory. The final key component in defining Local Policies is planning and configuring an *Audit Policy* for a Windows Server 2008 Active Directory network, which we will discuss in-depth in the following section.

# Planning and Configuring an Audit Policy

> The Audit Policy section of GPO Local Policies allows administrators to log successful and failed security events, such as logon events, account access, and object access. Auditing can be used to track user activities and system activities. Planning to audit requires that you determine the computers to be audited and the types of events you wish to track.