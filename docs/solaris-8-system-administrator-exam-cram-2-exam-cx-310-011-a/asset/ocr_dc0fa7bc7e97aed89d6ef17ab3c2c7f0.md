# # Practice Questions

# ## Question 1

+   Which of the following commands is used to determine when a particular login account was last used?
+   
+   - ○ a. **logins**
+   - ○ b. **last**
+   - ○ c. **whodo**
+   - ○ d. **ps**

Answer b is correct. The **logins** command displays attributes about login accounts, not the usage of the login accounts. Therefore, answer a is incorrect. The **whodo** and **ps** commands list information about processes. Therefore, answers c and d are incorrect.

# ## Question 2

+   The /etc/syslog.conf file was modified to capture messages from a particular user application, but the log file still does not contain any of those messages. Which of the following reasons could explain this situation? (Select all that apply.)
+   
+   - □ a. A typographical error exists in the /etc/syslog.conf entry that was added.
+   - □ b. The **syslogd** program was not restarted.
+   - □ c. The user application does not generate the expected facility and/or severity of messages.
+   - □ d. The **syslogd** program is not running.
+   - □ e. The wrong log is being examined.

Answers a, b, c, d, and e are correct. They are all reasons the syslog facility would not work as expected. Entries with typographical errors are ignored or cause other entries to be misinterpreted. The **syslogd** command reads the /etc/syslog.conf file only when it is started or when it receives the **SIGHUP** signal. The /etc/syslog.conf entry must match the expected facility/severity the user application is using to submit the messages. If the **syslogd** command is not running, it cannot receive and handle messages. Be certain that the messages are being sent to the intended log file.