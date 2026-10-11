# **Tips**

Why does installing the domain controller in an existing domain delete all local accounts on the server?

Joining an existing domain deletes all local accounts on the server because all accounts must be configured through the Active Directory. This feature eliminates possible security problems or duplicate accounts. When you have a stand-alone server, you can configure user accounts so that users can log on to your local machine. After you upgrade the server to domain controller status with the Active Directory, users cannot log on locally to the domain controller, but must be authenticated through the Active Directory.

What is a child domain?

A child domain exists beneath a parent domain. The parent domain is in control of the child domain. You can think of the parent domain as an umbrella, with the child domain existing beneath the umbrella. Child domains have a DNS extension of the parent domain. For example, if a domain is named corp.com, a child domain could be named atlanta.corp.com. See Chapter 9 to learn more.

![](bbox=[0.03, 0.51, 0.47, 0.82])

![](bbox=[0.51, 0.51, 0.95, 0.82])

+   10 Click the appropriate radio button to create a new forest of domain trees or place the new domain tree in an existing forest.

+   11 Click Next to continue.

+   12 Type the DNS name for the domain.

+   13 Click Next to continue.

Your selections may vary depending on the configuration you chose in Steps 5 and 6.

CONTINUED