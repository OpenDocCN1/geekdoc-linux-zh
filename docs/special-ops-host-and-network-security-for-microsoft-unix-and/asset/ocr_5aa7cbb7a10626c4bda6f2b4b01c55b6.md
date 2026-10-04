# Figure 6.7 Authenticating in LDP.EXE

![](bbox=[0.358, 0.101, 0.642, 0.203])

# Figure 6.8 Authenticated User Browsing Active Directory Tree

![](bbox=[0.285, 0.263, 0.753, 0.545])

Making searches in authenticated mode reveals much more. For the same Active Directory catalog where only 62 entries were visible to an anonymous user, now 1,300+ entries are visible. It is possible to search for specific types of entries or only in certain subtrees, such as CN=Users, DC=width, DC=home. This specifies only subtrees that hold user-related information. Configuration or Schema subtrees could be very interesting; for example: CN=Configuration, DC=width, DC=home", "CN=Schema, DC=width, DC=home.\ Note that although a privileged user by default can only browse this information, some entries may have been added by an administrator in a Schema subtree, for example, without assigning proper access rights to them, so that it is possible to modify them. This can lead to a complete disaster. If an Active Directory schema is damaged, this always leads to a malfunction. The only thing that can be done to fix the problem is to assign proper access rights to all objects created. Running Active Directory in a native mode (as opposed to mixed mode) can also limit the amount of information that is exposed, because native