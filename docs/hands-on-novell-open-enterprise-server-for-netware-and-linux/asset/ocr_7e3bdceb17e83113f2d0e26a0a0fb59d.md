![](bbox=[0.07, 0.06, 0.57, 0.3])

Figure 5-14 Setting a time restriction from 12:00 a.m. until 6:00 a.m.

+   i. Click OK to save the time restrictions and return to the iManager main window.
+   2. Stay logged in to iManager for the next activity.

# Implementing Intruder Detection Limits

Another potential login security problem is an intruder who is able to guess user passwords successfully. Forcing user passwords to be longer than four characters and training users to create nonobvious passwords that contain numbers as well as characters can go a long way toward preventing password guessing. Having nonobvious passwords is critical because intruders could get lucky with guesses or might have a password-guessing program that can send hundreds of password combinations to a computer in just a few seconds. An effective way to deter password guessing is to set the NetWare Intruder Detection feature in each OU container.

**Intruder detection** works at the container level by setting a limit on the number of incorrect login attempts that can be made on a user account in that container during a specified time period. When a potential intruder reaches the maximum number of incorrect login attempts in the established time period, the user's account is locked for a specified time period, and the time and station address of the login attempt is recorded on the user's account. The user account becomes available again at the end of the lockout time period, or the Admin user can free the account at any time. In the following activities, you use iManager to set the Intruder Detection option for your UAS network, and then test your security by attempting several invalid passwords to lock out a user account.

# Activity 5-7: Enabling Intruder Detection
**Time Required:** 10 minutes
**Objective:** Use iManager to configure intruder detection settings.
**Requirements:** Same as Activity 5-5; a Windows XP or SUSE Linux 10 computer

**Description:** Because they are working on secure government contracts, some UAS engineers and IT staff have had to sign nondisclosure agreements for the projects they're working on. To help secure user accounts from unauthorized access, Eric has enabled the Intruder Detection option for the UAS, Engineering, and IT containers. In this activity, you use iManager to enable intruder detection to lock out a user's account for five minutes when more than five incorrect login attempts have been made in a 10-minute period.

+   1. If necessary, start your computer, and log on to your local computer with your assigned user name and password.
+   2. Start iManager as described in Activity 5-5, and log in with your administrative user name and password.
+   3. To configure intruder detection settings for the IT OU, follow these steps: