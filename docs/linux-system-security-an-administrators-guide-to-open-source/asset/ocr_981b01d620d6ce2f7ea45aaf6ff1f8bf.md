# Output Examples

You may also want to write your own scripts or programs or use other (besides logcheck and swatch) existing ones to capture certain types of activity. Example 8-3 shows a sequence of failed login attempts as reported by login and PAM to syslogd (line wraps are due to formatting constraints), which may represent an attempted break-in.

# Example 8-3 Failed login Attempts Using the Same Username

```
Mar  2 17:54:15 topcat login[14435]: FAILED LOGIN 1 FROM roadrunner FOR guest, Authentication failure
Mar  2 17:54:23 topcat login[14435]: FAILED LOGIN 2 FROM roadrunner FOR guest, Authentication failure
Mar  2 17:54:28 topcat login[14435]: TOO MANY LOGIN TRIES (3) FROM roadrunner FOR guest, Have exhausted maximum number of retries for service.
Mar  2 17:54:28 topcat PAM_pwdb[14435]: 3 authentication failures; (uid=0) -> guest for login service
```

Be aware, however, that different attacks will generate different log entries (often called signatures). Unfortunately, collecting a thorough list (it will never be complete!) of attack patterns is difficult due to the dynamic nature of attacks. The process of identifying attacks is known as intrusion detection. The section Intrusion Detection on page 172 provides some resources related to that topic. In the meantime, Example 8-4 shows us a different set of failed login attempts (line wraps).

# Example 8-4 Failed login Attempts Using Different Usernames

```
Mar  2 18:00:10 topcat login[14478]: FAILED LOGIN 1 FROM roadrunner FOR guest, Authentication failure
Mar  2 18:00:16 topcat login[14478]: FAILED LOGIN 2 FROM roadrunner FOR joe, Authentication failure
Mar  2 18:00:20 topcat login[14478]: FAILED LOGIN 3 FROM roadrunner FOR mary, Authentication failure
Mar  2 18:00:24 topcat login[14478]: FAILED LOGIN SESSION FROM roadrunner FOR sdm, Authentication failure
Mar  2 18:00:24 topcat PAM_pwdb[14478]: 1 authentication failure; (uid=0) -> sdm for login service
Mar  2 18:00:24 topcat PAM_pwdb[14478]: 1 authentication failure; (uid=0) -> mary for login service
Mar  2 18:00:24 topcat PAM_pwdb[14478]: 1 authentication failure; (uid=0) -> joe for login service
Mar  2 18:00:24 topcat PAM_pwdb[14478]: 1 authentication failure; (uid=0) -> guest for login service
```

The important thing about Examples 8-3 and 8-4 is to notice any similar key words or phrases that could be used in writing a script to capture these break-in attempts. In this case, notice that, although these two examples show different log entries for the two attacks, the process identifier (the number in brackets after either the keyword login or PAM_pwdb) is identical for each sequence of attacks. That, together with the fact that the key phrase authentication failure appears in almost every entry associated with these attacks,