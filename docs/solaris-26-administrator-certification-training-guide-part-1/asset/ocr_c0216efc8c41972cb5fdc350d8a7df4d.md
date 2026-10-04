This chapter describes how to use the Solaris Admintool to add user accounts to the system. When you're adding or modifying user accounts, the Admintool edits the files /etc/passwd. /etc/shadow, and /etc/group. As root, you could edit these files directly, but it is not recommended. Errors in any of the files could cause adverse effects on the system.

# Adding User Accounts with Admintool

To perform administrative tasks such as adding user accounts, the administrator must be logged in as superuser or be a member of GID 14. The first step in setting up a new user account is to have the user provide the information you will need to administer this account. You'll also need to set up proper permissions so the users can share information with other members of their departments. To start, you'll need to know the user's full name, department, and any groups with which the user will be working. I like to sit down with the user and fill out an information sheet like the one in Table 5-2 so I have all of the information I'll need when I set up the account.

**Table 5-2 User Information Data Sheet**

| Item | Description |
|---|---|
| User Name: |  |
| UID: |  |
| Primary Group: |  |
| Secondary Groups: |  |
| Comment: |  |
| Default Shell: |  |
| Password Status and Aging: |  |
| Home Directory Server Name: |  |
| Home Directory Path Name: |  |
| Mail Server: |  |
| Department Name: |  |
| Department Administrator: |  |
| Manager: |  |
| Employee Name: |  |
| Employee Title: |  |
| Employee Status: |  |
| Employee Number: |  |
| Start Date: |  |
| Desktop System Name: |  |