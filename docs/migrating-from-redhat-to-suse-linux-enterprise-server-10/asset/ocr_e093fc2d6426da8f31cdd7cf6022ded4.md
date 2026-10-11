# Delete a Profile

To delete a profile, start YaST and select **Novell AppArmor > Delete Profile**. Select the profile to delete; then select **Next**. After you select **Yes** in the confirmation dialog, the profile is deleted and the application is no longer confined by AppArmor.

# Administer AppArmor Profiles with Command Line Tools

There are various tools to create and maintain AppArmor profiles. These are

+   autodep
+   genprof
+   logprof
+   vim

# autodep

autodep generates a profile skeloton for a program and loads into the Novell AppArmor module in complain mode.

The syntax is *autodep program1 program2 ...*

# genprof

genprof (Generate Profile) is used to create a profile for an application. Stop the application you want to create a profile for before running genprof.