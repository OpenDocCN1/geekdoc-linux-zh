In the previous exercise, you enabled multiple certificate templates for autoenrollment in a Windows Server 2008 network. In the next section, you will configure and manage the process of enrolling users and computers for PKI certificates obtained from a Windows Server 2008 CA.

# Managing Certificate Enrollments

Using a **Windows Server 2008** CA, you can manage certificate enrollment in a number of ways depending on the needs of your organization. This section presents the mechanisms that can be used to enroll various entities for PKI certificates, including users and workstations, as well as scenarios requiring specialized certificates, such as those used by network devices and smart card enrollment agents.

![](bbox=[0.03, 0.21, 0.23, 0.25])

In a Windows Server 2008 Active Directory environment, you can automate the distribution of PKI certificates using any combination of the following features:

+   *   **Certificate templates** can be used to automate the deployment of PKI certificates by controlling the security settings associated with each template. The Security tab in the Certificate Templates snap-in allows an administrator to configure any of the following permissions on a certificate template:
+       a. The **Full Control** ACL allows a user to perform any action against a particular template; this should be reserved for CA administrators only.
+       b. The **Read** ACL allows users or computers to read a certificate template.
+       c. The **Write** ACL allows users or computers to modify a certificate template; this should also be reserved for CA administrators.
+       d. The **Enroll** ACL allows users or computers to manually request a certificate based on this template.
+       e. The **Autoenroll** ACL allows users or computers to be automatically issued certificates based on this template. For the Autoenroll permission to function, the Enroll permission must also be configured for the user, computer, or group in question. Additionally, you will need to configure an autoenrollment policy for your Active Directory domain using Group Policy.

+   *   **Group Policy** can be used to establish autoenrollment settings for an Active Directory domain. Like other GPO settings, this is managed using the Group Policy Management MMC snap-in. The relevant settings to control PKI autoenrollment can be found in the User Configuration→**Windows Settings**→**Security Settings**→**Public Key Policies** or Computer Configuration→**Windows Settings**→**Security Settings**→**Public Key Policies** nodes. The Certificate Services Client—Auto-enrollment node includes the following settings:
+       a. Enroll certificates automatically.
+       b. Do not enroll certificates automatically.
+       c. If you select the option to enroll certificates automatically, you can also select one or more of the following settings:
+           i. Renew expired certificates, update pending certificates, and remove revoked certificates.
+           ii. Update certificates that use certificate templates.
+           iii. Expiry notification to notify when a certificate has only a certain percentage of its lifetime remaining.

+   *   The **Certificate Request Wizard** enables a user to manually create a certificate request file using the Certificates MMC snap-in; this wizard creates a request file that can be used by the Certification Authority Authority MMC to generate a certificate based on the request.
+   *   **Certification Authority Web Enrollment** enables users to manually request certificates using a Web interface, located by default at `https://<CA Name>/certsrv` on a CA that is running the Certification Authority Web Enrollment role service.