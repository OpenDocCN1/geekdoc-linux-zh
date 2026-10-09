# # ACTIVITY 14-3
## Resetting a Password

**Before You Begin:**

+   1. On `srvA`, you have logged in as `root` in the CLI.
2. The first terminal is displayed.
3. Log out of the `root` user account.

**Scenario:**
You have administrative access to your Linux system. Your colleague, Eric, has forgotten the password to log in to his system.

| What You Do | How You Do It |
| :--- | :--- |
| 1. Switch to the `root` user account. | a. Log in as `jsmith`.
b. Enter `su - root` to switch to the `root` user account.
c. Enter `p@ssw0rd`
d. Enter `whoami` to view your user name.
e. Observe that you are logged in as the `root` user. |
| 2. Change the password for the user, Eric. | a. Enter `passwd eric` to change the password of the user `Eric`.
b. Enter `myp@$Sw0rd1` to reset the password.
c. Enter `myp@$Sw0rd1` to confirm the password.
d. Observe that the password is reset.
e. Enter `exit` to exit the `root` user account. |