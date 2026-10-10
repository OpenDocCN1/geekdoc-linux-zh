PAUSE. You used Active Directory Domains and Trusts to verify a trust relationship.

In the previous exercise, you verified the validity of a trust relationship within the Active Directory Domains and Trusts MMC snap-in.

# VERIFY A TRUST RELATIONSHIP USING NETDOM

GET READY. Before you begin these steps, you must be logged on as a member of the Domain Admins group.

+   1. Open a command prompt and key the following text:
+   **netdom trust TrustingDomainName/d:TrustedDomainName/verify**
+   *   Replace `TrustingDomainName` with the domain that is allowing access to resources. `TrustedDomainName` is the domain that needs to gain access.

+   2. Press (**Enter**).

PAUSE. You used netdom to verify a trust relationship.

In the previous exercise, you verified the validity of an Active Directory trust relationship from the command line using the netdom tool.

# REVOKING A TRUST RELATIONSHIP

In some cases, it may be necessary to remove an established trust. If a corporation relinquishes its business relationship with a supplier that was trusted, you will need to revoke the trust to prevent unwanted access to network resources. Just like creating trust relationships, you can use Active Directory Domains and Trusts or netdom to revoke a trust.

# REVOKE A TRUST USING ACTIVE DIRECTORY DOMAINS AND TRUSTS

GET READY. Before you begin these steps, you must be logged on as a member of the Domain Admins group.

+   1. In Active Directory Domains and Trusts, right-click the domain for which you want to verify trusts and select **Properties**.
+   
+   2. On the Trusts tab, select **Domains Trusted By This Domain (Outgoing)** or **Domains That Trust This Domain (Incoming)**. Select the appropriate trust and click **Properties**.
+   
+   3. Click **Remove** and follow the prompts to revoke the trust relationship.
+   
+   4. Repeat steps 1 through 3 for the other end of the trust relationship.

PAUSE. You used Active Directory Domains and Trusts to revoke a trust relationship.

In the previous exercise, you removed an Active Directory trust relationship using the Active Directory Domains and Trusts MMC snap-in.

# REVOKE A TRUST USING NETDOM

GET READY. Before you begin these steps, you must be logged on as a member of the Domain Admins group.

+   1. Open a command prompt and enter the following text:
+   **netdom trust TrustingDomainName/d:TrustedDomainName/remove**