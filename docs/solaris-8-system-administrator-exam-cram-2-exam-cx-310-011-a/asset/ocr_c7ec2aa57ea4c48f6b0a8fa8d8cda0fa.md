Database file. The Authorization Attributes Database defines privileged operations associated with a profile and does not relate directly to command execution. Therefore, answer a is incorrect. The User Attributes Database associates users and roles with authorizations and profiles, which also do not directly relate to command execution. Therefore, answer c is incorrect.

# Question 4

+   Which of the following keys are allowed in the **attribute** field of the User Attributes Database file? (Select all that apply.)
+   
+   - [ ] a. **auths**
+   - [ ] b. **help**
+   - [ ] c. **profile**
+   - [ ] d. **roles**
+   - [ ] e. **type**

Answers a, c, d, and e are correct. The **attribute** field of the User Attributes Database file can be used to assign authorizations, profiles, and roles. The **type** key identifies entries as being either normal user accounts or roles. The **help** key is supported only in the Authorization and Profile Attributes Database files. Therefore, answer b is incorrect.

# Question 5

+   Which of the following is the definition of a role?
+   
+   - ◯ a. A special user account to which authorizations and profiles are assigned.
+   - ◯ b. A right used to grant access to a restriction function.
+   - ◯ c. A mechanism used to group authorizations and profile assignments.
+   - ◯ d. A user account that does not require a password.
+   - ◯ e. A user account that can be accessed via the login command.

Answer a is correct. A **right used to grant access to a restriction function** is the definition of an authorization. Therefore, answer b is incorrect. A **mechanism used to group authorizations and profile assignments** is the definition of a profile. Therefore, answer c is incorrect. Roles, like other user accounts, require a password and can be accessed only by using the su(1) command. Therefore, answers d and e are incorrect.