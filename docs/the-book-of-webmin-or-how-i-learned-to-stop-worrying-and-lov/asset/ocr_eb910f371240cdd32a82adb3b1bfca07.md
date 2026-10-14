# Default warning days for new users

The system can warn users when they log in through a terminal if an enforced password change is approaching within the number of days specified here.

# Default inactive days for new users

If a user is inactive for the specified number of days after the maximum days specified above is reached, the account will be disabled. Only a system administrator will be able to re-enable the account.

# Display Options

The following options configure how the user and group information will be displayed for the system user and group list page, as well as the edit user and group pages:

# Maximum number of users to display

If there are more users than the number specified here, Webmin will display a search dialog allowing you to see only the users you need to see.

# Sort users and groups by

Webmin will sort the users and groups according to the selection here. The default is not to sort the names, and simply list them in the order they appear in the passwd and group files.

# Number of previous logins to display

When viewing the login history of a user using the Display logins by option, this option specifies how many previous logins will be displayed. Unlimited means Webmin will display all logins that exist in the log file. Because logs are rotated at some interval, you will never see logins older than the last log rotation.

# Display users and groups by

Depending on the number of users you have, and how much information you need to see on the front page, you may wish to display them by name only, or display them categorized by primary group. Displaying by name only can allow a much larger number of names to appear on screen at once and may be more convenient than the default in environments with hundreds or thousands of users.

# Conceal plain-text password?

If selected, the Normal password field in the Edit User and Create User pages will display * marks in place of the characters typed. If set to No, the typed characters will be displayed. It may be a security risk to leave this option disabled, if user passwords will be entered or changed in the presence of others.

# Get user and group info from

Webmin can usually gather user and group information using standard system calls. In some operating systems this may not work, or may not work as expected. In such cases, you can configure Webmin to draw the information from the