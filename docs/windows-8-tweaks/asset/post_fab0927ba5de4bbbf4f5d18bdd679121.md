
complex passwords that will be hard for anyone to guess and hack with brute force techniques.

## Controlling Your Computer Accounts

Your computer’s physical security, as well as online security, depends on how easy it is to access your accounts. This book shows you many ways that you can protect your computer, but almost all of them can be defeated by an account on your computer that has a poor password or no password at all. This is why it is critical to ensure that your computer is protected by accounts with strong passwords. Anything less will weaken your entire security defense.

This section shows you how you can manage your user accounts in Windows 8 to make sure they are all well protected.

### Using Complex Passwords on All Your Computer Accounts

All the accounts on your computer should have a complex password associated with them in case your computer is ever exposed to the Internet. Passwords such as easy-to-remember words and predictable key combinations, such as "asdf," just don’t cut it. These types of passwords are vulnerable to brute force dictionary attacks where an intruder can use special software to try hundreds of combinations to hack into your account.

A complex password is a password that has at least eight characters and consists of uppercase and lowercase letters, as well as numbers or other symbols. Ftm3D8&- is an example of a complex password. Something such as this is very difficult to guess and will take quite some time for a brute force technique to crack it.

Using complex passwords on all your accounts might not be easy at first, but after a while they will grow on you and you will have no problem remembering them. To prevent losing access to any encrypted files, it is best to log on to each account that does not already have a complex password and change them. If you use the Set Password function in Computer Manager, you risk losing access to any files that were encrypted under the user’s account.

Follow these steps to safely change a user’s account password:

- 1. Log on to the user’s account that needs a password change.
- 2. Press and hold Ctrl+Alt+Delete so that the secure desktop is shown (see Figure 18-6).
- 3. Click the Change Password button.
- 4. Type the old password once and then the new password for the user twice, and click the blue arrow button.

![](img/ea75090cfee8ac890f64c8c4f62f7285_341_0.png)

Figure 18-6: Windows 8’s secure desktop offers you a safe way to change user passwords.

The password for the account has now been changed.

### Assigning a Password and Renaming the Guest Account

One of the default accounts set up in Windows 8 is the Guest account. This account can be useful if your computer is in a public place such as a library and a low-rights account is needed. However, for most of us, this account is just another possible security hole because it cannot be deleted. It is disabled by default, but it could be enabled again by a virus or malware if your computer ever gets infected. The best way to neutralize this account is to give it a random password and rename it to eliminate the chances that some script will be able to use it.

Follow these steps to protect this account:

- 1. Open the Start screen, type compmgmt.msc, and hit Enter.
- 2. After Computer Management loads, expand Local Users And Groups and click the Users folder. All the local computer accounts are listed, as shown in Figure 18-7.
- 3. Right-click the Guest account on the list and click Set Password.

A warning screen appears telling you what may happen if you proceed.

- 4. Disregard the warning message and click Proceed.
- 5. When the Set Password window appears, type a completely random, complex password in both boxes, and click OK. The new password will now be set.

I suggest using a password that is at least 20 characters long.

![](img/ea75090cfee8ac890f64c8c4f62f7285_342_0.png)

- 6. Rename the account to confuse any malicious scripts that might be looking for it. Right-click the Guest account again and click Rename.
- 7. Type a new account name that has some random letters and numbers in it.

You just want to make it different from Guest.

- 8. When you are done renaming it, click Enter and you are finished.

Your Guest account is now more secure than ever.

### Secure the Administrator Account

The Administrator account is the most important account on the computer because it has the highest permissions and can do anything it wants to the configuration and settings of your computer. Securing this valuable account is critical to the overall security of your computer.

You secure it by ensuring the account is disabled, setting a strong password, and renaming it so that it is harder for malicious scripts and viruses to try to use. Doing this is very similar to securing the Guest account as you just did in the previous section.

Follow these steps to protect your Administrator account:

- 1. Open the Start screen, type comppmgmt.msc, and hit Enter.
- 2. After Computer Management loads, expand Local Users And Groups and click the Users folder.
- 3. Right-click the Administrator account and click Properties.
- 4. Check the Account Is Disabled option if it is not already selected, as shown in Figure 18-8. Then click OK to save the changes.

![](img/ea75090cfee8ac890f64c8c4f62f7285_343_0.png)

Figure 18-8: Disabling the Administrator account is the first step toward securing it.

- 5. Right-click the Administrator account and click Set Password.
A warning screen appears telling you what might happen if you proceed.
- 6. Disregard this message and hit Proceed.
- 7. When the Set Password window appears, type a completely random, complex password in both boxes that I suggest is at least 20 characters long and click OK.
The new password will now be set.
- 8. Rename the account to confuse any malicious scripts that might be looking for it. Right-click the Administrator account again and select Rename.
- 9. Type a new name for the account that has some random letters and numbers in it. I like to use AdminDisabled [random numbers] as a new name.
- 10. Press Enter and you are finished.

Now both of the built-in Windows 8 accounts are secured.

### Hiding Usernames on the Logon Screen

If you use your computer in a high-security environment, it is very important to hide your username from the logon screen so that potential intruders are not able to figure out your username—before they even try to break your password. Using the Local Security Policy to your advantage, you can configure a setting that will automatically clear the username of the last person who logged in. This adds another layer of protection to your account by putting it in stealth mode. Follow these instructions to turn on this setting:

- 1. Open the Start screen, type **secpol.msc**, and hit Enter.
- 2. After the Local Security Policy editor has loaded, expand Local Policies and click Security Options.
- 3. Scroll through the list and right-click Interactive Logon: Do Not Display Last User Name, and then click Properties.
- 4. Select the Enabled box, as shown in Figure 18-9, and click OK.

![](img/ea75090cfee8ac890f64c8c4f62f7285_344_0.png)

Figure 18-9: Hide your username with the Local Security Policy editor.

- 5. Close the Local Security Policy editor and you are finished.

The next time you reboot, your username will be hidden.

### Setting the Account Lockout Policy

To complement the new complex password that your accounts now have, I recommend configuring the Account Lockout Policy to add even more security to your accounts. The Account Lockout Policy enables you to protect your account from an intruder trying dozens or even thousands of possible password combinations while attempting to guess your password. When configured, after the intruder has entered the wrong password a set number of times, the account will then be locked for a set amount of time. After that time interval has passed, the account is unlocked and the whole process is reset.

This provides valuable additional security for your accounts that will eliminate the effectiveness of certain brute force tools that will try every possible combination to hack into your account. By using the Account Lockout Policy, you can increase the amount of time a malicious user has to wait to try every possible combination to something infeasible.

Setting the Account Lockout Policy is very similar to configuring your computer not to show the last username that was used to log in with. Follow these steps to configure the lockout policy for your computer:

- 1. Open the Start screen, type **secpol.msc**, and hit Enter.
- 2. After the Local Security Policy editor loads, expand Account Policies and then click Account Lockout Policy.
- 3. Right-click Account Lockout Threshold and click Properties.
- 4. Increase the number of invalid logon attempts from 0 to a higher value to enable the feature.

I like to use 5 as my number of invalid logon attempts before my account is locked out.

- 5. Click OK to save the setting. A Suggested Value Settings window pops up that automatically populates the two other settings: Account Lockout Duration and Reset Account Lockout Counter After. Click OK here as well to use the default values.
- 6. If the 30-minute duration of the account lockout is too long for you, just right-click each setting, select Properties, and modify the value.

I typically use 10 minutes for both of these settings because I think it is a nice balance between added security and inconvenience when I may be using my computer half asleep and type in the wrong password more than five times.

Your Account Lockout Policy is now set up and will begin protecting your computer immediately.
