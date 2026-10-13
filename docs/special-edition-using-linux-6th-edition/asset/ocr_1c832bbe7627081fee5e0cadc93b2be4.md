# LISTING 15.2 CONTINUED

```
#password   required    /lib/security/pam_cracklib.so
password    required    /lib/security/pam_pwdb.so shadow nullok use_authtok
session     required    /lib/security/pam_pwdb.so
```

Each file contains four columns. The first column is the type column, which is one of the following:

+   - **auth**—Short for authentication. This type deals with verifying that a user is who he claims to be. This is normally done via a username/password pair, but it can also be done through a biometric device or a smartcard. You need modules to interact with the biometric device or smart card.
+   - **account**—Verifies access privileges and status of a particular account (active, expired, inactive, or disabled).
+   - **password**—Used to update authentication tokens. If a password has expired, it forces a password update.
+   - **session**—Prepares the environment for the user. Can perform logging actions and run programs at login and logout (such as mounting directories, performing a chroot, and more).

The second column is the control field and indicates how the value returned by the module is used. Modules return SUCCESS, FAILURE, or IGNORE as a value to the PAM library. SUCCESS and FAILURE are self-explanatory. IGNORE means that the module could not determine a success or failure. This might have happened because the mechanism for determining success or failure was not present or was inaccessible. The control field has one of the following values:

+   - **requisite**—This means that a FAILURE determination from this module is final. If this module is first and a logging module is included later, a FAILURE here passes FAILURE back to the restricted service immediately and the logging module does not run. You probably don’t want to use this control.
+   - **required**—The required control is combined with all other lines. That is, regardless of the determination from this module, all successive modules are evaluated as well (unless a requisite is encountered and it returns FAILURE—see the preceding text—or a sufficient is encountered and it returns SUCCESS—see the following text).
+   - **sufficient**—The sufficient control immediately passes a SUCCESS back to the calling restricted service as long as no prior required control holds a value of FAILURE. If a sufficient control holds a value of IGNORE or FAILURE, it is treated as an optional control with the same value.
+   - **optional**—An optional control field is ignored unless it is the only module for its type. If an optional control is the only one for its type, it is treated as a required control.