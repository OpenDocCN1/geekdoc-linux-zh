+   6. Which feature allows you to control how much space a user can take on a particular hard drive volume, configurable via Group Policy?
+   a. Disk quotas
+   b. Folder redirection
+   c. Offline files
+   d. Object access auditing
+   7. To prevent users from re-using a certain number of network passwords, what can you configure as part of a domain-wide policy or as part of a Fine-Grained Password Policy?
+   a. Minimum password length
+   b. Minimum password age
+   c. Maximum password age
+   d. Enforce password history
+   8. A PasswordSettingsObject (PSO) within Active Directory is also known as which type of object?
+   a. msDS-PasswordSettingsPrecedence
+   b. msDS-PasswordSettings
+   c. msDS-PasswordComplexityEnabled
+   d. msDS-MinimumPasswordLength
+   9. Which Group Policy feature allows users to access user files when the user is disconnected from the corporate network?
+   a. Folder redirection
+   b. Disk quotas
+   c. Offline files
+   d. Object access auditing
+   10. Which audit event type is triggered when user or group accounts are created, deleted, renamed, enabled, or disabled?
+   a. Account logon events
+   b. Account management events
+   c. Privileged use events
+   d. Policy management events

# Case Scenarios

# Scenario 8-1: Lucerne Publishing and Offline Files

You are a computer consultant. Linda Randall, Chief Information Officer of Lucerne Publishing, has asked for your help. The Lucerne Publishing network consists of a single Active Directory domain with four domain controllers running Windows Server 2008, three file servers, and 300 clients that are evenly divided between Windows XP Professional and Windows Vista.

Recently, several publishing projects stored in electronic format were lost when an employee’s laptop was stolen from a publishing convention. Previously, another employee lost important publishing project files during a fire sprinkler system incident in which the employee’s computer was destroyed.

Employees typically store documents in the Documents folder on their local systems. Linda wants all employees to store their data on the network servers. The data on the network servers is backed up regularly. Linda tells you that her editors tend to work on sensitive data that requires special handling. She is especially worried that the data is backed up and secured.

All client computers have P drive mappings that are supposed to be used for storing files. However, many employees do not understand drive mappings. They often store files in their Documents folder and then copy them over to the P drive. This is also an issue because many employees forget to copy their files to the server until something occurs, such as a data loss.

Given Lucerne Publishing’s concerns, answer the following questions:

+   a. How would you address Linda’s concern that some employees do not understand drive mappings and others forget to store their data on the server?
+   b. How can you address the situation concerning the sensitive data editors use?
+   c. How would you address the users with mobile computers so that they could work on their files while traveling?
+   d. Linda warns that some users may have huge amounts of data already stored in the My Documents folder on their local computer. How might this affect your recommendations?