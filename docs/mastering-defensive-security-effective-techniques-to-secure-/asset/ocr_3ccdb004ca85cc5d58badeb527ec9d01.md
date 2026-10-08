# Understanding layer 8 – the insider threat 121

Now, let's take a look at one example of a very common practice in IT departments, which is a really bad practice for security.

# Shared credentials

By default, the best practice says that shared credentials should NOT be allowed in your infrastructure. However, in case you do have them, you need to set up additional controls in place such as Multifactor Authentication (MFA), Role-Based Access Control (RBAC), and Privileged Access Management (PAM).

PAM works by locking shared credentials into a repository that can only be accessed by authenticated employee accounts (enabling accountability). The credential is used by the system administrator, the credential is reset for the next employee. Although PAM solves the challenge of shared accounts, it is very expensive to implement:

![](bbox=[0.118, 0.376, 0.842, 0.593])

Figure 4.7 – An example of a PAM system

The preceding diagram is an example of a PAM system and shows how each user logs into a centralized system (to enable accountability), and then from there, inject the shared account into the server.

# Audits

This topic was already covered in detail in Chapter 3, Comprehending Policies, Procedures, Compliance, and Audits; however, I want to highlight that audits are one of the most effective ways to detect malicious insiders, so make sure your infrastructure is audited regularly (either internally or externally).