# Question 6

+   Which of the following keys can be used in the **attribute** field of the RBAC Execution Attributes Database file? (Select all that apply.)
+   
+   - [ ] a. `auths`
+   - [ ] b. `gid`
+   - [ ] c. `help`
+   - [ ] d. `profiles`
+   - [ ] e. `uid`

Answers b and e are correct. The only valid keys for the **attribute** field of the Execution Attributes Database file are **gid**, **gid**, **euid**, and **uid**. The **auths** key can be specified only in the User and Profile Attributes Database files. Therefore, answer a is incorrect. The **help** key is supported only in the Authorization and Profile Attributes Database files. Therefore, answer c is incorrect. The **profiles** key can be specified only in the User Attributes Database file. Therefore, answer d incorrect.

# Question 7

+   Which of the following describes the format of the RBAC User Attributes Database file?
+   
+   - (○) a. `name:qualifier:res1:res2:attributes`
+   - (○) b. `name:res1:res2:description:attributes`
+   - (○) c. `name:res1:res2:short description:long description:attributes`
+   - (○) d. `name:policy:type:res1:res2:ID:attributes`

Answer a is correct. The RBAC User Attributes Database file uses the format `name:qualifier:res1:res2:attributes`. `name:res1:res2:description:attributes` is the format of the Profile Attributes Database file. Therefore, answer b is incorrect. `name:res1:res2:short description:long description:attributes` is the format of the Authorization Attributes Database file. Therefore, answer c is incorrect. `name:policy:type:res1:res2:ID:attributes` is the format of the Execution Attributes Database file. Therefore, answer d is incorrect.