
The command **complain** is used to activate learning or complain mode. You can either use the program or the profile as the argument: For instance, both **complain firefox** and **complain /etc/apparmor.d/usr.lib.firefox.firefox.sh** work to change AppArmor to learning mode for Firefox.

If you want to turn on learning mode for all applications confined by AppArmor, use **complain /etc/apparmor.d/\***.

In profiles that are in complain mode, the path to the application being confined is followed by **flags=(complain)**:

```
# Profile for /sbin/klogd
#include <tunables/global>
/sbin/klogd flags=(complain) {
...
}
```

Then actually use your application(s) to create events in the log file.

The next step is to start the Update Profile Wizard by starting YaST and selecting **Novell AppArmor > Update Profile Wizard**:

### Figure 7-6

![](img/63e88022bf135307e3eac051ad238b5b_351_0.png)

The interface is almost identical to the Add Profile Wizard interface; also the choices you are presented do not differ.

However, as you are updating different profiles, you have to pay special attention to the profile in the first line to be sure that your decision on allowing or denying fits the respective profile.

Once the log file has been processed, select **Finish**. The profiles will be reloaded, but AppArmor is still in complaint mode.

To have AppArmor again enforce the rules, use the command enforce, which has the same syntax as complain:

**enforce /etc/apparmor.d/*** puts all profiles in enforce mode.

# Delete a Profile

To delete a profile, start YaST and select **Novell AppArmor > Delete Profile**. Select the profile to delete; then select **Next**. After you select **Yes** in the confirmation dialog, the profile is deleted and the application is no longer confined by AppArmor.

# Administer AppArmor Profiles with Command Line Tools

There are various tools to create and maintain AppArmor profiles. These are:
- autodep
- genprof
- logprof
- vim

## autodep

autodep generates a profile skeleton for a program and loads into the Novell AppArmor module in complain mode.

The syntax is *autodep program1 program2 ...*

## genprof

genprof (Generate Profile) is used to create a profile for an application. Stop the application you want to create a profile for before running genprof.

genprof runs autodep on the specified program if there is no profile yet, puts the new or already existing profile in complain mode, marks the log file, and prompts the user to start the program to profile and to exercise its functionality.

```
dai0:~ # genprof firefox
Setting /usr/lib/firefox/firefox.sh to complain mode.

Please start the application to be profiled in another window and exercise its functionality now.

Once completed, select the "Scan" button below in order to scan the system logs for AppArmor events.

For each AppArmor event, you will be given the opportunity to choose whether the access should be allowed or denied.

Profiling: /usr/lib/firefox/firefox.sh

[(S)can system log for SubDomain events] / (P)inish
```

Once the user has done that and presses s in the terminal window where genprof is running, genprof calls logprof to run against the system log from where it was marked when genprof was started.

In case of access to a program, the dialog looks similar to the following:

```
Reading log entries from /var/log/audit/audit.log.
Updating subdomain profiles in /etc/apparmor.d.

Profile: /usr/lib/firefox/firefox.sh
Program: firefox
Execute: /bin/basename
Severity: unknown

[(I)nherit] / (P)rofile / (U)nconfined / (D)eny / Abo(r)t / (P)inish
```

In case of access to a file or directory, the dialog looks similar to this:

```
Complain-mode changes:

Profile:  /usr/lib/firefox/firefox.sh
Path:     /dev/tty
Mode:     rw
Severity: 9

1 - #include <abstractions/consols>
[2 - /dev/tty]

[(A)llow] / [D]eny / (G)lob w/(E)xt / (N)ew /
Abo(r)t / (F)inish
```

Press the number to switch lines as applicable, then press the letter in parenthesis corresponding to what you want to do. The options offered are the same as those within YaST. **New** corresponds to a certain extent to **edit** in YaST.

Once all log entries have been processed, you are returned to genprof, where you can start a new scan or Finish the profile generation.

```
Writing updated profile for /usr/lib/firefox/firefox.sh.

Profiling: /usr/lib/firefox/firefox.sh

[(S)can system log for SubDomain events] / (F)inish
```

## logprof

logprof is a tool used to scan the log **/var/log/audit/audit.log** for entries created by AppArmor for profiles in learning mode, and to interactively create new profile entries.

The choices you have are the same as those described under “genprof” on 7-21.

If you want logprof to start scanning from a certain point in the log file, you can pass a string that describes that point. The following is an entry in the log file:

```
type=APPARMOR msg=audit(852099290.789:1103): PERMITTING w
access to /root/.mozilla/firefox/uwgxf7zy.default/prefs.js
(firefox-bin(8770) profile /usr/lib/firefox/firefox.sh
active /usr/lib/firefox/firefox.sh)
```

Using the option -m: **logprof -m "852099290.789:1103"**, you can start the scan of the log file from that point, ignoring earlier entries.

## vim

The profiles can be changed using any text editor.

Compared to other editors, vim has the advantage that AppArmor includes a syntax highlighting description that enables vim to highlight syntax elements in profiles.

![](img/63e88022bf135307e3eac051ad238b5b_355_0.png)

> When confining Apache2, you can create subprofiles (also called hats) that use a different security context, for instance for pages using mod_php5. To make use of such subprofiles, an application has to be made “hat-aware.” For Apache2 this is achieved with module mod_change_hat that comes with AppArmor on SLES10. For details on hats, see **man change_hat** and section 5 of the *Administration Guide* in /usr/share/doc/manual/apparmor-admin_en/apparmor-admin_en.pdf. Subprofiles are part of the profile for the application itself and are administered with the same tools (genprof, logprof).

# Exercise 7-1 AppArmor

In this exercise you create, test, and improve a profile for the Firefox browser.

You will find this exercise in the workbook.

(End of Exercise)

# Objective 3

# Control AppArmor

AppArmor can be controlled using the script `/etc/init.d/boot.apparmor` or the link to this script, `/sbin/rcapparmor`. This script takes the usual parameters start, stop, etc, but because AppArmor is not a daemon, their significance is slightly different.

To control AppArmor, you have to know how to:
- Start and Stop AppArmor
- View AppArmor's Status
- Reload Profiles

## Start and Stop AppArmor

To confine an application, AppArmor has to be active before the application starts. Therefore, AppArmor is usually activated early in the boot process.

If you do not want AppArmor to confine your applications any longer, use `rcapparmor stop`. This unloads the profiles, but the AppArmor kernel modules apparmor and appnatch_pcre remain loaded. `rcapparmor kill` unloads the kernel modules as well. In both cases, applications are no longer confined.

`rcapparmor start` activates AppArmor. However, only applications started after the activation of AppArmor are confined. Even if, for instance, a profile for Squid exists, Squid will not be confined if it was already running before you started AppArmor. To include Squid in AppArmor's protection, you need to restart Squid after activating AppArmor.

## View AppArmor’s Status

**rcapparmor status** gives you a general overview of profiles and processes:

```
da10:~ # rcapparmor status
apparmor module is loaded.
50 profiles are loaded.
49 profiles are in enforce mode.
1 profiles are in complain mode.
Out of 69 processes running:
5 processes have profiles defined.
5 processes have profiles in enforce mode.
0 processes have profiles in complain mode.
```

To emphasize the point that, after restarting AppArmor, processes need to be restarted to be again confined, have a look at the following:

```
da10:~ # rcapparmor stop
Unloading AppArmor profiles                                  done
da10:~ # rcapparmor start
Loading AppArmor profiles                                    done
da10:~ # rcapparmor status
apparmor module is loaded.
50 profiles are loaded.
49 profiles are in enforce mode.
1 profiles are in complain mode.
Out of 62 processes running:
0 processes have profiles defined.
0 processes have profiles in enforce mode.
0 processes have profiles in complain mode.
```
