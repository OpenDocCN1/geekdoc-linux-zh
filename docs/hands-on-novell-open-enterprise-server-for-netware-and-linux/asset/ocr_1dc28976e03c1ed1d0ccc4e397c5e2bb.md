# Activity 14-8: Enabling Universal Passwords and Samba Access

**Time Required:** 10 minutes

**Objective:** Use iManager to enable universal passwords.

**Requirements:** A Windows XP computer

**Description:** Several employees in the AeroDyn Division will be using Windows XP without Novell Client to access data on the SUSE Linux server. Eric wants you to test how this works by using Samba. In this activity, you prepare for this task by enabling universal passwords and enabling user accounts for Samba access.

+   1. Log on to your Windows XP computer.
+   2. Start your Web browser, start iManager, and log in to iManager with your administrative user name and password.
+   3. Expand the **Passwords** heading and click the **Password Policies** link to display the existing password policies (see Figure 14-13).

![](bbox=[0.1, 0.3, 0.6, 0.55])

**Figure 14-13** The Password Policies window

+   4. Click the **Edit** button to display the Policy Summary tab shown in Figure 14-14. Verify that all the Universal Password settings are set to true, except the Remove the NDS password when setting Universal Password option, which should be set to false.

![](bbox=[0.1, 0.66, 0.6, 0.92])

**Figure 14-14** Viewing a summary of current password policies