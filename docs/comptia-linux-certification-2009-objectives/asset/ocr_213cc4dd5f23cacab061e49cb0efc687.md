# TOPIC C

# Manage User and Group Accounts

You created user and group accounts and even configured user profiles. Your next step will be to manage user and group accounts on an ongoing basis. This will enable you to efficiently organize your Linux environment. In this topic, you will manage user and group accounts.

Once a user or group account is created, there are many tasks that need to be performed to maintain that account. As a system administrator, you will be required to maintain the accounts and passwords of numerous users. This is achieved by effective management of user and group accounts.

# The userdel Command

The *userdel* command allows you to modify the system account files, deleting all entries that refer to the login of an existing user. However, it will not allow you to remove an account if the user is currently logged in. You must kill any running processes that belong to an account before deleting the account.

![](bbox=[0.75, 0.31, 0.9, 0.41])

![](bbox=[0.1, 0.42, 0.65, 0.71])

*Figure 2-10: The userdel command is used to delete an unused user account.*

# The -r Option

The *-r* option will delete the files in the user’s home directory, along with the home directory itself. Files located in other filesystems will have to be searched for and deleted manually.