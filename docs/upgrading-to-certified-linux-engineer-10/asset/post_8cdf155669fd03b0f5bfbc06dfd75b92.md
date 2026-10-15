
## Part I: Create a Profile for the Firefox Browser

Do the following:

- 1. Start Yast, enter the root password (novell).
- 2. Select Novell AppArmor > Add Profile Wizard.
- 3. At the prompt: Application to Profile, enter firefox.
- 4. Start Firefox by pressing Alt+F2, entering firefox and selecting Run. View some web pages. Close Firefox again.
- 5. In the YaST AppArmor Profile Wizard dialog, select Scan system log for AppArmor events.
- 6. Now you create the profile and need to answer several questions. Note that the application Firefox is quite complex and accesses several executables and files on the system.
- a. Select Inherit for /bin/basename and other executed program.
- b. For files and directories, choose an appropriate option, such as an #include, a filename, a directory, or a path with place holders, and select Allow.
- 7. When you are returned to the AppArmor Profile Wizard dialog, select Finish.
- 8. Make sure that the Firefox profile is in enforce mode by looking at /sys/kernel/security/apparmor/profiles using cat. There must be an entry /usr/lib/firefox/firefox.sh (enforce). If it is not, execute enforce firefox.

## Part II: Modify the Profile for Firefox to Allow Read Access to the Local File System

Do the following:

- 1. Open a terminal window and su - to root (password novell).
- 2. Enter tail -f /var/log/audit/audit.log.
- 3. Start Firefox by pressing Alt+F2, entering firefox and selecting Run. Try to view the file /usr/share/doc/packages/apparmor-docs/apparmor.7.html. (You should not be able to do so.)
- 4. View the log file in the terminal window. You should see a reject message.
- 5. Stop viewing the log file by pressing Ctrl+c.
- 6. In the terminal window, enter complain firefox.
- 7. In Firefox, try again to access /usr/share/doc/packages/apparmor-docs/apparmor.7.html. You should now be able to access the file.
- 8. Start Yast, enter the root password (novell).
- 9. Select Novell AppArmor > Update Profile Wizard.
- 10. You are presented with the same interface as in Part I, where you can choose Allow, Inherit, Deny, etc. Make sure you are updating the Firefox profile, not some other profile.
  Sooner or later you should see an entry for the path /usr/share/doc/packages/apparmor-docs/apparmor.7.html. By selecting the Glob button three times, you can create a suggestion /usr/share/doc/**. Allow it by selecting Allow.
- 11. When all entries in the log file have been processed, select Finish.
- 12. Put the Firefox profile back in enforce mode by entering enforce firefox in the terminal window.

10. Start Firefox again and select another Java demo available at the URL given in Step 4. This should work now, despite the profile being in enforce mode again.

## Part IV: Compare the Profile You Created with Those From SLES 10

Do the following:

- 1. Open a console window and view the profile /etc/apparmor.d/usr.lib.firefox.firefox.sh just created with cat.
- 2. Open another console window and view the profiles /etc/apparmor/profiles/extras/usr.lib.firefox.firefox*, using cat.
- 3. Compare the files. Note any differences and decide whether or not they are more restrictive than the one you created.

(End of Exercise)

## Objective 3 Control AppArmor

AppArmor can be controlled using the script **/etc/init.d/boot.apparmor** or the link to this script, **/sbin/rcapparmor**. This script takes the usual parameters start, stop, etc. but because AppArmor is not a daemon, their significance is slightly different.

To control AppArmor, you have to know how to

- Start and Stop AppArmor
- View AppArmor's Status
- Reload Profiles

### Start and Stop AppArmor

To confine an application, AppArmor has to be active before the application starts. Therefore, AppArmor is usually activated early in the boot process.

If you do not want AppArmor to confine your applications any longer, use **rcapparmor stop**. This unloads the profiles, but the AppArmor kernel modules apparmor and aamatch_pcre remain loaded. **rcapparmor kill** unloads the kernel modules as well. In both cases, applications are no longer confined.

**rcapparmor start** activates AppArmor. However, only applications started after the activation of AppArmor are confined. Even if, for instance, a profile for Squid exists, Squid will not be confined if it was already running before you started AppArmor. To include Squid in AppArmor's protection, you need to restart Squid after activating AppArmor.
