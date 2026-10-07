value is stored with the encrypted password. When a user logs in and supplies a password, the salt is first retrieved from the stored encrypted password. The supplied password is then encoded with the salt value and compared with the stored password. If there is a match, the user is authenticated.

Because it is used to obtain user and group names from the system–held UIDs and GIDs, the `/etc/passwd` file must be readable by anyone on the system, and this makes it vulnerable to attack. Anyone can pull out a user’s encrypted password string and compare it against a generated list of dictionary words that have been encrypted using the same algorithm used to encode the password. A cracker trying to break the password generates the list by encrypting simple dictionary words using all 4096 salt values. If the password string matches one in the list, the person running the test has that user’s password. In order to combat this security risk, the concept of *shadowing* was adopted.

Shadowing solves the problem by relocating the passwords to another file (`/etc/shadow`). Only root can read and write to the `/etc/shadow` file. By default, most Linux distributions use shadow passwords. Listing 5.1 shown earlier reflects this fact; all its password entries are `x`, which indicates that the password is shadowed.

Refer back to the last line in Listing 5.1. The password field in the donald entry is replaced with an x. A line in `/etc/shadow` contains the encrypted version of Donald’s password as well as some other information:

```
donald:HcX5zb8cpoxmY:11088:0:99999:7:0::
```

The fields in the `/etc/shadow` file are as follows:

**Username** This is Donald’s login name, which matches the one we saw in the `/etc/passwd` file.

**Encrypted Password** This is where the actual encrypted password is stored on a system using password shadowing.

**Last Password Change** This is the date that the last password change took place written as the number of days since January 1, 1970.

**Days Until Change Allowed** This defines the number of days that must elapse between password changes. This is typically set to 0, allowing the user to change the password as often as desired.

**Days Before Change Required** This sets the maximum number of days the user will be allowed to keep the same password. After the specified time period, the user will be forced to change the password. If password changes are not forced, this field is set to 99999.

**Days Warning Before Password Expires** This field is used to set the number of days prior to password expiration you want the user to be notified. Typically the user is notified a week in advance, so this field is set to 7.

**Days Between Expiration and Deactivation** This sets the number of days that an account may be expired before the account is disabled. If inactivation is not intended to be automatic, the field is set to −1 or left empty.