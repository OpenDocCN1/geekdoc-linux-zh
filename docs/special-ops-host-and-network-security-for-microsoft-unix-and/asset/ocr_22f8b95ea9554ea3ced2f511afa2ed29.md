# Chapter 17 • Architecting the Human Factor

+   3. Appoint a VPN coordination team to manage remote access requests. Once the documents have been filed, team members will be responsible for validating the request parameters (reason, duration, etc.) on both internal and external requests are reasonably similar in scope. This is also tasked with escalating requests that impose additional security risks, such as when a remote party requires services beyond simple client-server access, interactive system control or administrative access levels. The processes for approval should provide formal escalation triggers and procedures to avoid confusion about what is and is not acceptable.

+   4. Once requests have been validated, the VPN coordination team should contact the administrators of the internal devices that will be made accessible, verify that both they are aware of the remote access request and that they are confident that the host(s) available will not impose any additional security risks to the organization.

+   5. If your organization has an audit team for verifying information security policy compliance, involve them in this process as well. If possible, arrange for audit to verify any access limitations are in place before releasing the login information to the remote party.

+   6. Finally, the VPN coordination team can activate the remote access account and begin their periodic access review and renewal schedule.

# Technical VPN Access Procedures

The technical aspect of the remote access solution deals with developing a remote-access infrastructure that will support the requirements and granularity laid out in the documents provided in the organizational phase. Approving to allow NetBIOS access to the file server at 10.2.34.12 is moot if your infrastructure has no way of enforcing the destination address limitations. By the same token, if your VPN devices do provide such functionality but are extremely difficult to manage, the VPN administrators may be lax about applying access controls.

When selecting your VPN provider, look for the following features to assist the administrators in providing controlled access:

+    Easily configurable access control policies, capable of being enabled on a user or group basis.