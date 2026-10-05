# OffSec

Penetration Testing with Kali Linux

Next, the domain controller replies to the client with an Authentication Server Reply (AS-REP). Since Kerberos is a stateless protocol, the AS-REP contains a session key and a Ticket Granting (TGT). The session key is encrypted using the user's password hash and is decrypted by the client and reused. The TGT contains information regarding the domain, a timestamp, the IP address of the client, and the session key.

To avoid tampering, the TGT is encrypted by a secret key (NTLM hash of krbtgt¹¹⁰⁷⁹ account) known only to the KDC and cannot be decrypted by the client. Once the client has received the session key and the TGT, the KDC decides the client authentication process. By default, the TGT will be valid for ten hours, after which a renewal occurs. This renewal does not require the user to re-enter their password.

When the user wishes to access resources of the domain, such as a network share or a mailbox, it must again contact the KDC.

This time, the client constructs a Ticket Granting Service Request (TGS-REQ) packet which consists of the current user and a timestamp encrypted with the session key, the name of the resource, and the encrypted TGT.

Next, the ticket-granting service on the KDC receives the TGS-REQ, and if the resource exists in the domain, the TGT is decrypted using the secret key known only to the KDC. The session key is extracted from the TGT and used to decrypt the username and timestamp of the request. After this the KDC performs several checks:

+   1. The TGT must have a valid timestamp.
2. The username from the TGS-REQ has to match the username from the TGT.
3. The client IP address must coincide with the TGT IP address.

If this verification process succeeds, the ticket-granting service responds to the client with a Ticket Granting Service Reply (TGS-REP). This packet contains three parts:

+   1. The name of the service for which access has been granted.
2. A session key to be used between the client and the service.
3. A service ticket containing the username and group memberships along with the newly-created session key.

The service ticket's service name and session key are encrypted using the original session key associated with the TGT. The service ticket is encrypted using the password hash of the service account registered with the service in question.

Once the authentication process by the KDC is complete and the client has both a session key and a service ticket, the service authentication begins.

First, the client sends the application server an Application Request (AP-REQ), which includes the username and a timestamp encrypted with the session key associated with the service ticket itself.

> ¹¹⁰⁷⁹ (Active Directory Security, 2014), https://adsecurity.org/?p=483

PWK - © 2023 OffSec Services Limited. All rights reserved.

750