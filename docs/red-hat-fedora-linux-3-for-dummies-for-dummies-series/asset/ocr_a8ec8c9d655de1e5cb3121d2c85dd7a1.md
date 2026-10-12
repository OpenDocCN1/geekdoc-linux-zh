# Part I: Installing Fedora Core

![](bbox=[0.22, 0.1, 0.55, 0.39])

**Figure 4-5:** The Create New User dialog box.

+   * You can enter your full name if you want. That information is saved in the `/etc/passwd` file, which anyone with an account on your system can read. This information is generally useful to system administrators because it allows them to connect a person with each account. (Well, okay, it’s probably superfluous if you’re configuring your personal system.)

+   * The new password should be different from the one you use for `root`.

As you type the password, a line of asterisks (rather than the actual password) appears on-screen in case someone is looking over your shoulder as you type. (Fedora Core is showing its paranoid side here.) In text mode, you don’t get any feedback, such as asterisks or other characters.

+   * Among your many choices for a default shell, `/bin/bash` is a good choice (`bash` is a popular shell that is the default for Fedora Core).

4. Click **OK**.

Your account is created.

![](bbox=[0.12, 0.78, 0.19, 0.85])

Fedora Core uses the Pluggable Authentication Module (PAM), which prevents you from entering trivial or otherwise dangerous passwords; don’t use that as assurance, however, that your new password is a good one. A good password cannot be found in any dictionary because password crackers have programs that automatically try all dictionary words to crack your password. Avoid birthdays and anniversaries or anything someone could associate with you. For ideas about good passwords, check out Chapter 3. Just don’t forget it, and *don’t* write it on a sticky note and put it on your monitor!