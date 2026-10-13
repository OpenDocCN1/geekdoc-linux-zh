The Home Directory section is used to define (and create, if necessary) the account’s home directory. This path is stored in the /etc/passwd file. The appropriate initialization files are created in the home directory based on the type of login shell selected.

**Table 6.1 User Identity Fields**

| Field | Description |
|---|---|
| User Name | A unique user account name consisting of a maximum of eight upper- and lowercase letters and/or numbers. |
| User ID | The UID associated with the user account. It is a unique number, typically between 1,000 and 60,000. The next available number starting at 1,000 is supplied automatically. |
| Primary Group | The group to which the user should be assigned. The default value is 10 (staff). Any specified group must exist before members can be added. |
| Secondary Groups | Additional groups (separated by commas) to which the user should be assigned. Specified groups must exist before members can be added. |
| Comment | Any text that should be placed in the /etc/passwd field. |
| Login Shell | The Bourne (default), C, or Korn shell can be selected. To specify another shell, select Other from the drop-down menu and enter the name of the shell in the field. |

**Table 6.2 Account Security Fields**

| Field | Description |
|---|---|
| Password | The choices are Cleared Until First Login, Account Is Locked, No Password—Setuid Only, or Normal Password. |
| Min Change | The minimum number of days required between password changes. |
| Max Change | The maximum number of days the password is valid. |
| Max Inactive | The maximum number of days the account can be inactive before the password must be changed. |
| Expiration Date | The date the account expires. |
| Warning | The number of days the user is warned before the password expires. |