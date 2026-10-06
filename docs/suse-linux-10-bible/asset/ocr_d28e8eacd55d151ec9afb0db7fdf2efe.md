# 650 Part IV Implementing Network Services in SUSE Linux

PAM works by having a configuration file for each service that needs to authenticate users. For example, the login process has a separate PAM configuration file, as does the imap service.

These service configuration files are stored in /etc/pam.d and contain information about how the process gets information about the user, their account data, and passwords. Each file can contain four types of entries, discussed in Table 25-2.

# Table 25-2
PAM Configuration Entries

| Entry | Description |
| account | Used to check whether the user is allowed to log in, what the account expiry is, and so on. |
 password | Used to change the user's password. |
 auth | Used to check the user's password. |
 session | Used to enable or disable features of the user's session after he or has authenticated. This can be used to mount the user's home directory automatically.

> Note
PAM is not just for usernames and passwords; it is a general authentication library and can be used to check a smart card owned by the user to authenticate or in the future to read biometric data from the user, such as facial recognition.

For each entry type, you can specify a PAM module to handle the account, password-authentication, or session data related to a user account.

For example, if you want to allow the imap service to authenticate data to the system /etc/passwd and /etc/shadow, you need at minimum an account and authentication entry. This enables a user to log in if his or her account is active and also check whether the password provided by the user is correct.

```
auth required /lib/security/pam-unix.so nullok
account required /lib/security/pam-unix.so
```

This file has a bit of information in it, and you can see an entry for auth and account. The second, third, and fourth fields are also very important when configuring PAM for your service.

The second field determines how the data received back from the PAM module (specified in field three) is acted upon. When a PAM module is used, it returns