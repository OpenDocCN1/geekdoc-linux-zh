
system, you must use the yppasswd command to establish or change your password. Your system administrator can advise you on the specific procedures for your system.

## 1.5.1 Password Guidelines

The following guidelines are useful in selecting a password:

- *Do not* choose a word found in a dictionary.
- *Do not* use personal information as your password, or as a substring of it, such as your user name, names or nicknames (yours, your family's, your company's, your pet's), initials, or the make or model of your car.
- *Do not* use birthdays, Social Security or bank account numbers, employee identification numbers, telephone numbers, or other similar information as a password or as the numeric portion of a password.
- *Do not* use the default password you received with your account.
- *Do not* use old passwords or the same prefix or suffix you used in previous passwords. This rule also applies to any passwords you may have used in previous jobs.
- *Do not* use the same password on all systems when you have access to several different systems.
- *Do not* choose a password that is easy to guess (includes all of the above options) even if you reverse their spelling. Choose a password that is hard to guess, not hard to remember.
- *Do not* choose passwords shorter than six characters in length. The maximum length of your password depends on the security conventions in force on your system. (Password length is measured in bytes, rather than characters, but we can regard these terms as the same, for now.)
- *Do not* write your password on paper or place it in a file on the system.
- *Do not* put your password in e-mail.
- Use a mixture of uppercase and lowercase letters in your password if possible. You also should include any combination of numbers, punctuation marks, or underscores (_) in your password.
- Change your password frequently, especially if you think it might have been compromised.

On most systems, you can change your password as often or seldom as you like. However, to protect system security, your system administrator may set limits on how often you should change your password, the length of time your password remains valid, or the nature of changes you can make. Some typical password restrictions could be the following:

- Character restrictions
  - Minimum number of alphabetic characters
  - Minimum number of other characters, such as punctuation or numbers
  - Minimum number of characters in a new password that must be different from the old password
  - Maximum number of consecutive duplicate characters allowed in a password
- Time restrictions
  - Maximum number of weeks before your password expires
  - Number of weeks before you can change a password

See your system administrator for more information about password restrictions. There are several levels of security and access control that may be installed or activated on your system. See the Security manual for additional information about access control.

## 1.5.2 Password Procedures

To set or change your password, follow these steps:

- 1. Enter the passwd command:
  $ passwd
  The system displays the following message (identifying you as the user) and prompts you for your old password:
  Changing password for username
  Old password:
  If you do not have an old password, the system does not display this prompt. Go to step 3.
- 2. Enter your old password. For security reasons, the system does not display your password as you enter it.
  After the system verifies your old password, it is ready to accept your new password, and displays the following prompt:
  New password:
- 3. Enter your new password at the prompt.
  Remember that your new password entry does not appear on the screen. Finally, to verify the new password (since you cannot see it as you enter), the system prompts you to enter the new password again:
  Retype new password:
