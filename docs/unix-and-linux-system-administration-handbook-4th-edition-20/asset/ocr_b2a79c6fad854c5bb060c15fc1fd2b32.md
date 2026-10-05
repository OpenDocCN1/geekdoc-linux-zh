# Chapter 7 Adding New Users

A typical shadow entry looks like this:

millert:$md5em5j8Lh$aIIQ3pXe0sakdRaRFyy7Ppj::14469:0:180:14:::

Here is a more complete description of each field:

+   * The login name is the same as in /etc/passwd. This field connects a user's password and shadow entries.

+   * The encrypted password is identical in concept and execution to the one previously stored in /etc/passwd: a fake MD5 password is shown.

+   * The last change field records the time at which the user's password was last changed. This field is filled in by the password command.

+   * The fourth field sets the number of days that must elapse between password changes. The idea is to force authentic changes by preventing users from immediately reverting to a familiar password after a required change. However, we think this feature could be dangerous when a security intrusion has occurred. We suggest setting this field to 0.

+   * The fifth field sets the maximum number of days allowed between password changes. This feature allows the administrator to enforce password aging: see page 906 for more information. Under Linux, the actual enforced maximum number of days is the sum of this field and the seventh(grace period) field.

+   * The sixth field sets the number of days before password expiration login should begin when the user of the expiring expiration.

+   * Solaris and HP-UX differ from Linux in their interpretation of the seventh field. Under Linux, the seventh field specifies how many days after the maximum password age has been reached to wait before treating the login as expired.

+   * The Solaris/HP-UX behavior is as follows: If a user has not logged in within the number of days specified in the seventh field, the account is disabled. Disused accounts are a target of hackers, and this feature attempts to give you to take such accounts "off the market." However, it only works if the user can be found in the /var/adm/lastlog file; users who have never logged in will not be automatically disabled. Ergo, this feature does not work in a networked environment because each host has its own lastlog file.

+   * The eighth field specifies the days (in days since January 1, 1970) on which the user's account will expire. The user may not log in after this date until the field has been reset by an administrator. If the field is left blank, the account will never expire.

On Linux you can use usermod to set the expiration field; it takes days in the format yyyy-mm-dd. Solaris’s usermod also computes days since