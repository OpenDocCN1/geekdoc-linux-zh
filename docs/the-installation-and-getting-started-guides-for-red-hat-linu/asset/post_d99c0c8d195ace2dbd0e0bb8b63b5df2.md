
![](img/46f4935125ba89e12897afbe9d77a097_187_0.png)

## Figure 8-7: Root Password Verification Screen

The screen is a little confusing because neither the title, nor the description really explains the screen’s purpose. Linuxconf seems to be asking for the new password, which isn’t actually the case. Instead, Linuxconf wants the current root password to verify access to the root account. Linuxconf does require root access to run, but once running there’s nothing to keep anyone from sitting down at the computer if the person using Linuxconf steps out for a minute. The potential pitfalls are extensive! If the person who was originally using Linuxconf logs out of root, they won’t be able to get back into it. A lack of validation would also give free reign over the computer to whoever had changed root’s password. Once you have entered root’s current password, it will prompt you for a new password. There is also a field called Confirmation where you will need to type the password again (see figure 8-5). This is to prevent you from mistyping the password. Passwords must be at least 6 characters in length. They may contain numbers as well as a mix of lowercase and uppercase letters. If you decide against changing the root password, just hit Cancel. Once you have entered the new password select Accept. The change takes place immediately and is effective not only for logging in as root, but also for becoming root using the su command.

## Disabling a User Account — Quick Reference

- 1 Start Linuxconf by typing linuxconf at the shell prompt.
- 2 Open [Config] -> [Users accounts] -> [Normal] -> [User accounts].
- 3 Select the account.
- 4 De-select the account is enabled check box.
- 5 Select Accept.

## Disabling a User Account — General Overview

Why disable an account? Good question! There's no single answer, but we can provide some reasons why this option is available. The biggest reason is security. For example, you may have created a special account to be used by clients, co-workers, or friends to access specific files on your system. This account gets used from time to time, but should only be used when you know there's a need. Leaving an unused account around is a target for people who'd want to break into your system. Deleting it requires you to recreate it every time you want to use it. Disabling an account solves both problems by allowing you to simply select or de-select a check-box. To disable an account:

- 1 Start Linuxconf by typing linuxconf at the shell prompt.
- 2 Open [Config] -> [Users accounts] -> [Normal] -> [User accounts].
- 3 De-select the check-box that states that The account is enabled. Select the Accept button at the bottom of the window and you're all set.

The account is disabled and can be enabled later using a similar method.

## Enabling a User Account

By default, all newly created user accounts are enabled. If you need to enable an account, you can use Linuxconf to do it.

Start Linuxconf by typing linuxconf at the shell prompt.

Open [Config] -> [Users accounts] -> [Normal] -> [User accounts].

Select the account you want to enable.

Select the The account is enabled check-box and then select Accept at the bottom of the screen.

## Deleting a User Account — Quick Reference

Start Linuxconf by typing linuxconf at the shell prompt.

Open [Config] -> [Users accounts] -> [User accounts].

Select the account you wish to delete.

On the User information screen select Del.

On the Deleting account... screen, choose the appropriate option for the account's data.

Select Accept.

## Deleting a User Account — General Overview

> Please Note: While there are a couple options that let you retain files associated with an account, any information or files deleted are gone and effectively unrecoverable. Take care when using this option! To delete an account:

- Start Linuxconf by typing linuxconf at the shell prompt.
- Open [Config] -> [Users accounts] -> [User accounts].
- On the User accounts screen (see figure 8-3) select the account you wish to delete.
- At the bottom of the User information screen (see figure 8-6) select Del to delete the account.

Linuxconf will then prompt you with a list of options.
