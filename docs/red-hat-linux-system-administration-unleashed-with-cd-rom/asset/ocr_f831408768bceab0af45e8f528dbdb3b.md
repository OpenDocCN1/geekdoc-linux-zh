+   - limit [class-name] [max-users] [times] [message-file]—Allows the number of simultaneous users in a particular access class to be limited during certain times of day. The class-name parameter specifies the access class that is being limited. The max-users parameter sets the maximum number of simultaneous users for the given access class. The times parameter uses the same format as in the times located in the UUCP. sys file. message-file will be displayed to users denied access to the FTP server as a result of this command string.

+   - passwd-check none|trivial|rfc822 enforce|warn—Allows the level of password checking used by the FTP server to be configured. The first parameter in this command string specifies the type of password checking that should be used. The following password checking methods are supported:
+     - none—Disables password checking.
+     - trivial—Passwords are required to contain an "@" character.
+     - rfc822—Passwords are required to be an RFC822-compliant electronic mail address.

The second parameter in this command string specifies what action should be taken when the password checking mechanisms report an invalid password. This option may be set to either warn, which simply notifies the user of an invalid password use but allows them to log into the FTP server, or enforce, which notifies the user of the invalid password and disallows access to the server.

The ftpaccess file supports a number of logging mechanisms that are useful when engaging in post-mortem security auditing. The output of these logging mechanisms can also serve as input for automated host-based intrusion detection systems. The following logging capabilities are supported:

+   - loginfails [count]—Allows the threshold setting for repeated login failures message logging to be set to a user-definable value. The default setting for this threshold value is 5. This means that a message will be logged to the system logging facilities when an FTP client fails to log in to the FTP server more than four times during one particular session.

+   - log commands [keyword-list]—Allows the commands sent by FTP users to be logged for later analysis. The keyword-list parameter is a comma-separated list of keywords that allow logging to be defined for a particular type of FTP user. The anonymous, guest, and real keywords are supported. The anonymous keyword makes this command string apply only to anonymous FTP logins, the guest parameter applies only to guest accounts, and the real parameter applies to actual system users logged in to the FTP server.