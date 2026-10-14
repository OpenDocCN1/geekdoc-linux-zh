+   - **password**—Verifies passwords and the strength of passwords.
+   - **session**—Processes session setup or teardown.

Each module family can contain multiple member modules. Each member module can be used to validate a specific characteristic required by the application being invoked. As an example, a collection of modules could check the group membership of an account, which terminal the account is being used from, as well as time of day. If all conditions are met, control is passed to the next family of modules. If not, the user session can be terminated.

In the simplest of cases, a family of rules can be satisfied by a single check. In most cases, however, applications require the validation of multiple aspects of an authentication before a user is granted access.

Each module can be further tweaked by passing parameters that modify its behavior. These passed values override preset default characteristics. The configuration files that store the default behaviors are stored in /etc/security. We examine them more closely in the next section.

For each member of each family, it is possible to define a “level of compliance” the rule must satisfy. This metric is called a control flag within PAM. Four different levels of control flags are currently recognized:

+   - **Required**—Individual veto for the module family. Unless this test returns a valid result, the family will refuse access.
+   - **Requisite**—Immediate veto of access. If this test fails, the authentication request will be immediately denied.
+   - **Sufficient**—If this test passes, no other steps need take place. Failure of this rule does not terminate the authentication process. Rule evaluation resumes with the next member of family.
+   - **Optional**—This rule is used to trigger events that do not directly affect the authentication process. It is usually used to provide the client with additional status information.

The permutations and combinations of the modules types (family), the control flags (compliance), and the individual modules available make PAM a granular method of authentication. The variations available also make understanding PAM configurations somewhat daunting. To get a better understanding of a typical PAM configuration, let’s examine an out-of-the-box configuration. Located in the /etc/pam.d directory is a PAM configuration file for the login process. Listing 5.5 shows the content of this file.