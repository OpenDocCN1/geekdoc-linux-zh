+   8. You have assigned several applications using GPOs. Users have complained that there is a delay when they double-click the application icon, which you know is the result of the application being installed in the background. What option can you use to pre-install assigned applications when users log on or power on their computers?
+   a. Uninstall when the application falls out of scope
+   b. Install This Application At Logon
+   c. Advanced Installation Mode
+   d. Path rule

+   9. Which of the following is used to develop information systems software through a structured process that includes analysis, design, implementation, and maintenance?
+   a. Hash algorithm
+   b. System Development Life Cycle
+   c. Software Restriction Policy
+   d. Group Policy Object

+   10. Which of the following Default Security Levels in Software Restriction Policies will disallow any executable from running that has not been explicitly enabled by the Active Directory administrator?
+   a. Basic User
+   b. Restricted
+   c. Disallowed
+   d. Power User

# Case Scenarios

# Scenario 9-1: Planning Group Policy Software Deployments

Your company, a healthcare organization, is currently working toward compliance with new government standards on patient confidentiality. Your IT department has decided that using software restriction policies with standard user access permissions will help to fulfill the necessary security requirements. You are preparing an implementation plan that is based on user needs and security requirements. Users should not be able to access any programs with the exception of those that are pertinent to their jobs. In addition, the user needs within the organization are as follows:

+   * Users only need access to e-mail and a patient database.
+   * The patient database has its own built-in security access system that is configured for each user based on the user's needs within the program.
+   * All user accounts are located in containers based on the user's office location.

In addition, the following points should be considered in your implementation plan:

+   * Software restriction policy settings should not affect settings that are already in place within existing GPOs. If problems arise with software restriction policies, they should be easy to rectify, without affecting other security areas.
+   * Administrator accounts should not be affected by software restrictions.
+   * Other applications should not be affected by any of the restrictions.

List the key points that should be part of your implementation plan based on the information provided here.

# Scenario 9-2: Consulting with Wide World Importers

You have been asked by Max Benson, CEO of Wide World Importers, to advise the company on the software deployment issues they are facing. Wide World Importers is an import/export company handling primarily clothing and textile products. It has offices in New York, New York; San Diego, California; and Fort Lauderdale, Florida. Wide World's network is configured as a single Active Directory domain with sites and OUs for each location. Below each top-level OU is a second layer of OUs representing the functional areas of Shipping, Finance, and Marketing. The users and client computers are distributed as shown in Table 9-1.